---
title:  "2.Pandas Efficiency"
excerpt: "Pandas 의 올바른 코드짜기를 알아봅시다."
categories:
  - Py_Preprocessing
tags:
  - 전처리
last_modified_at: 2021-01-15

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
---


## Intro

- Sofia Heisler의 A Beginner’s Guide to Optimizing Pandas Code for Speed 을 참조하였다.
- 초창기에 판다스는 느리다는 평가를 받았다고 한다.
- 물론 최적화가 되어있는 c 코드를 이길수는 없을것이지만, 어느정도 '잘' 짜여진 판다스 코드는 충분히 빠르다.
- 하지만 느린 코드를 짜고 파이썬도 느리구나.... 라는 불평을 하는 사람은 마땅히 벌을 받아야 할 것이다. 
    - 내가 주로 다루는 데이터가 1기가가 넘는 데이터가 거의 없었으니, 그냥 for 문으로 돌려놓고 유튜브 한번 보고 오면 다 돌아가는 수준이였다. 
    - 그래서 최적화에 관심을 가지지 않았는데, 최근들어 EDA 와 동시에 작업해야되는 일이 많아지면서 (시각화, 분석 등...) 점점 느려터진 속도에 화가 나던 중, 문득 최적화에 대해서는 찾아본적이 없다는것을 깨닫고 찾아본 결과 내 코드는 쓰레기 그 자체였다.
    - 앞으로는 올바른 판다스 문법으로 안좋은 코드를 모두 고칠 계획이다.(컴퓨터야 미안해!)


```python
import pandas as pd
import numpy as np
```


```python
from seaborn import load_dataset
diamonds=load_dataset('diamonds')
df = diamonds.copy()
df.head()
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
      <th>carat</th>
      <th>cut</th>
      <th>color</th>
      <th>clarity</th>
      <th>depth</th>
      <th>table</th>
      <th>price</th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.23</td>
      <td>Ideal</td>
      <td>E</td>
      <td>SI2</td>
      <td>61.5</td>
      <td>55.0</td>
      <td>326</td>
      <td>3.95</td>
      <td>3.98</td>
      <td>2.43</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.21</td>
      <td>Premium</td>
      <td>E</td>
      <td>SI1</td>
      <td>59.8</td>
      <td>61.0</td>
      <td>326</td>
      <td>3.89</td>
      <td>3.84</td>
      <td>2.31</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.23</td>
      <td>Good</td>
      <td>E</td>
      <td>VS1</td>
      <td>56.9</td>
      <td>65.0</td>
      <td>327</td>
      <td>4.05</td>
      <td>4.07</td>
      <td>2.31</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.29</td>
      <td>Premium</td>
      <td>I</td>
      <td>VS2</td>
      <td>62.4</td>
      <td>58.0</td>
      <td>334</td>
      <td>4.20</td>
      <td>4.23</td>
      <td>2.63</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.31</td>
      <td>Good</td>
      <td>J</td>
      <td>SI2</td>
      <td>63.3</td>
      <td>58.0</td>
      <td>335</td>
      <td>4.34</td>
      <td>4.35</td>
      <td>2.75</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.describe()
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
      <th>carat</th>
      <th>depth</th>
      <th>table</th>
      <th>price</th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>53940.000000</td>
      <td>53940.000000</td>
      <td>53940.000000</td>
      <td>53940.000000</td>
      <td>53940.000000</td>
      <td>53940.000000</td>
      <td>53940.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>0.797940</td>
      <td>61.749405</td>
      <td>57.457184</td>
      <td>3932.799722</td>
      <td>5.731157</td>
      <td>5.734526</td>
      <td>3.538734</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.474011</td>
      <td>1.432621</td>
      <td>2.234491</td>
      <td>3989.439738</td>
      <td>1.121761</td>
      <td>1.142135</td>
      <td>0.705699</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.200000</td>
      <td>43.000000</td>
      <td>43.000000</td>
      <td>326.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>0.400000</td>
      <td>61.000000</td>
      <td>56.000000</td>
      <td>950.000000</td>
      <td>4.710000</td>
      <td>4.720000</td>
      <td>2.910000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>0.700000</td>
      <td>61.800000</td>
      <td>57.000000</td>
      <td>2401.000000</td>
      <td>5.700000</td>
      <td>5.710000</td>
      <td>3.530000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>1.040000</td>
      <td>62.500000</td>
      <td>59.000000</td>
      <td>5324.250000</td>
      <td>6.540000</td>
      <td>6.540000</td>
      <td>4.040000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>5.010000</td>
      <td>79.000000</td>
      <td>95.000000</td>
      <td>18823.000000</td>
      <td>10.740000</td>
      <td>58.900000</td>
      <td>31.800000</td>
    </tr>
  </tbody>
</table>
</div>



## for 문

- 내가 했던 실수들의 예시이다! 
- 데이터 프레임 행을 하나씩 반복하여서, 적용하려 한다.
- 이 방법의 경우 매우 직관적이다. 우리가 문법을 배울때도, for , while 등의 구문을 먼저 배우며 또한 이런 구조를 index(데이터) 각각에 적용하는것도 매우 직관적.
- 하지만 최적화 면에서 매우 구리다.


```python
# 캐럿수가 크고, 가격도 크면 좋은 다이아몬드라고 1을 주고 싶다.
def cal(df):
    for i in range(0,len(df)):
        if (df.loc[i,'carat'] > 0.4) & (df.loc[i,'price'] > 300) :
            df.loc[i,'good'] = 1
```


```python
%%timeit -n 1 -r 1 # 1번 roop, 1개의 best : 즉 그냥 한번 돌린 시간을 재겠다는 것이다.
cal(df)
# 실행하는데에 시간이 좀 걸리는 모습을 볼 수 있다.
# 이정도 속도면, data columns 이 100만개정도 되면 거의 2~3분 걸리는거다!
```

    13.5 s ± 0 ns per loop (mean ± std. dev. of 1 run, 1 loop each)
    


```python
sum(df['good'])
```




    39549



## Iterrows 방법

- iterrows 메서드는 데이터 프레임의 행을 반복하며 행행 자체를 포함하는 객체+index 를 반환해준다.
- for 문과 뭐가 다르는지 궁금하겠지만, iterrows 는 pandas 와 잘 작동하도록 최적화가 되어있다. 
- 같은 문제를 평균적으로 for 문 보다 4배이상 빠르게 해결한다고 한다.


```python
df = diamonds.copy()
```


```python
df.iloc[[1]]
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
      <th>carat</th>
      <th>cut</th>
      <th>color</th>
      <th>clarity</th>
      <th>depth</th>
      <th>table</th>
      <th>price</th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>0.21</td>
      <td>Premium</td>
      <td>E</td>
      <td>SI1</td>
      <td>59.8</td>
      <td>61.0</td>
      <td>326</td>
      <td>3.89</td>
      <td>3.84</td>
      <td>2.31</td>
    </tr>
  </tbody>
</table>
</div>



- 먼저 idx 함수를 정의해서 index 와 row를 어떻게 뽑아내는지 알아보자.


```python
def idx(df):
    for index,row in df.iloc[[0]].iterrows() : # itterrows 를 적용한 뒤에 index 와 row 를 적용
        return index,row
```


```python
index,row=idx(df)
```

- 아래와 같이 index 는 수, row 는 pandas series 의 형태로 나오게 된다.


```python
print(type(row))
print(index)
```

    <class 'pandas.core.series.Series'>
    0
    


```python
for index,row in df.head().iterrows():
    print(index)
    print(row)
```

    0
    carat       0.23
    cut        Ideal
    color          E
    clarity      SI2
    depth       61.5
    table         55
    price        326
    x           3.95
    y           3.98
    z           2.43
    Name: 0, dtype: object
    1
    carat         0.21
    cut        Premium
    color            E
    clarity        SI1
    depth         59.8
    table           61
    price          326
    x             3.89
    y             3.84
    z             2.31
    Name: 1, dtype: object
    2
    carat      0.23
    cut        Good
    color         E
    clarity     VS1
    depth      56.9
    table        65
    price       327
    x          4.05
    y          4.07
    z          2.31
    Name: 2, dtype: object
    3
    carat         0.29
    cut        Premium
    color            I
    clarity        VS2
    depth         62.4
    table           58
    price          334
    x              4.2
    y             4.23
    z             2.63
    Name: 3, dtype: object
    4
    carat      0.31
    cut        Good
    color         J
    clarity     SI2
    depth      63.3
    table        58
    price       335
    x          4.34
    y          4.35
    z          2.75
    Name: 4, dtype: object
    

- 이제 위의 iterrows 를 가지고 for 문으로 하려 했던, 0.4 캐럿, 300 이상의 금액일 때에 새로운 good 열에 1 을 할당하는 함수를 돌려보자.


```python
%%timeit -n 1 -r 1
good_list = []
for index,row in df.iterrows():
    if (row['carat'] > 0.4)&(row['price']>300):
        good_list.append(1) # list 에 저장해야된다.
    else :
        good_list.append(0)
df['good'] = good_list
```

    3.56 s ± 0 ns per loop (mean ± std. dev. of 1 run, 1 loop each)
    


```python
sum(df['good']) # 맞게변환된것을 볼 수 있다.
```




    39549



## 벡터화

- 판다스의 기본 단위인 데이터 프레임과 시리즈는 모두 배열 기반이다.
- 벡터화 한 다음 계산하게 되면 엄청나게 빠르다.


```python
%%timeit -n 100 -r 3
df.loc[(df['carat'] > 0.4)&(df['price']>300),'good'] = 1
```

    1.21 ms ± 83.4 µs per loop (mean ± std. dev. of 3 runs, 100 loops each)
    


```python
sum(df['good']) 
```




    39549



## 넘파이로 바꿔서 연산

- 넘파이는 '과학 계산을 위한 파이썬 기본 패키지' 를 표방한다.
- 즉 내부가 최적화된 사전 컴파일 된 C 코드로 작업을 수행하게 된다.
- 판다스와 마찬가지로 넘파이는 배열객체에서 작동하지만 INDEX, 데이터 유형 확인 등 판다스 시리즈 작업시 필요한 불필요한 작업을 피할 수 있어 매우매우 빠르다.

- 만약 index를 사용해야 하는 연산이면 벡터화만으로 충분하지만, index 를 쓸 필요가 없고 매우 빠른 연산을 하고 싶다면 value 메서드를 이용해서 배열화 하는것이 빠르게 할 수 있을것이다.


```python
%%timeit -n 100 -r 3
df['good'] = ((df['carat'].values > 0.4)&(df['price'].values>300))*1
```

    277 µs ± 33.6 µs per loop (mean ± std. dev. of 3 runs, 100 loops each)
    
