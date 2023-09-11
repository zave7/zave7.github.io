---
title: 파이썬 판다스(Pandas) 데이터프레임
categories: Python
tags: 
  - Python
  - Pandas
  - DataFrame
---

# 데이터 프레임
[Pandas DataFrame 공식문서](https://pandas.pydata.org/docs/reference/frame.html)
- 2차원 데이터 구조이다.
- 행과 열로 구성되어있다.
- 각 열은 각각의 데이터 타입을 가진다.

### 1. 생성


#### - list 를 통해 생성


```python
import pandas as pd

data_list = [
    [1, 2, 3, 4, 5],
    [6, 7 , 8, 9, 10]
]

df_list = pd.DataFrame(data = data_list, columns = ["하나", "둘", "셋", "넷", "다섯"])
print(df_list)
```

       하나  둘  셋  넷  다섯
    0   1  2  3  4   5
    1   6  7  8  9  10


#### - dictionary 를 통해 생성



```python
data_dictionary = {
    "삼성전자": [10000, 20000, 30000],
    "SK텔레콤": [10500, 20500, 30500]
}
df_dictionary = pd.DataFrame(data_dictionary)
print(df_dictionary)
```

        삼성전자  SK텔레콤
    0  10000  10500
    1  20000  20500
    2  30000  30500


### 2. 속성

DataFrame은 다음의 속성을 가진다.
- index : index (기본 값을 RangeIndex
- columns : column 명
- values : numpy array 형식의 데이터 값
- dtypes : column 별 데이터 타입
- T : DataFrame을 전치(Transpose) - 행렬의 행과 열을 바꾸어 얻어낸 행렬


```python
print(f"인덱스 :{df_dictionary.index}")
print(f"컬럼 : {df_dictionary.columns}")
print(f"값 : {df_dictionary.values}")
print(f"데이터 타입 : {df_dictionary.dtypes}")
print(f"전치 : {df_dictionary.T}")
```

    인덱스 : RangeIndex(start=0, stop=3, step=1)
    컬럼 : Index(['삼성전자', 'SK텔레콤'], dtype='object')
    값 : 
     [[10000 10500]
      [20000 20500]
      [30000 30500]]
    데이터 타입 : 
        삼성전자     int64
        SK텔레콤    int64
        dtype: object
    전치 :            
                0      1      2
    삼성전자   10000  20000  30000
    SK텔레콤  10500  20500  30500


### 3. 조회

- loc : index, 컬럼으로 데이터를 가져온다
- iloc : 데이터 순서로 데이터를 가져온다


```python
print(f"loc : \n{df_dictionary.loc[:, '삼성전자']}")
print(f"iloc : \n{df_dictionary.iloc[0, 0]}")

```

    loc : 
    0    10000
    1    20000
    2    30000
    Name: 삼성전자, dtype: int64
    iloc : 
    10000


- 특정 컬럼 조회


```python
print(f"컬럼 조회 : \n{df_dictionary['SK텔레콤']}")
print(f"컬럼 속성으로 조회 : \n{df_dictionary.SK텔레콤}")
```

    컬럼 조회 : 
    0    10500
    1    20500
    2    30500
    Name: SK텔레콤, dtype: int64
    컬럼 속성으로 조회 : 
    0    10500
    1    20500
    2    30500
    Name: SK텔레콤, dtype: int64


### 3. Index 지정


```python
df_dictionary.index = list("abc")
print(df_dictionary)
```

    <bound method DataFrame.__len__ of     삼성전자  SK텔레콤
    a  10000  10500
    b  20000  20500
    c  30000  30500>
        삼성전자  SK텔레콤
    a  10000  10500
    b  20000  20500
    c  30000  30500


### 4. 컬럼 다루기

DataFrame에 Key 값으로 column의 이름을 지정하여 column을 선택할 수 있다.

1개의 column을 가져올 수 있으며, <b>1개의 column 선택시 Series</b>가 된다.


```python
print(df_dictionary["삼성전자"])
print(type(df_dictionary["삼성전자"]))
```

    a    10000
    b    20000
    c    30000
    Name: 삼성전자, dtype: int64
    <class 'pandas.core.series.Series'>


2개 이상의 column 선택은 fancy indexing으로 가능하다.


```python
fancy_indexing = df_dictionary[["삼성전자", "SK텔레콤"]]
print(fancy_indexing)
print(type(fancy_indexing))
print(df_dictionary.loc[:, "삼성전자"])

```

        삼성전자  SK텔레콤
    a  10000  10500
    b  20000  20500
    c  30000  30500
    <class 'pandas.core.frame.DataFrame'>
    a    10000
    b    20000
    c    30000
    Name: 삼성전자, dtype: int64


### 5. 시리즈, 데이터 프레임 확장

#### 1) 시리즈 확장


```python
import pandas as pd

series_concat_1 = pd.Series([1, 2, 3, 4, 5], index = [1, 2, 3, 4, 5])
series_concat_2 = pd.Series([6, 7, 8, 9, 10])
print(f"axis 0 :\n{pd.concat([series_concat_1, series_concat_2])}") # axis 값이 0 이기 때문에
```

    axis 0 :
    1     1
    2     2
    3     3
    4     4
    5     5
    0     6
    1     7
    2     8
    3     9
    4    10
    dtype: int64


기본 axis 값이 0 이기 때문에 행방향으로 합쳐졌다.


```python
print(f"axis = 1:\n{pd.concat([series_concat_1, series_concat_2], axis = 1)}")
```

    axis = 1:
         0     1
    1  1.0   7.0
    2  2.0   8.0
    3  3.0   9.0
    4  4.0  10.0
    5  5.0   NaN
    0  NaN   6.0


첫번째 시리즈를 기준으로 axis 1 방향으로 합쳐진 후 인덱스가 일치하지 않는 행의 경우 추가된다.<br>
아래는 순서를 바꿔서 출력해보았다.


```python
print(f"axis = 1:\n{pd.concat([series_concat_2, series_concat_1], axis = 1)}")
```

    axis = 1:
          0    1
    0   6.0  NaN
    1   7.0  1.0
    2   8.0  2.0
    3   9.0  3.0
    4  10.0  4.0
    5   NaN  5.0


join으로 집합 연산을 할 수 있다. default는 "outer"이다.


```python
# inner 교집합
print(f"axis = 1:\n{pd.concat([series_concat_2, series_concat_1], axis = 1, join = 'inner')}")
```

    axis = 1:
        0  1
    1   7  1
    2   8  2
    3   9  3
    4  10  4



```python
# outer
print(f"axis = 1:\n{pd.concat([series_concat_2, series_concat_1], axis = 1, join = 'outer')}")
```

    axis = 1:
          0    1
    0   6.0  NaN
    1   7.0  1.0
    2   8.0  2.0
    3   9.0  3.0
    4  10.0  4.0
    5   NaN  5.0


### 6. 연산

#### 1) 시리즈 연산

- 사칙연산


```python
series_op = pd.Series([1, 2, 3, 4, 5])
print(f"더하기:\n{series_op + 2}")
print(f"빼기:\n{series_op - 2}")
print(f"곱하기:\n{series_op * 2}")
print(f"나누기:\n{series_op / 2}")
```

    더하기:
    0    3
    1    4
    2    5
    3    6
    4    7
    dtype: int64
    빼기:
    0   -1
    1    0
    2    1
    3    2
    4    3
    dtype: int64
    곱하기:
    0     2
    1     4
    2     6
    3     8
    4    10
    dtype: int64
    나누기:
    0    0.5
    1    1.0
    2    1.5
    3    2.0
    4    2.5
    dtype: float64


- 시리즈 연산


```python
series_op_2 = pd.Series([1, 1, 1, 1, 1])
print(f"시리즈 더하기:\n{series_op + series_op_2}")
print(f"시리즈 빼기:\n{series_op - series_op_2}")
print(f"시리즈 곱하기:\n{series_op * series_op_2}")
print(f"시리즈 나누기:\n{series_op / series_op_2}")
```

    시리즈 더하기:
    0    2
    1    3
    2    4
    3    5
    4    6
    dtype: int64
    시리즈 빼기:
    0    0
    1    1
    2    2
    3    3
    4    4
    dtype: int64
    시리즈 곱하기:
    0    1
    1    2
    2    3
    3    4
    4    5
    dtype: int64
    시리즈 나누기:
    0    1.0
    1    2.0
    2    3.0
    3    4.0
    4    5.0
    dtype: float64


#### 2) 데이터 프레임 연산

- concat : 그냥 가져다 붙이는 경우
- merge : 공통된 컬럼이나 인덱스가 있는 경우


```python
df_1 = pd.DataFrame({'a':['a0','a1','a2','a3'],
                   'b':['b0','b1','b2','b3'],
                   'c':['c0','c1','c2','c3']},
                  index = [0,1,2,3])
df_2 = pd.DataFrame({'a':['a2','a3','a4','a5'],
                   'b':['b2','b3','b4','b5'],
                   'c':['c2','c3','c4','c5'],
                   'd':['d2','d3','d4','d5']},
                   index = [2,3,4,5])
```

concat 연산 (axis 0)


```python
concat_0 = pd.concat([df_1, df_2])
print(concat_0)
```

        a   b   c    d
    0  a0  b0  c0  NaN
    1  a1  b1  c1  NaN
    2  a2  b2  c2  NaN
    3  a3  b3  c3  NaN
    2  a2  b2  c2   d2
    3  a3  b3  c3   d3
    4  a4  b4  c4   d4
    5  a5  b5  c5   d5


df1 기준으로 없는 열은 NaN 값이 채워진다.<br>
다음은 axis 1 기준으로 concat 해보았다.


```python
concat_1 = pd.concat([df_1, df_2], axis = 1)
print(concat_1)
```

         a    b    c    a    b    c    d
    0   a0   b0   c0  NaN  NaN  NaN  NaN
    1   a1   b1   c1  NaN  NaN  NaN  NaN
    2   a2   b2   c2   a2   b2   c2   d2
    3   a3   b3   c3   a3   b3   c3   d3
    4  NaN  NaN  NaN   a4   b4   c4   d4
    5  NaN  NaN  NaN   a5   b5   c5   d5


인덱스 기준으로 합쳐졌으며 인덱스에 해당하는 값이 없는 경우 NaN으로 채워진다.

### 7. 결측치 처리

- 제거 : dropna
- 대체 : filna, interpolate

#### dropna


```python
import numpy as np

df_na = pd.concat([df_1, df_2])
print(f"<axis 0>:\n{df_na.dropna()}") # 결측값이 있는 행 제거
print(f"<axis 1>:\n{df_na.dropna(axis = 1)}") # 결측값이 있는 열 제거

```

    <axis 0>:
        a   b   c   d
    2  a2  b2  c2  d2
    3  a3  b3  c3  d3
    4  a4  b4  c4  d4
    5  a5  b5  c5  d5
    <axis 1>:
        a   b   c
    0  a0  b0  c0
    1  a1  b1  c1
    2  a2  b2  c2
    3  a3  b3  c3
    2  a2  b2  c2
    3  a3  b3  c3
    4  a4  b4  c4
    5  a5  b5  c5


#### filna

값 대체


```python
df_na = pd.concat([df_1, df_2])
print(f"<axis 0>:\n{df_na.fillna(0)}")
print(f"<axis 1>:\n{df_na.fillna(0, axis = 1)}")
```

    <axis 0>:
        a   b   c   d
    0  a0  b0  c0   0
    1  a1  b1  c1   0
    2  a2  b2  c2   0
    3  a3  b3  c3   0
    2  a2  b2  c2  d2
    3  a3  b3  c3  d3
    4  a4  b4  c4  d4
    5  a5  b5  c5  d5
    <axis 1>:
        a   b   c   d
    0  a0  b0  c0   0
    1  a1  b1  c1   0
    2  a2  b2  c2   0
    3  a3  b3  c3   0
    2  a2  b2  c2  d2
    3  a3  b3  c3  d3
    4  a4  b4  c4  d4
    5  a5  b5  c5  d5


방향에 해당하는 값으로 대체


```python
df_na = pd.concat([df_1, df_2])
df_ffill = df_na.fillna(method = "ffill")
df_bfill = df_na.fillna(method = "bfill")
print(f"앞의 값으로 채우기 : {df_ffill}") # 첫 행부터는 값이 없으므로 그대로 결측치값이 남음
print(f"뒤의 값으로 채우기 : {df_bfill}")
```

    앞의 값으로 채우기 :     a   b   c    d
    0  a0  b0  c0  NaN
    1  a1  b1  c1  NaN
    2  a2  b2  c2  NaN
    3  a3  b3  c3  NaN
    2  a2  b2  c2   d2
    3  a3  b3  c3   d3
    4  a4  b4  c4   d4
    5  a5  b5  c5   d5
    뒤의 값으로 채우기 :     a   b   c   d
    0  a0  b0  c0  d2
    1  a1  b1  c1  d2
    2  a2  b2  c2  d2
    3  a3  b3  c3  d2
    2  a2  b2  c2  d2
    3  a3  b3  c3  d3
    4  a4  b4  c4  d4
    5  a5  b5  c5  d5


앞/뒤 방향으로 결측값 채우는 횟수를 제한하기


```python
df_na = pd.concat([df_1, df_2])
df_b_limmit = df_na.fillna(method = "bfill", limit = 2)
print(f"뒤의 값으로 2개까지만 채우기 : {df_b_limmit}")
```

    뒤의 값으로 2개까지만 채우기 :     a   b   c    d
    0  a0  b0  c0  NaN
    1  a1  b1  c1  NaN
    2  a2  b2  c2   d2
    3  a3  b3  c3   d2
    2  a2  b2  c2   d2
    3  a3  b3  c3   d3
    4  a4  b4  c4   d4
    5  a5  b5  c5   d5


결측값을 변수별 평균으로 대체하기


```python
df_na = pd.DataFrame(
    {
        "a": [1, 2, 3, 4],
        "b": [4, float('NaN'), float('NaN'), 7],
        "c": [7, 8, 9, 10],
        "d": [10, float('nan'), 12, 13],
        "e": [13, 14, 15, 16]
    }
)
df_m: pd.Series = df_na.mean()
print(f"평균값 시리즈 :\n{df_m}")
df_na.fillna(df_m)
```

    평균값 시리즈 :
    a     2.500000
    b     5.500000
    c     8.500000
    d    11.666667
    e    14.500000
    dtype: float64





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
      <th>e</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>4.0</td>
      <td>7</td>
      <td>10.000000</td>
      <td>13</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>5.5</td>
      <td>8</td>
      <td>11.666667</td>
      <td>14</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>5.5</td>
      <td>9</td>
      <td>12.000000</td>
      <td>15</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>7.0</td>
      <td>10</td>
      <td>13.000000</td>
      <td>16</td>
    </tr>
  </tbody>
</table>
</div>



특정 컬럼 평균으로 대체하기


```python
df_na = pd.DataFrame(
    {
        "a": [1, 2, 3, 4],
        "b": [4, float('NaN'), float('NaN'), 7],
        "c": [7, 8, 9, 10],
        "d": [10, float('nan'), 12, 13],
        "e": [13, 14, 15, 16]
    }
)
df_m: pd.Series = df_na.mean()
print(f"1개 열 :\n{df_na.fillna(df_m['a'])}")
print(f"여러개 열 :\n{df_na.fillna(df_m['a':'b'])}")

```

    1개 열 :
       a    b   c     d   e
    0  1  4.0   7  10.0  13
    1  2  2.5   8   2.5  14
    2  3  2.5   9  12.0  15
    3  4  7.0  10  13.0  16
    여러개 열 :
       a    b   c     d   e
    0  1  4.0   7  10.0  13
    1  2  5.5   8   NaN  14
    2  3  5.5   9  12.0  15
    3  4  7.0  10  13.0  16


결측값을 다른 변수의 값으로 대체


```python
df_na = pd.DataFrame(
    {
        "a": [1, 2, 3, 4],
        "b": [4, float('NaN'), float('NaN'), 7],
        "c": [7, 8, 9, 10],
        "d": [10, float('nan'), 12, 13],
        "e": [13, 14, 15, 16]
    }
)

df_na["b_new"] = np.where(pd.isnull(df_na["b"]), df_na["a"], df_na["b"])
df_na
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
      <th>e</th>
      <th>b_new</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>4.0</td>
      <td>7</td>
      <td>10.0</td>
      <td>13</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>NaN</td>
      <td>8</td>
      <td>NaN</td>
      <td>14</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>NaN</td>
      <td>9</td>
      <td>12.0</td>
      <td>15</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>7.0</td>
      <td>10</td>
      <td>13.0</td>
      <td>16</td>
      <td>7.0</td>
    </tr>
  </tbody>
</table>
</div>



### interpolate

데이터 결측치를 보간하여 대체


```python
df_interpolate = pd.DataFrame(
    {
        "a": [1, 6, 3, 4],
        "b": [4, float('NaN'), 6, 7],
        "c": [7, 8, 9, 10],
        "d": [10, float('nan'), 12, 13],
        "e": [13, 14, 15, 16]
    }
)
```

선형 보간
- [API reference](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.interpolate.html)


```python
print(f"axis 0:\n{df_interpolate.interpolate(axis = 0)}") # method 기본값인 "linear", 값을 동일한 간격으로 처리
print(f"axis 1:\n{df_interpolate.interpolate(axis = 1)}")
```

    axis 0:
       a    b   c     d   e
    0  1  4.0   7  10.0  13
    1  6  5.0   8  11.0  14
    2  3  6.0   9  12.0  15
    3  4  7.0  10  13.0  16
    axis 1:
         a    b     c     d     e
    0  1.0  4.0   7.0  10.0  13.0
    1  6.0  7.0   8.0  11.0  14.0
    2  3.0  6.0   9.0  12.0  15.0
    3  4.0  7.0  10.0  13.0  16.0


### 8. 중복 제거


```python
df_duplicate = pd.concat([df_1, df_1])
print(f"중복 제거 전 :\n{df_duplicate}")

df_duplicate_drop = pd.DataFrame(
        {
            'id': [1, 2, 3, 4, 6, 6, 6, 8, 9, 10],
            'name': [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
        }
    ).drop_duplicates()
print(f"중복 제거 후 :\n{df_duplicate.drop_duplicates()}")

# id열만 중복 제거하여 데이터 프레임으로 변환
col_duplicate_drop = df_duplicate_drop.drop_duplicates(subset = "id", keep = "first") # keep : 'fisrt' - 중복 첫번째 행만 제외하고 삭제, 'last' - 중복 마지막 행만 제외하고 삭제, False - 중복되는 행을 모두 삭제
print(f"id열 기준으로 중복 제거 :\n{col_duplicate_drop}")
```

    중복 제거 전 :
        a   b   c
    0  a0  b0  c0
    1  a1  b1  c1
    2  a2  b2  c2
    3  a3  b3  c3
    0  a0  b0  c0
    1  a1  b1  c1
    2  a2  b2  c2
    3  a3  b3  c3
    중복 제거 후 :
        a   b   c
    0  a0  b0  c0
    1  a1  b1  c1
    2  a2  b2  c2
    3  a3  b3  c3
    id열 기준으로 중복 제거 :
       id  name
    0   1     1
    1   2     2
    2   3     3
    3   4     4
    4   6     5
    7   8     8
    8   9     9
    9  10    10
    <class 'pandas.core.frame.DataFrame'>

