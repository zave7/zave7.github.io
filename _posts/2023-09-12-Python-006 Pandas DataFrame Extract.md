---
title: 파이썬 판다스(Pandas) 데이터프레임 데이터 추출
categories: Python
tags: 
  - Python
  - Pandas
  - DataFrame
  - Operation
---
# 데이터프레임 데이터 추출


```python
import pandas as pd

df = pd.read_csv("https://raw.githubusercontent.com/jin0choi1216/dataset/main/AAPL.csv", index_col = 0)
df.head(5)
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
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2012-01-03</th>
      <td>14.621429</td>
      <td>14.732143</td>
      <td>14.607143</td>
      <td>14.686786</td>
      <td>12.466090</td>
      <td>302220800</td>
    </tr>
    <tr>
      <th>2012-01-04</th>
      <td>14.642857</td>
      <td>14.810000</td>
      <td>14.617143</td>
      <td>14.765714</td>
      <td>12.533089</td>
      <td>260022000</td>
    </tr>
    <tr>
      <th>2012-01-05</th>
      <td>14.819643</td>
      <td>14.948214</td>
      <td>14.738214</td>
      <td>14.929643</td>
      <td>12.672229</td>
      <td>271269600</td>
    </tr>
    <tr>
      <th>2012-01-06</th>
      <td>14.991786</td>
      <td>15.098214</td>
      <td>14.972143</td>
      <td>15.085714</td>
      <td>12.804703</td>
      <td>318292800</td>
    </tr>
    <tr>
      <th>2012-01-09</th>
      <td>15.196429</td>
      <td>15.276786</td>
      <td>15.048214</td>
      <td>15.061786</td>
      <td>12.784389</td>
      <td>394024400</td>
    </tr>
  </tbody>
</table>
</div>



### 1. 데이터 추출하기

#### 1) 비교 연산


```python
df[(df["Close"] >= 150) & (df["Open"] >= 160) ]
df.query("(Close >= 150) and (Open >= 160)") # 같은 쿼리
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
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2021-11-22</th>
      <td>161.679993</td>
      <td>165.699997</td>
      <td>161.000000</td>
      <td>161.020004</td>
      <td>159.410767</td>
      <td>117467900</td>
    </tr>
    <tr>
      <th>2021-11-23</th>
      <td>161.119995</td>
      <td>161.800003</td>
      <td>159.059998</td>
      <td>161.410004</td>
      <td>159.796844</td>
      <td>96041900</td>
    </tr>
    <tr>
      <th>2021-11-24</th>
      <td>160.750000</td>
      <td>162.139999</td>
      <td>159.639999</td>
      <td>161.940002</td>
      <td>160.321533</td>
      <td>69463600</td>
    </tr>
    <tr>
      <th>2021-12-01</th>
      <td>167.479996</td>
      <td>170.300003</td>
      <td>164.529999</td>
      <td>164.770004</td>
      <td>163.123276</td>
      <td>152052500</td>
    </tr>
    <tr>
      <th>2021-12-03</th>
      <td>164.020004</td>
      <td>164.960007</td>
      <td>159.720001</td>
      <td>161.839996</td>
      <td>160.222549</td>
      <td>118023100</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2023-08-21</th>
      <td>175.070007</td>
      <td>176.130005</td>
      <td>173.740005</td>
      <td>175.839996</td>
      <td>175.839996</td>
      <td>46311900</td>
    </tr>
    <tr>
      <th>2023-08-22</th>
      <td>177.059998</td>
      <td>177.679993</td>
      <td>176.250000</td>
      <td>177.229996</td>
      <td>177.229996</td>
      <td>42084200</td>
    </tr>
    <tr>
      <th>2023-08-23</th>
      <td>178.520004</td>
      <td>181.550003</td>
      <td>178.330002</td>
      <td>181.119995</td>
      <td>181.119995</td>
      <td>52722800</td>
    </tr>
    <tr>
      <th>2023-08-24</th>
      <td>180.669998</td>
      <td>181.100006</td>
      <td>176.009995</td>
      <td>176.380005</td>
      <td>176.380005</td>
      <td>54945800</td>
    </tr>
    <tr>
      <th>2023-08-25</th>
      <td>177.380005</td>
      <td>179.149994</td>
      <td>175.820007</td>
      <td>178.610001</td>
      <td>178.610001</td>
      <td>51418700</td>
    </tr>
  </tbody>
</table>
<p>224 rows × 6 columns</p>
</div>



#### 2) 질의


```python
 # 문자열 query
df.query("Volume > 100000000")
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
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2012-01-03</th>
      <td>14.621429</td>
      <td>14.732143</td>
      <td>14.607143</td>
      <td>14.686786</td>
      <td>12.466090</td>
      <td>302220800</td>
    </tr>
    <tr>
      <th>2012-01-04</th>
      <td>14.642857</td>
      <td>14.810000</td>
      <td>14.617143</td>
      <td>14.765714</td>
      <td>12.533089</td>
      <td>260022000</td>
    </tr>
    <tr>
      <th>2012-01-05</th>
      <td>14.819643</td>
      <td>14.948214</td>
      <td>14.738214</td>
      <td>14.929643</td>
      <td>12.672229</td>
      <td>271269600</td>
    </tr>
    <tr>
      <th>2012-01-06</th>
      <td>14.991786</td>
      <td>15.098214</td>
      <td>14.972143</td>
      <td>15.085714</td>
      <td>12.804703</td>
      <td>318292800</td>
    </tr>
    <tr>
      <th>2012-01-09</th>
      <td>15.196429</td>
      <td>15.276786</td>
      <td>15.048214</td>
      <td>15.061786</td>
      <td>12.784389</td>
      <td>394024400</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2023-02-03</th>
      <td>148.029999</td>
      <td>157.380005</td>
      <td>147.830002</td>
      <td>154.500000</td>
      <td>153.843628</td>
      <td>154357300</td>
    </tr>
    <tr>
      <th>2023-05-05</th>
      <td>170.979996</td>
      <td>174.300003</td>
      <td>170.759995</td>
      <td>173.570007</td>
      <td>173.096512</td>
      <td>113316400</td>
    </tr>
    <tr>
      <th>2023-06-05</th>
      <td>182.630005</td>
      <td>184.949997</td>
      <td>178.039993</td>
      <td>179.580002</td>
      <td>179.337830</td>
      <td>121946500</td>
    </tr>
    <tr>
      <th>2023-06-16</th>
      <td>186.729996</td>
      <td>186.990005</td>
      <td>184.270004</td>
      <td>184.919998</td>
      <td>184.670624</td>
      <td>101235600</td>
    </tr>
    <tr>
      <th>2023-08-04</th>
      <td>185.520004</td>
      <td>187.380005</td>
      <td>181.919998</td>
      <td>181.990005</td>
      <td>181.744583</td>
      <td>115799700</td>
    </tr>
  </tbody>
</table>
<p>1997 rows × 6 columns</p>
</div>




```python
# 인덱스 컬럼 기준 query
df.query("Date > '2020-01-01'")
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
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-02</th>
      <td>74.059998</td>
      <td>75.150002</td>
      <td>73.797501</td>
      <td>75.087502</td>
      <td>73.249023</td>
      <td>135480400</td>
    </tr>
    <tr>
      <th>2020-01-03</th>
      <td>74.287498</td>
      <td>75.144997</td>
      <td>74.125000</td>
      <td>74.357498</td>
      <td>72.536888</td>
      <td>146322800</td>
    </tr>
    <tr>
      <th>2020-01-06</th>
      <td>73.447502</td>
      <td>74.989998</td>
      <td>73.187500</td>
      <td>74.949997</td>
      <td>73.114883</td>
      <td>118387200</td>
    </tr>
    <tr>
      <th>2020-01-07</th>
      <td>74.959999</td>
      <td>75.224998</td>
      <td>74.370003</td>
      <td>74.597504</td>
      <td>72.771019</td>
      <td>108872000</td>
    </tr>
    <tr>
      <th>2020-01-08</th>
      <td>74.290001</td>
      <td>76.110001</td>
      <td>74.290001</td>
      <td>75.797501</td>
      <td>73.941643</td>
      <td>132079200</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2023-08-21</th>
      <td>175.070007</td>
      <td>176.130005</td>
      <td>173.740005</td>
      <td>175.839996</td>
      <td>175.839996</td>
      <td>46311900</td>
    </tr>
    <tr>
      <th>2023-08-22</th>
      <td>177.059998</td>
      <td>177.679993</td>
      <td>176.250000</td>
      <td>177.229996</td>
      <td>177.229996</td>
      <td>42084200</td>
    </tr>
    <tr>
      <th>2023-08-23</th>
      <td>178.520004</td>
      <td>181.550003</td>
      <td>178.330002</td>
      <td>181.119995</td>
      <td>181.119995</td>
      <td>52722800</td>
    </tr>
    <tr>
      <th>2023-08-24</th>
      <td>180.669998</td>
      <td>181.100006</td>
      <td>176.009995</td>
      <td>176.380005</td>
      <td>176.380005</td>
      <td>54945800</td>
    </tr>
    <tr>
      <th>2023-08-25</th>
      <td>177.380005</td>
      <td>179.149994</td>
      <td>175.820007</td>
      <td>178.610001</td>
      <td>178.610001</td>
      <td>51418700</td>
    </tr>
  </tbody>
</table>
<p>919 rows × 6 columns</p>
</div>




```python
# 컬럼 값 비교 쿼리
df.query("Open > Close")
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
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2012-01-09</th>
      <td>15.196429</td>
      <td>15.276786</td>
      <td>15.048214</td>
      <td>15.061786</td>
      <td>12.784389</td>
      <td>394024400</td>
    </tr>
    <tr>
      <th>2012-01-10</th>
      <td>15.211071</td>
      <td>15.214286</td>
      <td>15.053571</td>
      <td>15.115714</td>
      <td>12.830169</td>
      <td>258196400</td>
    </tr>
    <tr>
      <th>2012-01-11</th>
      <td>15.095714</td>
      <td>15.101786</td>
      <td>14.975357</td>
      <td>15.091071</td>
      <td>12.809250</td>
      <td>215084800</td>
    </tr>
    <tr>
      <th>2012-01-12</th>
      <td>15.081429</td>
      <td>15.103571</td>
      <td>14.955357</td>
      <td>15.049643</td>
      <td>12.774082</td>
      <td>212587200</td>
    </tr>
    <tr>
      <th>2012-01-19</th>
      <td>15.362500</td>
      <td>15.406071</td>
      <td>15.232500</td>
      <td>15.276786</td>
      <td>12.966883</td>
      <td>261738400</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2023-08-10</th>
      <td>179.479996</td>
      <td>180.750000</td>
      <td>177.600006</td>
      <td>177.970001</td>
      <td>177.729996</td>
      <td>54686900</td>
    </tr>
    <tr>
      <th>2023-08-15</th>
      <td>178.880005</td>
      <td>179.479996</td>
      <td>177.050003</td>
      <td>177.449997</td>
      <td>177.449997</td>
      <td>43622600</td>
    </tr>
    <tr>
      <th>2023-08-16</th>
      <td>177.130005</td>
      <td>178.539993</td>
      <td>176.500000</td>
      <td>176.570007</td>
      <td>176.570007</td>
      <td>46964900</td>
    </tr>
    <tr>
      <th>2023-08-17</th>
      <td>177.139999</td>
      <td>177.509995</td>
      <td>173.479996</td>
      <td>174.000000</td>
      <td>174.000000</td>
      <td>66062900</td>
    </tr>
    <tr>
      <th>2023-08-24</th>
      <td>180.669998</td>
      <td>181.100006</td>
      <td>176.009995</td>
      <td>176.380005</td>
      <td>176.380005</td>
      <td>54945800</td>
    </tr>
  </tbody>
</table>
<p>1388 rows × 6 columns</p>
</div>




```python
# isin 값에 해당하는 인덱스 목록 반환
isin = df["Volume"].isin([394024400, 258196400])
df.query("Volume in [394024400, 258196400]") # 동일한 쿼리
print(f"isin :\n{isin}")
df[isin]
```

    isin :
    Date
    2012-01-03    False
    2012-01-04    False
    2012-01-05    False
    2012-01-06    False
    2012-01-09     True
                  ...  
    2023-08-21    False
    2023-08-22    False
    2023-08-23    False
    2023-08-24    False
    2023-08-25    False
    Name: Volume, Length: 2931, dtype: bool





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
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2012-01-09</th>
      <td>15.196429</td>
      <td>15.276786</td>
      <td>15.048214</td>
      <td>15.061786</td>
      <td>12.784389</td>
      <td>394024400</td>
    </tr>
    <tr>
      <th>2012-01-10</th>
      <td>15.211071</td>
      <td>15.214286</td>
      <td>15.053571</td>
      <td>15.115714</td>
      <td>12.830169</td>
      <td>258196400</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 일치하는 시리즈 반환
df.query("Volume == 1000")
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
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
# 변수 치환
value = 1000
df.query("Volume == @value")
df.query(f"Volume == {value}")
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
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>



### 2. 인덱스 컬럼 변환


```python
df.reset_index()
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
      <th>Date</th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2012-01-03</td>
      <td>14.621429</td>
      <td>14.732143</td>
      <td>14.607143</td>
      <td>14.686786</td>
      <td>12.466090</td>
      <td>302220800</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2012-01-04</td>
      <td>14.642857</td>
      <td>14.810000</td>
      <td>14.617143</td>
      <td>14.765714</td>
      <td>12.533089</td>
      <td>260022000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2012-01-05</td>
      <td>14.819643</td>
      <td>14.948214</td>
      <td>14.738214</td>
      <td>14.929643</td>
      <td>12.672229</td>
      <td>271269600</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2012-01-06</td>
      <td>14.991786</td>
      <td>15.098214</td>
      <td>14.972143</td>
      <td>15.085714</td>
      <td>12.804703</td>
      <td>318292800</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2012-01-09</td>
      <td>15.196429</td>
      <td>15.276786</td>
      <td>15.048214</td>
      <td>15.061786</td>
      <td>12.784389</td>
      <td>394024400</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2926</th>
      <td>2023-08-21</td>
      <td>175.070007</td>
      <td>176.130005</td>
      <td>173.740005</td>
      <td>175.839996</td>
      <td>175.839996</td>
      <td>46311900</td>
    </tr>
    <tr>
      <th>2927</th>
      <td>2023-08-22</td>
      <td>177.059998</td>
      <td>177.679993</td>
      <td>176.250000</td>
      <td>177.229996</td>
      <td>177.229996</td>
      <td>42084200</td>
    </tr>
    <tr>
      <th>2928</th>
      <td>2023-08-23</td>
      <td>178.520004</td>
      <td>181.550003</td>
      <td>178.330002</td>
      <td>181.119995</td>
      <td>181.119995</td>
      <td>52722800</td>
    </tr>
    <tr>
      <th>2929</th>
      <td>2023-08-24</td>
      <td>180.669998</td>
      <td>181.100006</td>
      <td>176.009995</td>
      <td>176.380005</td>
      <td>176.380005</td>
      <td>54945800</td>
    </tr>
    <tr>
      <th>2930</th>
      <td>2023-08-25</td>
      <td>177.380005</td>
      <td>179.149994</td>
      <td>175.820007</td>
      <td>178.610001</td>
      <td>178.610001</td>
      <td>51418700</td>
    </tr>
  </tbody>
</table>
<p>2931 rows × 7 columns</p>
</div>



### 3. Apply


```python
df_kospi = pd.read_csv('https://raw.githubusercontent.com/jin0choi1216/dataset/main/KOSPI_stocks.csv', index_col = 0)
df_kospi.head()
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
      <th>Code</th>
      <th>ISU_CD</th>
      <th>Name</th>
      <th>Market</th>
      <th>Dept</th>
      <th>Close</th>
      <th>ChangeCode</th>
      <th>Changes</th>
      <th>ChagesRatio</th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Volume</th>
      <th>Amount</th>
      <th>Marcap</th>
      <th>Stocks</th>
      <th>MarketId</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>005930</td>
      <td>KR7005930003</td>
      <td>삼성전자</td>
      <td>KOSPI</td>
      <td>NaN</td>
      <td>67100</td>
      <td>2</td>
      <td>-1100</td>
      <td>-1.61</td>
      <td>67100</td>
      <td>67400</td>
      <td>66900</td>
      <td>7032462</td>
      <td>471934306900</td>
      <td>400572409105000</td>
      <td>5969782550</td>
      <td>STK</td>
    </tr>
    <tr>
      <th>1</th>
      <td>373220</td>
      <td>KR7373220003</td>
      <td>LG에너지솔루션</td>
      <td>KOSPI</td>
      <td>NaN</td>
      <td>546000</td>
      <td>1</td>
      <td>11000</td>
      <td>2.06</td>
      <td>527000</td>
      <td>549000</td>
      <td>525000</td>
      <td>249493</td>
      <td>135513119000</td>
      <td>127764000000000</td>
      <td>234000000</td>
      <td>STK</td>
    </tr>
    <tr>
      <th>2</th>
      <td>000660</td>
      <td>KR7000660001</td>
      <td>SK하이닉스</td>
      <td>KOSPI</td>
      <td>NaN</td>
      <td>116500</td>
      <td>2</td>
      <td>-4400</td>
      <td>-3.64</td>
      <td>117400</td>
      <td>118300</td>
      <td>115300</td>
      <td>3533647</td>
      <td>412064064200</td>
      <td>84812275522500</td>
      <td>728002365</td>
      <td>STK</td>
    </tr>
    <tr>
      <th>3</th>
      <td>207940</td>
      <td>KR7207940008</td>
      <td>삼성바이오로직스</td>
      <td>KOSPI</td>
      <td>NaN</td>
      <td>757000</td>
      <td>2</td>
      <td>-6000</td>
      <td>-0.79</td>
      <td>755000</td>
      <td>764000</td>
      <td>754000</td>
      <td>23435</td>
      <td>17763884000</td>
      <td>53878718000000</td>
      <td>71174000</td>
      <td>STK</td>
    </tr>
    <tr>
      <th>4</th>
      <td>005490</td>
      <td>KR7005490008</td>
      <td>POSCO홀딩스</td>
      <td>KOSPI</td>
      <td>NaN</td>
      <td>577000</td>
      <td>2</td>
      <td>-2000</td>
      <td>-0.35</td>
      <td>567000</td>
      <td>583000</td>
      <td>561000</td>
      <td>904736</td>
      <td>519579225000</td>
      <td>48797599710000</td>
      <td>84571230</td>
      <td>STK</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 함수를 매개변수로 받아 호출한다
def checkChangesRatio(val: int) -> str:
    if val > 0:
        return "오른 주식"
    else:
        return "내린 주식"

df_kospi.ChagesRatio.apply(checkChangesRatio)
```




    0      내린 주식
    1      오른 주식
    2      내린 주식
    3      내린 주식
    4      내린 주식
           ...  
    946    오른 주식
    947    오른 주식
    948    내린 주식
    949    내린 주식
    950    내린 주식
    Name: ChagesRatio, Length: 951, dtype: object




```python
# 람다 표현식
df_kospi.ChagesRatio.apply(lambda val: "오른 주식" if val > 0 else "내린 주식")
```




    0      내린 주식
    1      오른 주식
    2      내린 주식
    3      내린 주식
    4      내린 주식
           ...  
    946    오른 주식
    947    오른 주식
    948    내린 주식
    949    내린 주식
    950    내린 주식
    Name: ChagesRatio, Length: 951, dtype: object



### 4. With Numpy


```python
import numpy as np
df_kospi["ADD"] = np.where(df_kospi.ChagesRatio > 0, "오른 주식", "내린 주식")
df_kospi
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
      <th>Code</th>
      <th>ISU_CD</th>
      <th>Name</th>
      <th>Market</th>
      <th>Dept</th>
      <th>Close</th>
      <th>ChangeCode</th>
      <th>Changes</th>
      <th>ChagesRatio</th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Volume</th>
      <th>Amount</th>
      <th>Marcap</th>
      <th>Stocks</th>
      <th>MarketId</th>
      <th>TT</th>
      <th>ADD</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>005930</td>
      <td>KR7005930003</td>
      <td>삼성전자</td>
      <td>KOSPI</td>
      <td>NaN</td>
      <td>67100</td>
      <td>2</td>
      <td>-1100</td>
      <td>-1.61</td>
      <td>67100</td>
      <td>67400</td>
      <td>66900</td>
      <td>7032462</td>
      <td>471934306900</td>
      <td>400572409105000</td>
      <td>5969782550</td>
      <td>STK</td>
      <td>내린 주식</td>
      <td>내린 주식</td>
    </tr>
    <tr>
      <th>1</th>
      <td>373220</td>
      <td>KR7373220003</td>
      <td>LG에너지솔루션</td>
      <td>KOSPI</td>
      <td>NaN</td>
      <td>546000</td>
      <td>1</td>
      <td>11000</td>
      <td>2.06</td>
      <td>527000</td>
      <td>549000</td>
      <td>525000</td>
      <td>249493</td>
      <td>135513119000</td>
      <td>127764000000000</td>
      <td>234000000</td>
      <td>STK</td>
      <td>오른 주식</td>
      <td>오른 주식</td>
    </tr>
    <tr>
      <th>2</th>
      <td>000660</td>
      <td>KR7000660001</td>
      <td>SK하이닉스</td>
      <td>KOSPI</td>
      <td>NaN</td>
      <td>116500</td>
      <td>2</td>
      <td>-4400</td>
      <td>-3.64</td>
      <td>117400</td>
      <td>118300</td>
      <td>115300</td>
      <td>3533647</td>
      <td>412064064200</td>
      <td>84812275522500</td>
      <td>728002365</td>
      <td>STK</td>
      <td>내린 주식</td>
      <td>내린 주식</td>
    </tr>
    <tr>
      <th>3</th>
      <td>207940</td>
      <td>KR7207940008</td>
      <td>삼성바이오로직스</td>
      <td>KOSPI</td>
      <td>NaN</td>
      <td>757000</td>
      <td>2</td>
      <td>-6000</td>
      <td>-0.79</td>
      <td>755000</td>
      <td>764000</td>
      <td>754000</td>
      <td>23435</td>
      <td>17763884000</td>
      <td>53878718000000</td>
      <td>71174000</td>
      <td>STK</td>
      <td>내린 주식</td>
      <td>내린 주식</td>
    </tr>
    <tr>
      <th>4</th>
      <td>005490</td>
      <td>KR7005490008</td>
      <td>POSCO홀딩스</td>
      <td>KOSPI</td>
      <td>NaN</td>
      <td>577000</td>
      <td>2</td>
      <td>-2000</td>
      <td>-0.35</td>
      <td>567000</td>
      <td>583000</td>
      <td>561000</td>
      <td>904736</td>
      <td>519579225000</td>
      <td>48797599710000</td>
      <td>84571230</td>
      <td>STK</td>
      <td>내린 주식</td>
      <td>내린 주식</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>946</th>
      <td>014915</td>
      <td>KR7014911002</td>
      <td>성문전자우</td>
      <td>KOSPI</td>
      <td>NaN</td>
      <td>5830</td>
      <td>1</td>
      <td>50</td>
      <td>0.87</td>
      <td>5780</td>
      <td>5830</td>
      <td>5780</td>
      <td>123</td>
      <td>711790</td>
      <td>3498000000</td>
      <td>600000</td>
      <td>STK</td>
      <td>오른 주식</td>
      <td>오른 주식</td>
    </tr>
    <tr>
      <th>947</th>
      <td>002787</td>
      <td>KR7002782001</td>
      <td>진흥기업2우B</td>
      <td>KOSPI</td>
      <td>NaN</td>
      <td>11170</td>
      <td>1</td>
      <td>150</td>
      <td>1.36</td>
      <td>11020</td>
      <td>11170</td>
      <td>10910</td>
      <td>148</td>
      <td>1623110</td>
      <td>3293005360</td>
      <td>294808</td>
      <td>STK</td>
      <td>오른 주식</td>
      <td>오른 주식</td>
    </tr>
    <tr>
      <th>948</th>
      <td>000227</td>
      <td>KR7000222000</td>
      <td>유유제약2우B</td>
      <td>KOSPI</td>
      <td>NaN</td>
      <td>10080</td>
      <td>2</td>
      <td>-240</td>
      <td>-2.33</td>
      <td>10090</td>
      <td>10090</td>
      <td>10080</td>
      <td>75</td>
      <td>756060</td>
      <td>3281644800</td>
      <td>325560</td>
      <td>STK</td>
      <td>내린 주식</td>
      <td>내린 주식</td>
    </tr>
    <tr>
      <th>949</th>
      <td>001525</td>
      <td>KR7001521004</td>
      <td>동양우</td>
      <td>KOSPI</td>
      <td>NaN</td>
      <td>5210</td>
      <td>2</td>
      <td>-10</td>
      <td>-0.19</td>
      <td>5220</td>
      <td>5220</td>
      <td>5210</td>
      <td>37</td>
      <td>192810</td>
      <td>3218378510</td>
      <td>617731</td>
      <td>STK</td>
      <td>내린 주식</td>
      <td>내린 주식</td>
    </tr>
    <tr>
      <th>950</th>
      <td>001527</td>
      <td>KR7001522002</td>
      <td>동양2우B</td>
      <td>KOSPI</td>
      <td>NaN</td>
      <td>10150</td>
      <td>2</td>
      <td>-10</td>
      <td>-0.10</td>
      <td>10040</td>
      <td>10220</td>
      <td>10040</td>
      <td>53</td>
      <td>534860</td>
      <td>3131975350</td>
      <td>308569</td>
      <td>STK</td>
      <td>내린 주식</td>
      <td>내린 주식</td>
    </tr>
  </tbody>
</table>
<p>951 rows × 19 columns</p>
</div>



### 5. 값 집계


```python
df_value_count = df_kospi.ADD.value_counts()
print(type(df_value_count))
df_value_count
```

    <class 'pandas.core.series.Series'>





    ADD
    내린 주식    583
    오른 주식    368
    Name: count, dtype: int64



### 6. 순위


```python
df_kospi.Marcap.rank(ascending = False)
```




    0        1.0
    1        2.0
    2        3.0
    3        4.0
    4        5.0
           ...  
    946    947.0
    947    948.0
    948    949.0
    949    950.0
    950    951.0
    Name: Marcap, Length: 951, dtype: float64



### 7. Group by


```python
df_krx = pd.read_csv("https://raw.githubusercontent.com/jin0choi1216/dataset/main/KRX_stocks.csv", index_col=0)
print(df_krx.head())
df_krx[["Market", "ChagesRatio"]].groupby("Market").mean()
```

         Code        ISU_CD      Name Market Dept   Close  ChangeCode  Changes  \
    0  005930  KR7005930003      삼성전자  KOSPI  NaN   67100           2    -1100   
    1  373220  KR7373220003  LG에너지솔루션  KOSPI  NaN  546000           1    11000   
    2  000660  KR7000660001    SK하이닉스  KOSPI  NaN  116500           2    -4400   
    3  207940  KR7207940008  삼성바이오로직스  KOSPI  NaN  757000           2    -6000   
    4  005490  KR7005490008  POSCO홀딩스  KOSPI  NaN  577000           2    -2000   
    
       ChagesRatio    Open    High     Low   Volume        Amount  \
    0        -1.61   67100   67400   66900  7032462  471934306900   
    1         2.06  527000  549000  525000   249493  135513119000   
    2        -3.64  117400  118300  115300  3533647  412064064200   
    3        -0.79  755000  764000  754000    23435   17763884000   
    4        -0.35  567000  583000  561000   904736  519579225000   
    
                Marcap      Stocks MarketId  
    0  400572409105000  5969782550      STK  
    1  127764000000000   234000000      STK  
    2   84812275522500   728002365      STK  
    3   53878718000000    71174000      STK  
    4   48797599710000    84571230      STK  





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
      <th>ChagesRatio</th>
    </tr>
    <tr>
      <th>Market</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>KONEX</th>
      <td>-0.168281</td>
    </tr>
    <tr>
      <th>KOSDAQ</th>
      <td>-0.391093</td>
    </tr>
    <tr>
      <th>KOSDAQ GLOBAL</th>
      <td>-0.813600</td>
    </tr>
    <tr>
      <th>KOSPI</th>
      <td>0.107560</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_krx[["Market", "ChagesRatio", "Open"]].groupby("Market").agg({"ChagesRatio": "mean", "Open": "sum"})
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
      <th>ChagesRatio</th>
      <th>Open</th>
    </tr>
    <tr>
      <th>Market</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>KONEX</th>
      <td>-0.168281</td>
      <td>624219</td>
    </tr>
    <tr>
      <th>KOSDAQ</th>
      <td>-0.391093</td>
      <td>17308486</td>
    </tr>
    <tr>
      <th>KOSDAQ GLOBAL</th>
      <td>-0.813600</td>
      <td>2906500</td>
    </tr>
    <tr>
      <th>KOSPI</th>
      <td>0.107560</td>
      <td>34526986</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_krx[["Market", "ChagesRatio", "Open"]].groupby("Market").agg({"ChagesRatio": ["max", "sum"], "Open": ["min", "mean"]})
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="2" halign="left">ChagesRatio</th>
      <th colspan="2" halign="left">Open</th>
    </tr>
    <tr>
      <th></th>
      <th>max</th>
      <th>sum</th>
      <th>min</th>
      <th>mean</th>
    </tr>
    <tr>
      <th>Market</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>KONEX</th>
      <td>14.89</td>
      <td>-21.54</td>
      <td>0</td>
      <td>4876.710938</td>
    </tr>
    <tr>
      <th>KOSDAQ</th>
      <td>29.99</td>
      <td>-633.18</td>
      <td>0</td>
      <td>10690.849907</td>
    </tr>
    <tr>
      <th>KOSDAQ GLOBAL</th>
      <td>13.70</td>
      <td>-40.68</td>
      <td>7170</td>
      <td>58130.000000</td>
    </tr>
    <tr>
      <th>KOSPI</th>
      <td>30.00</td>
      <td>102.29</td>
      <td>0</td>
      <td>36305.978970</td>
    </tr>
  </tbody>
</table>
</div>



### 8. Merge


```python
market_price_change = pd.read_csv('https://raw.githubusercontent.com/jin0choi1216/dataset/main/market_price_change_2022.csv')
print(market_price_change.head(2))
print(market_price_change.shape)
purchases_of_equities = pd.read_csv('https://raw.githubusercontent.com/jin0choi1216/dataset/main/purchases_of_equities_2022.csv')
print(purchases_of_equities.head(2))
print(purchases_of_equities.shape)

# 컬럼 이름이 같을 경우

# inner
merged_inner = pd.merge(left = market_price_change, right = purchases_of_equities, how = "inner", on = ["티커", "종목명"])
print(f"inner shape : {merged_inner.shape}")

# left
merged_left = pd.merge(left = market_price_change, right = purchases_of_equities, how = "left", on = ["티커", "종목명"])
print(f"left shape : {merged_left.shape}")

# right
merged_right = pd.merge(left = market_price_change, right = purchases_of_equities, how = "right", on = ["티커", "종목명"])
print(f"right shape : {merged_right.shape}")

# outer
merged_outer = pd.merge(left = market_price_change, right = purchases_of_equities, how = "outer", on = ["티커", "종목명"])
print(f"outer shape : {merged_outer.shape}")
```

           티커     종목명     시가     종가   변동폭    등락률      거래량         거래대금
    0  095570  AJ네트웍스   6110   5720  -390  -6.38  2947645  17162545200
    1  006840   AK홀딩스  15150  17200  2050  13.53   455492   7706148650
    (942, 8)
           티커     종목명    매도거래량    매수거래량  순매수거래량       매도거래대금       매수거래대금  순매수거래대금
    0  060310      3S  3318765  3318765       0   7721430565   7721430565        0
    1  095570  AJ네트웍스  2947645  2947645       0  17162545200  17162545200        0
    (2625, 8)
    inner shape : (916, 14)
    left shape : (942, 14)
    right shape : (2625, 14)
    outer shape : (2651, 14)



```python
# 컬럼 이름이 다를 경우
pur2 = purchases_of_equities.rename(columns = { "티커": "티커2", "종목명": "종목명2" })

diff_column = pd.merge(
    left = market_price_change,
    right = pur2,
    how = "inner",
    left_on = ["티커", "종목명"],
    right_on = ["티커2", "종목명2"],
    suffixes = ("_L", "_R")
)
diff_column
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
      <th>티커</th>
      <th>종목명</th>
      <th>시가</th>
      <th>종가</th>
      <th>변동폭</th>
      <th>등락률</th>
      <th>거래량</th>
      <th>거래대금</th>
      <th>티커2</th>
      <th>종목명2</th>
      <th>매도거래량</th>
      <th>매수거래량</th>
      <th>순매수거래량</th>
      <th>매도거래대금</th>
      <th>매수거래대금</th>
      <th>순매수거래대금</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>095570</td>
      <td>AJ네트웍스</td>
      <td>6110</td>
      <td>5720</td>
      <td>-390</td>
      <td>-6.38</td>
      <td>2947645</td>
      <td>17162545200</td>
      <td>095570</td>
      <td>AJ네트웍스</td>
      <td>2947645</td>
      <td>2947645</td>
      <td>0</td>
      <td>17162545200</td>
      <td>17162545200</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>006840</td>
      <td>AK홀딩스</td>
      <td>15150</td>
      <td>17200</td>
      <td>2050</td>
      <td>13.53</td>
      <td>455492</td>
      <td>7706148650</td>
      <td>006840</td>
      <td>AK홀딩스</td>
      <td>455492</td>
      <td>455492</td>
      <td>0</td>
      <td>7706148650</td>
      <td>7706148650</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>027410</td>
      <td>BGF</td>
      <td>4365</td>
      <td>4305</td>
      <td>-60</td>
      <td>-1.37</td>
      <td>14388855</td>
      <td>62685829240</td>
      <td>027410</td>
      <td>BGF</td>
      <td>14388855</td>
      <td>14388855</td>
      <td>0</td>
      <td>62685829240</td>
      <td>62685829240</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>282330</td>
      <td>BGF리테일</td>
      <td>205500</td>
      <td>210500</td>
      <td>5000</td>
      <td>2.43</td>
      <td>712994</td>
      <td>146603104000</td>
      <td>282330</td>
      <td>BGF리테일</td>
      <td>712994</td>
      <td>712994</td>
      <td>0</td>
      <td>146603104000</td>
      <td>146603104000</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>138930</td>
      <td>BNK금융지주</td>
      <td>7390</td>
      <td>6500</td>
      <td>-890</td>
      <td>-12.04</td>
      <td>37130723</td>
      <td>264104001940</td>
      <td>138930</td>
      <td>BNK금융지주</td>
      <td>37130723</td>
      <td>37130723</td>
      <td>0</td>
      <td>264104001940</td>
      <td>264104001940</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>911</th>
      <td>005010</td>
      <td>휴스틸</td>
      <td>5420</td>
      <td>5070</td>
      <td>-350</td>
      <td>-6.46</td>
      <td>9608972</td>
      <td>49226534830</td>
      <td>005010</td>
      <td>휴스틸</td>
      <td>9608972</td>
      <td>9608972</td>
      <td>0</td>
      <td>49226534830</td>
      <td>49226534830</td>
      <td>0</td>
    </tr>
    <tr>
      <th>912</th>
      <td>000540</td>
      <td>흥국화재</td>
      <td>3165</td>
      <td>3370</td>
      <td>205</td>
      <td>6.48</td>
      <td>15972406</td>
      <td>59888402133</td>
      <td>000540</td>
      <td>흥국화재</td>
      <td>15972406</td>
      <td>15972406</td>
      <td>0</td>
      <td>59888402133</td>
      <td>59888402133</td>
      <td>0</td>
    </tr>
    <tr>
      <th>913</th>
      <td>000547</td>
      <td>흥국화재2우B</td>
      <td>19300</td>
      <td>16200</td>
      <td>-3100</td>
      <td>-16.06</td>
      <td>18918</td>
      <td>364549550</td>
      <td>000547</td>
      <td>흥국화재2우B</td>
      <td>18918</td>
      <td>18918</td>
      <td>0</td>
      <td>364549550</td>
      <td>364549550</td>
      <td>0</td>
    </tr>
    <tr>
      <th>914</th>
      <td>000545</td>
      <td>흥국화재우</td>
      <td>6020</td>
      <td>6150</td>
      <td>130</td>
      <td>2.16</td>
      <td>68957</td>
      <td>432345040</td>
      <td>000545</td>
      <td>흥국화재우</td>
      <td>68957</td>
      <td>68957</td>
      <td>0</td>
      <td>432345040</td>
      <td>432345040</td>
      <td>0</td>
    </tr>
    <tr>
      <th>915</th>
      <td>003280</td>
      <td>흥아해운</td>
      <td>1625</td>
      <td>1355</td>
      <td>-270</td>
      <td>-16.62</td>
      <td>4552374</td>
      <td>6915159460</td>
      <td>003280</td>
      <td>흥아해운</td>
      <td>4552374</td>
      <td>4552374</td>
      <td>0</td>
      <td>6915159460</td>
      <td>6915159460</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>916 rows × 16 columns</p>
</div>



### 9. Pivot Table


```python
# 2012 ~ 2023
GOOGL = pd.read_csv('https://raw.githubusercontent.com/jin0choi1216/dataset/main/GOOGL.csv')
AAPL = pd.read_csv('https://raw.githubusercontent.com/jin0choi1216/dataset/main/AAPL.csv')

GOOGL["Symbol"] = "Google"
AAPL["Symbol"] = "Apple"

df = pd.concat([GOOGL, AAPL])
```


```python
# 날짜를 기준으로 구글과 애플별로 피벗
pivot = pd.pivot_table(data = df, index = "Date", columns = "Symbol", values = "Close")
print(pivot)

# 인덱스 여러개 지정
pivots = pd.pivot_table(data = df, index = ["Date", "Symbol"], values = "Close", aggfunc = "mean")
print(pivots)
```

    Symbol           Apple      Google
    Date                              
    2012-01-03   14.686786   16.651901
    2012-01-04   14.765714   16.723724
    2012-01-05   14.929643   16.491741
    2012-01-06   15.085714   16.266768
    2012-01-09   15.061786   15.577077
    ...                ...         ...
    2023-08-21  175.839996  128.369995
    2023-08-22  177.229996  129.080002
    2023-08-23  181.119995  132.369995
    2023-08-24  176.380005  129.779999
    2023-08-25  178.610001  129.880005
    
    [2931 rows x 2 columns]
                            Close
    Date       Symbol            
    2012-01-03 Apple    14.686786
               Google   16.651901
    2012-01-04 Apple    14.765714
               Google   16.723724
    2012-01-05 Apple    14.929643
    ...                       ...
    2023-08-23 Google  132.369995
    2023-08-24 Apple   176.380005
               Google  129.779999
    2023-08-25 Apple   178.610001
               Google  129.880005
    
    [5862 rows x 1 columns]


### 9. 이전 값 비교


```python
# 이전 값 과의 차이
GOOGL.Low.diff()

# 이전 값 과의 차이 퍼센트 수치
GOOGL.Low.pct_change()
```




    0            NaN
    1       0.012646
    2      -0.006645
    3      -0.009814
    4      -0.043953
              ...   
    2926    0.001424
    2927    0.013907
    2928    0.012079
    2929   -0.002310
    2930   -0.017905
    Name: Low, Length: 2931, dtype: float64



### 10. 결측치 수치 확인


```python
is_null = merged_outer.isnull()
print(is_null.head(5))
print(is_null.sum())
```

          티커    종목명     시가     종가    변동폭    등락률    거래량   거래대금  매도거래량  매수거래량  \
    0  False  False  False  False  False  False  False  False  False  False   
    1  False  False  False  False  False  False  False  False  False  False   
    2  False  False  False  False  False  False  False  False  False  False   
    3  False  False  False  False  False  False  False  False  False  False   
    4  False  False  False  False  False  False  False  False  False  False   
    
       순매수거래량  매도거래대금  매수거래대금  순매수거래대금  
    0   False   False   False    False  
    1   False   False   False    False  
    2   False   False   False    False  
    3   False   False   False    False  
    4   False   False   False    False  
    티커            0
    종목명           0
    시가         1709
    종가         1709
    변동폭        1709
    등락률        1709
    거래량        1709
    거래대금       1709
    매도거래량        26
    매수거래량        26
    순매수거래량       26
    매도거래대금       26
    매수거래대금       26
    순매수거래대금      26
    dtype: int64


### 11. 데이터 밀기


```python
GOOGL["Low_2"] = GOOGL.Low.shift(1, fill_value = 9999) 
GOOGL
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
      <th>Date</th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
      <th>Symbol</th>
      <th>Low_2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2012-01-03</td>
      <td>16.339840</td>
      <td>16.720470</td>
      <td>16.325577</td>
      <td>16.651901</td>
      <td>16.651901</td>
      <td>146912940</td>
      <td>Google</td>
      <td>9999.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2012-01-04</td>
      <td>16.642391</td>
      <td>16.773024</td>
      <td>16.532032</td>
      <td>16.723724</td>
      <td>16.723724</td>
      <td>114445440</td>
      <td>Google</td>
      <td>16.325577</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2012-01-05</td>
      <td>16.569820</td>
      <td>16.615866</td>
      <td>16.422173</td>
      <td>16.491741</td>
      <td>16.491741</td>
      <td>131184684</td>
      <td>Google</td>
      <td>16.532032</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2012-01-06</td>
      <td>16.495245</td>
      <td>16.516518</td>
      <td>16.261011</td>
      <td>16.266768</td>
      <td>16.266768</td>
      <td>107608284</td>
      <td>Google</td>
      <td>16.422173</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2012-01-09</td>
      <td>16.178679</td>
      <td>16.191191</td>
      <td>15.546296</td>
      <td>15.577077</td>
      <td>15.577077</td>
      <td>232671096</td>
      <td>Google</td>
      <td>16.261011</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2926</th>
      <td>2023-08-21</td>
      <td>127.180000</td>
      <td>128.729996</td>
      <td>126.559998</td>
      <td>128.369995</td>
      <td>128.369995</td>
      <td>25248700</td>
      <td>Google</td>
      <td>126.379997</td>
    </tr>
    <tr>
      <th>2927</th>
      <td>2023-08-22</td>
      <td>128.509995</td>
      <td>130.279999</td>
      <td>128.320007</td>
      <td>129.080002</td>
      <td>129.080002</td>
      <td>22067500</td>
      <td>Google</td>
      <td>126.559998</td>
    </tr>
    <tr>
      <th>2928</th>
      <td>2023-08-23</td>
      <td>130.179993</td>
      <td>133.410004</td>
      <td>129.869995</td>
      <td>132.369995</td>
      <td>132.369995</td>
      <td>27819700</td>
      <td>Google</td>
      <td>128.320007</td>
    </tr>
    <tr>
      <th>2929</th>
      <td>2023-08-24</td>
      <td>133.949997</td>
      <td>134.250000</td>
      <td>129.570007</td>
      <td>129.779999</td>
      <td>129.779999</td>
      <td>28500700</td>
      <td>Google</td>
      <td>129.869995</td>
    </tr>
    <tr>
      <th>2930</th>
      <td>2023-08-25</td>
      <td>129.539993</td>
      <td>130.759995</td>
      <td>127.250000</td>
      <td>129.880005</td>
      <td>129.880005</td>
      <td>26744800</td>
      <td>Google</td>
      <td>129.570007</td>
    </tr>
  </tbody>
</table>
<p>2931 rows × 9 columns</p>
</div>



### 12. 이동 평균, 누적 평균


```python
expanding = GOOGL.Low.expanding() # 누적 평균 
print(expanding.mean())
rolling = GOOGL.Low.rolling(window = 5) # 이동평균
print(rolling.mean())
```

    0       16.325577
    1       16.428804
    2       16.426594
    3       16.385198
    4       16.217418
              ...    
    2926    57.929351
    2927    57.953392
    2928    57.977945
    2929    58.002379
    2930    58.026005
    Name: Low, Length: 2931, dtype: float64
    0              NaN
    1              NaN
    2              NaN
    3              NaN
    4        16.217418
               ...    
    2926    127.875998
    2927    127.684000
    2928    128.083998
    2929    128.140001
    2930    128.314001
    Name: Low, Length: 2931, dtype: float64

