---
title: KNN - 구현
categories: ML-Algorithm
tags:
  - KNN
  - ML
  - Python
  - Numpy
---

### 히스토그램 그래프 구현

```python
import matplotlib.pyplot as plt
import numpy as np

data = np.random.normal(0, 1, size=10)

fig, ax = plt.subplots(figsize=(5, 5))

ax.hist(x=data)

```




    (array([1., 0., 1., 2., 0., 0., 2., 3., 0., 1.]),
     array([-2.32546836, -1.94938303, -1.57329769, -1.19721236, -0.82112703,
            -0.4450417 , -0.06895636,  0.30712897,  0.6832143 ,  1.05929964,
             1.43538497]),
     <BarContainer object of 10 artists>)




    
![png](/images/ml/knn/knn_01.png)
    


### data set 생성


```python
import matplotlib.pyplot as plt
import numpy as np

x_data = np.random.normal(loc=5, scale=1, size=(100, 1))
y_data = np.random.normal(loc=3, scale=1, size=(100, 1))

# zip
# data = np.array(list(zip(x_data, y_data)))

# 전치행렬
# data = np.array([x_data, y_data]).T

# concat
# data = np.concatenate([x_data, y_data], axis=1)

# normal
data = np.random.normal(loc=[5, 3], scale=[1, 1], size=(100, 2))

print(f"mean = {np.mean(data, axis=0)}")
print(f"std = {np.std(data, axis=0)}")
```

    mean = [4.99971037 3.01467485]
    std = [1.02003973 0.97765966]


### centroid


```python
import matplotlib.pyplot as plt
import numpy as np

centroid = np.random.randint(-5, 5, size=2)

print(f"cent = {centroid}")

data = np.random.normal(loc=centroid, scale=[1, 2], size=(100, 2))

print(f"mean = {data.mean(axis=0)}")
print(f"std = {data.std(axis=0)}")

fig, ax = plt.subplots(figsize=(7, 7))

ax.scatter(centroid[0], centroid[1], color='red', s=100)
ax.scatter(data[:,0], data[:,1])


```

    cent = [-4  4]
    mean = [-3.99231889  4.11606231]
    std = [1.04389966 1.81089299]





    <matplotlib.collections.PathCollection at 0x11e5aff90>




    
![png](/images/ml/knn/knn_02.png)
    


### cluster (class dataset)


```python
import matplotlib.pyplot as plt
import numpy as np

centroids = np.random.randint(-10, 10, size=(4, 2))

data_set = np.vstack(
    [
        np.random.normal(loc=cent, scale=1, size=(100, 2)) 
        for cent in centroids
    ]
)

fig, ax = plt.subplots(figsize=(6, 6))

for (idx_cent, cent) in enumerate(centroids):
    unit = 100
    start = idx_cent * unit
    end = start + unit
    data = data_set[start:end]
    ax.scatter(x=data[:, 0], y=data[:, 1])
    ax.scatter(x=cent[0], y=cent[1], color="purple", marker="x", s=100)
```


    
![png](/images/ml/knn/knn_03.png)
    


### targets


```python
import matplotlib.pyplot as plt
import numpy as np

for i in range(4):
    print(
        np.full(shape=(100,), fill_value=i)
    )
```

    [0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
     0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
     0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0]
    [1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
     1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
     1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1]
    [2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2
     2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2
     2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2]
    [3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3
     3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3
     3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3]


### KNN 구현


```python
import matplotlib.pyplot as plt
import numpy as np
import operator

# Data set 생성
centroids = np.random.randint(-10, 11, size=(5, 2))
test_centroids = centroids[0]
data_centroids = centroids[1:]
range_data_centroids = range(len(data_centroids))
unit = 100
y = np.hstack([
        np.full(shape=(unit,), fill_value=i)
        for i in range_data_centroids
    ])
data_set = np.vstack([
        np.random.normal(loc=data_centroids[i], scale=1, size=(unit, 2))
        for i in range_data_centroids
    ])
test_size = 10
test_set = np.random.normal(loc=test_centroids, scale=1, size=(test_size, 2))

# euclidean distance 구하기
def classify(data_set, test_set, K: int) -> list[int]:
    classifications = [ -1 for _ in range(len(test_set)) ]
    for (idx_test, test) in enumerate(test_set):
        diffs = abs(data_set - test)
        euclidean_distances = (diffs.sum(axis=1) ** 0.5).reshape(-1, 1)
        concatenated = np.concatenate([ euclidean_distances, y.reshape(-1, 1) ], axis=1)
        sorted_euclidean_distances = concatenated[concatenated[:, 0].argsort()]
        K_distances = sorted_euclidean_distances[:K]
        count_list = [ 0 for _ in range_data_centroids ]
        for (_, clazz) in K_distances:
            count_list[int(clazz)] += 1
        (max_index, _) = max(enumerate(count_list), key=operator.itemgetter(1))
        classifications[idx_test] = max_index
    return classifications

classifications = classify(data_set=data_set, test_set=test_set, K=5)

# knn visualization
fig, ax = plt.subplots(figsize=(8, 8))
color_list = ["blue", "red", "green", "orange"]
for (idx_centroids, centroid) in enumerate(data_centroids):
    start = idx_centroids * unit
    end = start + unit
    data = data_set[start:end]
    ax.scatter(x=data[:, 0], y=data[:, 1], s=10, color=color_list[idx_centroids])

for idx_test, test in enumerate(test_set):
    ax.scatter(x=test[0],y=test[1], s=20, color=color_list[classifications[idx_test]])
    ax.annotate(f" {classifications[idx_test]}", xy=(test[0], test[1]))

x_min, x_max = ax.get_xlim()
y_min, y_max = ax.get_ylim()
x_mesh = np.linspace(start=x_min, stop=x_max, num=(abs(int(x_max))+abs(int(x_min))) * 7)
y_mesh = np.linspace(start=y_min, stop=y_max, num=(abs(int(y_max))+abs(int(y_min))) * 7)
xx,yy = np.meshgrid(x_mesh, y_mesh)
background = np.concatenate([xx.flatten().reshape(-1, 1), yy.flatten().reshape(-1, 1)], axis=1)
boundary_classifications = classify(data_set=data_set, test_set=background, K=5)
ax.scatter(
    x=background[:, 0], 
    y=background[:, 1],
    c=[ color_list[i] for i in boundary_classifications],
    alpha=0.1, s=10
)
x_center, y_center = (abs(x_max) - abs(x_min))/2, (abs(y_max) - abs(y_min))/2
ax.text(x_center, y_center, "classes")
for (x, y) in test_set:
    ax.plot((x, x_center), (y, y_center), color="gray", linestyle="dotted")
```


    
![png](/images/ml/knn/knn_04.png)
