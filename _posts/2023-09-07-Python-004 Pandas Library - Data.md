---
title: 파이썬 판다스(Pandas) 데이터 구조
categories: Python
tags: 
  - Python
  - Pandas
  - Series
  - DataFrame
---

파이썬 Pandas 라이브러리에 대해 정리합니다.
판다스는 파이썬 데이터 처리를 위한 라이브러리이다.

# Pandas 데이터 구조

Pandas는 총 세 가지의 데이터 구조를 사용합니다.
- 시리즈(Series)
- 데이터프레임(DataFrame)
- 패널(Panel) / 추후 업로드

## 1. 시리즈

시리즈 클래스는 1차원 배열의 값에 각 값에 대응되는 인덱스를 부여할 수 있는 구조를 갖고 있다.


```python
import pandas as pd
sr = pd.Series([17000, 18000, 1000, 5000], index=["피자", "치킨", "콜라", "맥주"])
print(sr)
print(f"시리즈의 값 : {sr.values}")
print(f"시리즈의 인덱스 : {sr.index}")
```

    피자    17000
    치킨    18000
    콜라     1000
    맥주     5000
    dtype: int64
    시리즈의 값 : [17000 18000  1000  5000]
    시리즈의 인덱스 : Index(['피자', '치킨', '콜라', '맥주'], dtype='object')


## 2. 데이터프레임

데이터프레임은 2차원 리스트를 매개변수로 전달한다.  2차원이므로 행뱡향 인덱스(index)와 열방향 인덱스(column)가 존재한다.  
다시 말해, 행과 열을 가지는 자료구조이다.


```python
values = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
index = ["one", "two", "three"]
columns = ["A", "B", "C"]
df = pd.DataFrame(values, index=index, columns=columns)
print(df)
```

           A  B  C
    one    1  2  3
    two    4  5  6
    three  7  8  9


### 1) 데이터프레임의 생성

데이터프레임은 리스트, 시리즈, 딕셔너리, Numpy의 ndarrays, 또 다른 데이터프레임으로부터 생성할 수 있다.


```python
# 리스트로 생성하기
data = [
    ["1000", "Steve", 90.72], 
    ["1001", "James", 78.09], 
    ["1002", "Doyeon", 98.43], 
    ["1003", "Jane", 64.19], 
    ["1004", "Pilwoong", 81.30],
    ["1005", "Tony", 99.14],
]

df = pd.DataFrame(data)
print(df)
```

          0         1      2
    0  1000     Steve  90.72
    1  1001     James  78.09
    2  1002    Doyeon  98.43
    3  1003      Jane  64.19
    4  1004  Pilwoong  81.30
    5  1005      Tony  99.14


열 이름 지정


```python
df = pd.DataFrame(data, columns=["학번", "이름", "점수"])
print(df)
```

         학번        이름     점수
    0  1000     Steve  90.72
    1  1001     James  78.09
    2  1002    Doyeon  98.43
    3  1003      Jane  64.19
    4  1004  Pilwoong  81.30
    5  1005      Tony  99.14


딕셔너리로 데이터프레임 생성


```python
data = {
    "학번" : ["1000", "1001", "1002", "1003", "1004", "1005"],
    "이름" : ["Steve", "James", "Doyeon", "Jane", "Pilwoong", "Tony"],
    "점수" : [90.72, 78.09, 98.43, 64.19, 81.30, 99.14]
}
df_dict = pd.DataFrame(data)
print(df_dict)
```

         학번        이름     점수
    0  1000     Steve  90.72
    1  1001     James  78.09
    2  1002    Doyeon  98.43
    3  1003      Jane  64.19
    4  1004  Pilwoong  81.30
    5  1005      Tony  99.14


### 2) 데이터프레임 조회


```python
# 앞 부분을 3개만 보기
print(df.head(3))
```

         학번      이름     점수
    0  1000   Steve  90.72
    1  1001   James  78.09
    2  1002  Doyeon  98.43



```python
# 뒷 부분을 3개만 보기
print(df.tail(3))
```

         학번        이름     점수
    3  1003      Jane  64.19
    4  1004  Pilwoong  81.30
    5  1005      Tony  99.14



```python
# 열 조회
print(df["학번"])
```

    0    1000
    1    1001
    2    1002
    3    1003
    4    1004
    5    1005
    Name: 학번, dtype: object


### 3) 외부 데이터 읽기

Pandas는 CSV, 텍스트, Excel, SQL, HTML, JSON 등 다양한 데이터 파일을 읽고 데이터 프레임을 생성할 수 있다.


```python
df = pd.read_csv("dataframe.csv")
print(df)
```

       student id name  score
    0           1   aa     10
    1           2   bb     20
    2           3   cc     30
    3           4   dd     40


이 경우 인덱스가 자동으로 부여된다.


```python
print(df.index)
```

    RangeIndex(start=0, stop=4, step=1)

