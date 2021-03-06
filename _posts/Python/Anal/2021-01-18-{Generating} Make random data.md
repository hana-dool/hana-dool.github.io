﻿---
title:  "0.various data sets"
excerpt: "파이썬의 내장 및 랜덤 데이터에 대해 알아봅시다."
categories:
  - Py_Analysis
tags:
  - 데이터 생성
last_modified_at: 2021-01-18

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
---


```python
# import pandas as pd
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib as mpl
import matplotlib.pyplot as plt
```

# Intro

- 굳이 Random data/내장 data set 을 여기 소개하는 이유는, Analysis 를 실습할 때에 데이터를 외부에서 직접 가져오는것 보다는 내장 데이터셋을 쓰는게 추후 재현성에 훨씬 좋고 또한 편리하기 때문이다.
- 그러므로 데이터 분석시에 random data 혹은 내장 데이터를 사용해서 분석을 진행하는것을 추천한다.

# Make classification data

`make_classification`함수는 설정에 따른 분류용 가상 데이터를 생성하는 명령이다. 이 함수의 인수와 반환값은 다음과 같다.

* 인수:	
 * `n_samples` : 표본 데이터의 수, 디폴트 100
 * `n_features` : 독립 변수의 수, 디폴트 20
 * `n_informative` : 독립 변수 중 종속 변수와 상관 관계가 있는 성분의 수, 디폴트 2
 * `n_redundant` : 독립 변수 중 다른 독립 변수의 선형 조합으로 나타나는 성분의 수, 디폴트 2
 * `n_repeated` : 독립 변수 중 단순 중복된 성분의 수, 디폴트 0
 * `n_classes` : 종속 변수의 클래스 수, 디폴트 2
 * `n_clusters_per_class` : 클래스 당 클러스터의 수, 디폴트 2
 * `weights` : 각 클래스에 할당된 표본 수
 * `random_state` : 난수 발생 시드    
  
* 반환값:	
 * `X` : [n_samples, n_features] 크기의 배열 
    * 독립 변수
 * `y` : [n_samples] 크기의 배열 
    * 종속 변수

## X 변수 1개/ y class 1개


```python
from sklearn.datasets import make_classification

X, y = make_classification(n_features=1, # 독립변수는 X 하나
                           n_informative=1, # Y 변수와 관련되는 X변수의 수 X변수가 1개이므로 1보단 작아야한다.
                           n_redundant=0, # 독립변수중 다른 독립변수와 선형조합으로 나타나는 성분의 수 즉 X3= X1+3X2 
                           n_clusters_per_class=1, # 클래스당 클러스터의 수
                           random_state=4)
```


```python
plt.scatter(X, y, marker='o', c=y, s=100, edgecolor="k", linewidth=2)

plt.xlabel("$X$")
plt.ylabel("$y$")
```




    Text(0, 0.5, '$y$')




    
![png](/assets/images/{Generating}_Make_random_data/output_7_1.png)
    


## X변수 2개/y class 1개

x변수중 1개만 y class 에 연관되는 경우


```python
X, y = make_classification(n_features=2,  # 독립변수는 X1,X2 둘
                           n_informative=1, # Y 변수와 관련되는 X변수의 
                           n_redundant=0, # 독립변수중 다른 독립변수와 선형조합으로 나타나는 성분의 수 
                           n_clusters_per_class=1, 
                           random_state=4)

plt.scatter(X[:, 0], X[:, 1], marker='o', c=y, s=100, edgecolor="k", linewidth=2)

plt.xlabel("$X_1$")
plt.ylabel("$X_2$")
plt.show()
```


    
![png](/assets/images/{Generating}_Make_random_data/output_10_0.png)
    


x변수 2개가 모두 y class 에 연관되는 경우


```python
X, y = make_classification(n_samples=500, 
                           n_features=2,
                           n_informative=2,
                           n_redundant=0,
                           n_clusters_per_class=1, 
                           random_state=6)
plt.scatter(X[:, 0], X[:, 1], marker='o', c=y,
            s=100, edgecolor="k", linewidth=2)

plt.xlim(-4, 4)
plt.ylim(-4, 4)
plt.xlabel("$X_1$")
plt.ylabel("$X_2$");
```


    
![png](/assets/images/{Generating}_Make_random_data/output_12_0.png)
    


## class 별 데이터 갯수에 차이가 있는 경우

클래스 별 데이터의 갯수에 차이를 주고 싶을 땐, weights인수를 설정하면 된다. 이는 추후 배울 비대칭데이터를 시뮬레이션 할 때 사용할 것이다. 다음 코드에서는 weight인수를 각 각 0.9, 0.1로 설정 했다


```python
X, y = make_classification(n_features=2,  # 독립변수는 X1,X2 둘
                           n_informative=2, # Y 변수와 관련되는 X변수의 수
                           n_redundant=0, # 독립변수중 다른 독립변수와 선형조합으로 나타나는 성분의 수 
                           n_clusters_per_class=1, 
                           weights=[0.9, 0.1], # 데이터 별 클래스 갯수의 차이
                           random_state=6)

plt.scatter(X[:, 0], X[:, 1], marker='o', c=y, s=100, edgecolor="k", linewidth=2)
plt.xlabel("$X_1$")
plt.ylabel("$X_2$") ;
```


    
![png](/assets/images/{Generating}_Make_random_data/output_15_0.png)
    


## 클래스끼리 분리가 되지 않은 무작위 패턴

`n_clusters_per_class` 인수를 2로 설정하여, 클래스 당 클러스터 갯수를 늘리면 다음 코드의 결과 처럼 클래스 끼리 잘 분리되어 있지 않은 가상데이터를 얻을 수 있다. 클래스 당 클러스터 갯수를 설정할 때 주의 할 점은 $\text{n_classes} \times \text{n_clusters_per_class}$ 는  $2^{\text{n_informative}}$보다 작거나 같도록 설정해야 한다는 것이다. 


```python
X2, Y2 = make_classification(n_samples=400, 
                             n_features=2, 
                             n_informative=2, 
                             n_redundant=0,
                             n_clusters_per_class=2, 
                             random_state=0)

plt.scatter(X2[:, 0], X2[:, 1], marker='o', c=Y2,s=100, edgecolor="k", linewidth=2)
plt.xlabel("$X_1$")
plt.ylabel("$X_2$")
plt.show()
```


    
![png](/assets/images/{Generating}_Make_random_data/output_18_0.png)
    


## y클래스가 n개 


```python
X, y = make_classification(n_samples=300, n_features=2, n_informative=2, n_redundant=0,
                           n_clusters_per_class=1, n_classes=3, random_state=0)
plt.scatter(X[:, 0], X[:, 1], marker='o', c=y,
            s=100, edgecolor="k", linewidth=2)

plt.xlabel("$X_1$")
plt.ylabel("$X_2$")
plt.show()
```


    
![png](/assets/images/{Generating}_Make_random_data/output_20_0.png)
    


## 가우시안 정규분포 가상데이터

`make_blobs` 함수는 등방성 가우시안 정규분포를 이용해 가상 데이터를 생성한다. 이 때 등방성이라는 말은 모든 방향으로 같은 성질을 가진다는 뜻이다. 다음 데이터 생성 코드의 결과를 보면 `make_classification` 함수로 만든 가상데이터와  모양이 다른 것을 확인 할 수 있다. `make_blobs`는 보통 클러스링 용 가상데이터를 생성하는데 사용한다. `make_blobs` 함수의 인수와 반환값은 다음과 같다.

* 인수:	
 * `n_samples` : 표본 데이터의 수, 디폴트 100
 * `n_features` : 독립 변수의 수, 디폴트 20
 * `centers` : 생성할 클러스터의 수 혹은 중심, [n_centers, n_features] 크기의 배열. 디폴트 3
 * `cluster_std`: 클러스터의 표준 편차, 디폴트 1.0
 * `center_box`: 생성할 클러스터의 바운딩 박스(bounding box), 디폴트 (-10.0, 10.0)) 
   
* 반환값:	
 * `X` : [n_samples, n_features] 크기의 배열 
    * 독립 변수
 * `y` : [n_samples] 크기의 배열 
    * 종속 변수


```python
from sklearn.datasets import make_blobs

plt.title("3 class")
X, y = make_blobs(n_samples=300,
                  n_features=2, 
                  centers=3, 
                  random_state=1)
plt.scatter(X[:, 0], X[:, 1], marker='o', c=y, s=100,edgecolor="k", linewidth=2)
plt.xlabel("$X_1$")
plt.ylabel("$X_2$")
plt.show()
```


    
![png](/assets/images/{Generating}_Make_random_data/output_23_0.png)
    


## 초승달 모양 데이터

make_moons` 함수는 초승달 모양 클러스터 두 개 형상의 데이터를 생성한다. `make_moons` 명령으로 만든 데이터는 직선을 사용하여 분류할 수 없다.

* 인수:	
 * `n_samples` : 표본 데이터의 수, 디폴트 100
 * `noise`: 잡음의 크기. 0이면 정확한 반원을 이룸


```python
from sklearn.datasets import make_moons

X, y = make_moons(n_samples=400, 
                  noise=0.1, 
                  random_state=0)

plt.scatter(X[:, 0], X[:, 1], marker='o', c=y, s=100,edgecolor="k", linewidth=2)
plt.xlabel("$X_1$")
plt.ylabel("$X_2$")
plt.show()
```


    
![png](/assets/images/{Generating}_Make_random_data/output_26_0.png)
    


# Make Regression data

`make_regression()` 명령은 내부적으로 입력(독립 변수) 데이터인 $X$ 행렬, 잡음 $\epsilon$ 벡터, 계수 $w$ 벡터를 확률적으로 생성한 후, 위 관계식에 따라 출력(종속 변수) 데이터 $y$ 벡터를 계산하여 $X$, $y$ 값을 출력한다. 자세한 사용법은 다음과 같다.

```
X, y = make_regression(...)
```
또는
```
X, y, w = make_regression(..., coef=True, ...)
```

입력 인수는 다음과 같다.

 * `n_samples` : 정수 (옵션, 디폴트 100)
    * 표본 데이터의 갯수 $N$
 * `n_features` : 정수 (옵션, 디폴트 100)
    * 독립 변수(feature)의 수(차원) $M$
 * `n_targets` : 정수 (옵션, 디폴트 1)
    * 종속 변수(target)의 수(차원)
 * `bias` : 실수 (옵션, 디폴트 0.0)
    * y 절편
 * `noise` : 실수 (옵션, 디폴트 0.0)
    * 출력 즉, 종속 변수에 더해지는 잡음 $\epsilon$의 표준 편차
 * `coef` : 불리언 (옵션, 디폴트 False)
   * True 이면 선형 모형의 계수도 출력
 * `random_state` : 정수 (옵션, 디폴트 None)
   * 난수 발생용 시드값 
 * `n_informative` : 정수 (옵션, 디폴트 10)
    * 독립 변수(feature) 중 실제로 종속 변수와 상관 관계가 있는 독립 변수의 수(차원)
 * `effective_rank`: 정수 또는 None (옵션, 디폴트 None)
    * 독립 변수(feature) 중 서로 독립인 독립 변수의 수. 만약 None이면 모두 독립
 * `tail_strength` : 0부터 1사이의 실수 (옵션, 디폴트 0.5)
    * `effective_rank`가 None이 아닌 경우 독립 변수간의 상관관계를 결정하는 변수. 0.5면 독립 변수간의 상관관계가 없다.  

출력은 다음과 같다.

 * `X` : [`n_samples`, `n_features`] 형상의 2차원 배열
    * 독립 변수의 표본 데이터 행렬 $X$
 * `y` : [`n_samples`] 형상의 1차원 배열 또는 [`n_samples`, `n_targets`] 형상의 2차원 배열
    * 종속 변수의 표본 데이터 벡터 $y$
 * `coef` : [`n_features`] 형상의 1차원 배열 또는 [`n_features`, `n_targets`] 형상의 2차원 배열 (옵션)
    * 선형 모형의 계수 벡터 $w$, 입력 인수 `coef`가 True 인 경우에만 출력됨

## noise = 0 


```python
from sklearn.datasets import make_regression

X, y, w = make_regression(n_samples=10, 
                          n_features=1, 
                          bias=0, 
                          noise=0,
                          coef=True, 
                          random_state=0)
```


```python
display(X, y ,w) 
```


    array([[ 0.97873798],
           [ 2.2408932 ],
           [ 1.86755799],
           [ 0.95008842],
           [ 1.76405235],
           [ 0.4105985 ],
           [-0.97727788],
           [ 0.40015721],
           [-0.10321885],
           [-0.15135721]])



    array([ 77.48913677, 177.41712535, 147.85924209,  75.22087885,
           139.66444108,  32.50811146, -77.37353667,  31.6814481 ,
            -8.17209494, -11.98332915])



    array(79.17250381)



```python
plt.scatter(X, y)
plt.xlabel("x")
plt.ylabel("y")
```




    Text(0, 0.5, 'y')




    
![png](/assets/images/{Generating}_Make_random_data/output_32_1.png)
    


## noise 가 있는 경우


```python
X, y, w = make_regression(n_samples=50, n_features=1, bias=100, noise=10,
                          coef=True, random_state=0)
plt.scatter(X, y, s=100)
plt.xlabel("x")
plt.ylabel("y")
plt.show()
```


    
![png](/assets/images/{Generating}_Make_random_data/output_34_0.png)
    


## X1,X2 / 독립/ 둘다 Y 와 관련

`make_regression` 명령은 위에서 설명한 인수 이외에도 다음과 같은 인수를 가질 수 있다.

* `n_informative` : 정수 (옵션, 디폴트 10)
    * 독립 변수(feature) 중 실제로 종속 변수와 상관 관계가 있는 독립 변수의 수(차원)
* `effective_rank`: 정수 또는 None (옵션, 디폴트 None)
    * 독립 변수(feature) 중 서로 독립인 독립 변수의 수. 만약 None이면 모두 독립
* `tail_strength` : 0부터 1사이의 실수 (옵션, 디폴트 0.5)
    * `effective_rank`가 None이 아닌 경우 독립 변수간의 상관관계를 결정하는 변수. 0.5면 독립 변수간의 상관관계가 없다.


```python
X, y, w = make_regression(n_samples=300, 
                          n_features=2,
                          noise=10,
                          coef=True, 
                          random_state=0)

plt.scatter(X[:, 0], X[:, 1], c=y, s=100, cmap=mpl.cm.bone)
plt.xlabel("x1")
plt.ylabel("x2") ;
```


    
![png](/assets/images/{Generating}_Make_random_data/output_37_0.png)
    


## X1,X2 독립이 아닌 경우

만약 두 독립 변수가 서로 독립이 아니고 상관관계를 가지는 경우에는 tail_strength 인수를 0에 가까운 작은 값으로 설정한다. 


```python
X, y, w = make_regression(n_samples=300, n_features=2, effective_rank=1, noise=0,
                          tail_strength=0, coef=True, random_state=0)

plt.scatter(X[:, 0], X[:, 1], c=y, s=100, cmap=mpl.cm.bone)
plt.xlabel("x1")
plt.ylabel("x2")
plt.axis("equal")
plt.show()
```


    
![png](/assets/images/{Generating}_Make_random_data/output_40_0.png)
    


# 내장 분류 데이터셋

## iris 꽃 유형예측

붓꽃 데이터는 통계학자 피셔(R.A Fisher)의 붓꽃의 분류 연구에 기반한 데이터다. load_iris() 명령으로 로드한다. 데이터는 다음과 같이 구성되어 있다.

타겟 데이터
- setosa, versicolor, virginica의 세가지 붓꽃 종(species)

특징 데이터

- 꽃받침 길이(Sepal Length) 
- 꽃받침 폭(Sepal Width) 
- 꽃잎 길이(Petal Length) 
- 꽃잎 폭(Petal Width) 



```python
from sklearn.datasets import load_iris
iris = load_iris()
```


```python
df = pd.DataFrame(iris.data, columns=iris.feature_names)
sy = pd.Series(iris.target, dtype="category")
sy = sy.cat.rename_categories(iris.target_names)
df['species'] = sy
df.tail()
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
      <th>sepal length (cm)</th>
      <th>sepal width (cm)</th>
      <th>petal length (cm)</th>
      <th>petal width (cm)</th>
      <th>species</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>145</th>
      <td>6.7</td>
      <td>3.0</td>
      <td>5.2</td>
      <td>2.3</td>
      <td>virginica</td>
    </tr>
    <tr>
      <th>146</th>
      <td>6.3</td>
      <td>2.5</td>
      <td>5.0</td>
      <td>1.9</td>
      <td>virginica</td>
    </tr>
    <tr>
      <th>147</th>
      <td>6.5</td>
      <td>3.0</td>
      <td>5.2</td>
      <td>2.0</td>
      <td>virginica</td>
    </tr>
    <tr>
      <th>148</th>
      <td>6.2</td>
      <td>3.4</td>
      <td>5.4</td>
      <td>2.3</td>
      <td>virginica</td>
    </tr>
    <tr>
      <th>149</th>
      <td>5.9</td>
      <td>3.0</td>
      <td>5.1</td>
      <td>1.8</td>
      <td>virginica</td>
    </tr>
  </tbody>
</table>
</div>



## 와인 가격예측

와인의 화학 조성을 사용하여 와인의 종류를 예측하기 위한 데이터이다. load_wine() 명령으로 로드하며 다음과 같이 구성되어 있다.

타겟 데이터

- 와인의 종류 0, 1, 2의 세가지 값

특징 데이터

- 알콜(Alcohol)
- 말산(Malic acid)
- 회분(Ash)
- 회분의 알칼리도(Alcalinity of ash)
- 마그네슘(Magnesium)
- 총 폴리페놀(Total phenols)
- 플라보노이드 폴리페놀(Flavanoids)
- 비 플라보노이드 폴리페놀(Nonflavanoid phenols)
- 프로안토시아닌(Proanthocyanins)
- 색상의 강도(Color intensity)
- 색상(Hue)
- 희석 와인의 OD280/OD315 비율 (OD280/OD315 of diluted wines)
- 프롤린(Proline)



```python
from sklearn.datasets import load_wine
wine = load_wine()
```


```python
X = pd.DataFrame(wine.data, columns=wine.feature_names)
y = pd.Series(wine.target, dtype="category")
sy = y.cat.rename_categories(wine.target_names)
df['class'] = sy
df.tail()
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
      <th>sepal length (cm)</th>
      <th>sepal width (cm)</th>
      <th>petal length (cm)</th>
      <th>petal width (cm)</th>
      <th>species</th>
      <th>class</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>145</th>
      <td>6.7</td>
      <td>3.0</td>
      <td>5.2</td>
      <td>2.3</td>
      <td>virginica</td>
      <td>class_2</td>
    </tr>
    <tr>
      <th>146</th>
      <td>6.3</td>
      <td>2.5</td>
      <td>5.0</td>
      <td>1.9</td>
      <td>virginica</td>
      <td>class_2</td>
    </tr>
    <tr>
      <th>147</th>
      <td>6.5</td>
      <td>3.0</td>
      <td>5.2</td>
      <td>2.0</td>
      <td>virginica</td>
      <td>class_2</td>
    </tr>
    <tr>
      <th>148</th>
      <td>6.2</td>
      <td>3.4</td>
      <td>5.4</td>
      <td>2.3</td>
      <td>virginica</td>
      <td>class_2</td>
    </tr>
    <tr>
      <th>149</th>
      <td>5.9</td>
      <td>3.0</td>
      <td>5.1</td>
      <td>1.8</td>
      <td>virginica</td>
      <td>class_2</td>
    </tr>
  </tbody>
</table>
</div>




```python
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.30, random_state=42)
```

## 유방암 진단 데이터


```python
from sklearn.datasets import load_breast_cancer
cancer = load_breast_cancer()

```


```python
X = pd.DataFrame(cancer.data, columns=cancer.feature_names)
y = pd.Series(cancer.target, dtype="category")
sy = y.cat.rename_categories(cancer.target_names)
df['class'] = sy
df.tail()

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
      <th>sepal length (cm)</th>
      <th>sepal width (cm)</th>
      <th>petal length (cm)</th>
      <th>petal width (cm)</th>
      <th>species</th>
      <th>class</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>145</th>
      <td>6.7</td>
      <td>3.0</td>
      <td>5.2</td>
      <td>2.3</td>
      <td>virginica</td>
      <td>benign</td>
    </tr>
    <tr>
      <th>146</th>
      <td>6.3</td>
      <td>2.5</td>
      <td>5.0</td>
      <td>1.9</td>
      <td>virginica</td>
      <td>malignant</td>
    </tr>
    <tr>
      <th>147</th>
      <td>6.5</td>
      <td>3.0</td>
      <td>5.2</td>
      <td>2.0</td>
      <td>virginica</td>
      <td>benign</td>
    </tr>
    <tr>
      <th>148</th>
      <td>6.2</td>
      <td>3.4</td>
      <td>5.4</td>
      <td>2.3</td>
      <td>virginica</td>
      <td>benign</td>
    </tr>
    <tr>
      <th>149</th>
      <td>5.9</td>
      <td>3.0</td>
      <td>5.1</td>
      <td>1.8</td>
      <td>virginica</td>
      <td>benign</td>
    </tr>
  </tbody>
</table>
</div>



## 대표 수종 데이터
 

대표 수종 데이터는 미국 삼림을 30×30m 영역으로 나누어 각 영역의 특징으로부터 대표적인 나무의 종류(species of tree)을 예측하기위한 데이터이다. 수종은 7종류이지만 특징 데이터가 54종류, 표본 데이터의 갯수가 581,012개에 달하는 대규모 데이터이다.




```python
from sklearn.datasets import fetch_covtype
covtype = fetch_covtype()
```


```python
X = pd.DataFrame(covtype.data, 
                  columns=["x{:02d}".format(i + 1) for i in range(covtype.data.shape[1])],
                  dtype=int)
y = covtype.target
```


```python
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.30, random_state=42)
```


```python
pd.DataFrame(df.nunique()).T
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
      <th>x01</th>
      <th>x02</th>
      <th>x03</th>
      <th>x04</th>
      <th>x05</th>
      <th>x06</th>
      <th>x07</th>
      <th>x08</th>
      <th>x09</th>
      <th>x10</th>
      <th>...</th>
      <th>x46</th>
      <th>x47</th>
      <th>x48</th>
      <th>x49</th>
      <th>x50</th>
      <th>x51</th>
      <th>x52</th>
      <th>x53</th>
      <th>x54</th>
      <th>covtype</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1978</td>
      <td>361</td>
      <td>67</td>
      <td>551</td>
      <td>700</td>
      <td>5785</td>
      <td>207</td>
      <td>185</td>
      <td>255</td>
      <td>5827</td>
      <td>...</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
<p>1 rows × 55 columns</p>
</div>




```python
df.iloc[:, 10:54] = df.iloc[:, 10:54].astype('category')
```

# 내장 데이터셋

from sklearn.model_selection import train_test_split <br>
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.30, random_state=42)

## 보스턴 집값예측

타겟 데이터
- 1978 보스턴 주택 가격
- 506개 타운의 주택 가격 중앙값 (단위 1,000 달러)

특징 데이터
- CRIM: 범죄율
- INDUS: 비소매상업지역 면적 비율
- NOX: 일산화질소 농도
- RM: 주택당 방 수
- LSTAT: 인구 중 하위 계층 비율
- B: 인구 중 흑인 비율
- PTRATIO: 학생/교사 비율
- ZN: 25,000 평방피트를 초과 거주지역 비율
- CHAS: 찰스강의 경계에 위치한 경우는 1, 아니면 0
- AGE: 1940년 이전에 건축된 주택의 비율
- RAD: 방사형 고속도로까지의 거리
- DIS: 직업센터의 거리
- TAX: 재산세율

데이터 특징
- 회귀분석에 이용할 수 있다.
- categorical 이 하나도 없음
- 곁측치도 하나도 없다.
- (506,14) 의 데이터


```python
from sklearn.datasets import load_boston
import pandas as pd
boston = load_boston() 
X = pd.DataFrame(boston.data, columns=boston.feature_names)
y = pd.DataFrame(boston.target, columns=["MEDV"])
df = pd.concat([X, y], axis=1)
df.tail()
y = boston.target #많은 모델들이 y 는 1dim 을 기대할떄가 많아서
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
      <th>CRIM</th>
      <th>ZN</th>
      <th>INDUS</th>
      <th>CHAS</th>
      <th>NOX</th>
      <th>RM</th>
      <th>AGE</th>
      <th>DIS</th>
      <th>RAD</th>
      <th>TAX</th>
      <th>PTRATIO</th>
      <th>B</th>
      <th>LSTAT</th>
      <th>MEDV</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>501</th>
      <td>0.06263</td>
      <td>0.0</td>
      <td>11.93</td>
      <td>0.0</td>
      <td>0.573</td>
      <td>6.593</td>
      <td>69.1</td>
      <td>2.4786</td>
      <td>1.0</td>
      <td>273.0</td>
      <td>21.0</td>
      <td>391.99</td>
      <td>9.67</td>
      <td>22.4</td>
    </tr>
    <tr>
      <th>502</th>
      <td>0.04527</td>
      <td>0.0</td>
      <td>11.93</td>
      <td>0.0</td>
      <td>0.573</td>
      <td>6.120</td>
      <td>76.7</td>
      <td>2.2875</td>
      <td>1.0</td>
      <td>273.0</td>
      <td>21.0</td>
      <td>396.90</td>
      <td>9.08</td>
      <td>20.6</td>
    </tr>
    <tr>
      <th>503</th>
      <td>0.06076</td>
      <td>0.0</td>
      <td>11.93</td>
      <td>0.0</td>
      <td>0.573</td>
      <td>6.976</td>
      <td>91.0</td>
      <td>2.1675</td>
      <td>1.0</td>
      <td>273.0</td>
      <td>21.0</td>
      <td>396.90</td>
      <td>5.64</td>
      <td>23.9</td>
    </tr>
    <tr>
      <th>504</th>
      <td>0.10959</td>
      <td>0.0</td>
      <td>11.93</td>
      <td>0.0</td>
      <td>0.573</td>
      <td>6.794</td>
      <td>89.3</td>
      <td>2.3889</td>
      <td>1.0</td>
      <td>273.0</td>
      <td>21.0</td>
      <td>393.45</td>
      <td>6.48</td>
      <td>22.0</td>
    </tr>
    <tr>
      <th>505</th>
      <td>0.04741</td>
      <td>0.0</td>
      <td>11.93</td>
      <td>0.0</td>
      <td>0.573</td>
      <td>6.030</td>
      <td>80.8</td>
      <td>2.5050</td>
      <td>1.0</td>
      <td>273.0</td>
      <td>21.0</td>
      <td>396.90</td>
      <td>7.88</td>
      <td>11.9</td>
    </tr>
  </tbody>
</table>
</div>




```python
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.30, random_state=42)
```


```python
df.info()
#print(boston.DESCR) 를 하면 정보를 더 볼 수 있다.
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 506 entries, 0 to 505
    Data columns (total 14 columns):
     #   Column   Non-Null Count  Dtype  
    ---  ------   --------------  -----  
     0   CRIM     506 non-null    float64
     1   ZN       506 non-null    float64
     2   INDUS    506 non-null    float64
     3   CHAS     506 non-null    float64
     4   NOX      506 non-null    float64
     5   RM       506 non-null    float64
     6   AGE      506 non-null    float64
     7   DIS      506 non-null    float64
     8   RAD      506 non-null    float64
     9   TAX      506 non-null    float64
     10  PTRATIO  506 non-null    float64
     11  B        506 non-null    float64
     12  LSTAT    506 non-null    float64
     13  MEDV     506 non-null    float64
    dtypes: float64(14)
    memory usage: 55.5 KB
    

## 캘리포니아 집값예측

타겟 데이터
- 1990년 캘리포니아의 각 행정 구역 내 주택 가격의 중앙값

특징 데이터
- MedInc : 행정 구역 내 소득의 중앙값
- HouseAge : 행정 구역 내 주택 연식의 중앙값
- AveRooms : 평균 방 갯수
- AveBedrms : 평균 침실 갯수
- Population : 행정 구역 내 인구 수
- AveOccup : 평균 자가 비율
- Latitude : 해당 행정 구역의 위도
- Longitude : 해당 행정 구역의 경도

데이터 특징
- 곁측치가 없는 회귀 데이터 
- (20640, 9)


```python
from sklearn.datasets import fetch_california_housing
import pandas as pd
california = fetch_california_housing()
X = pd.DataFrame(california.data, columns=california.feature_names)
y = pd.DataFrame(california.target,columns=["Target"])
df = pd.concat([X, y], axis=1)
df.tail()
y = california.target
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
      <th>MedInc</th>
      <th>HouseAge</th>
      <th>AveRooms</th>
      <th>AveBedrms</th>
      <th>Population</th>
      <th>AveOccup</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Target</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>20635</th>
      <td>1.5603</td>
      <td>25.0</td>
      <td>5.045455</td>
      <td>1.133333</td>
      <td>845.0</td>
      <td>2.560606</td>
      <td>39.48</td>
      <td>-121.09</td>
      <td>0.781</td>
    </tr>
    <tr>
      <th>20636</th>
      <td>2.5568</td>
      <td>18.0</td>
      <td>6.114035</td>
      <td>1.315789</td>
      <td>356.0</td>
      <td>3.122807</td>
      <td>39.49</td>
      <td>-121.21</td>
      <td>0.771</td>
    </tr>
    <tr>
      <th>20637</th>
      <td>1.7000</td>
      <td>17.0</td>
      <td>5.205543</td>
      <td>1.120092</td>
      <td>1007.0</td>
      <td>2.325635</td>
      <td>39.43</td>
      <td>-121.22</td>
      <td>0.923</td>
    </tr>
    <tr>
      <th>20638</th>
      <td>1.8672</td>
      <td>18.0</td>
      <td>5.329513</td>
      <td>1.171920</td>
      <td>741.0</td>
      <td>2.123209</td>
      <td>39.43</td>
      <td>-121.32</td>
      <td>0.847</td>
    </tr>
    <tr>
      <th>20639</th>
      <td>2.3886</td>
      <td>16.0</td>
      <td>5.254717</td>
      <td>1.162264</td>
      <td>1387.0</td>
      <td>2.616981</td>
      <td>39.37</td>
      <td>-121.24</td>
      <td>0.894</td>
    </tr>
  </tbody>
</table>
</div>




```python
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.30, random_state=42)
```


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 20640 entries, 0 to 20639
    Data columns (total 9 columns):
     #   Column      Non-Null Count  Dtype  
    ---  ------      --------------  -----  
     0   MedInc      20640 non-null  float64
     1   HouseAge    20640 non-null  float64
     2   AveRooms    20640 non-null  float64
     3   AveBedrms   20640 non-null  float64
     4   Population  20640 non-null  float64
     5   AveOccup    20640 non-null  float64
     6   Latitude    20640 non-null  float64
     7   Longitude   20640 non-null  float64
     8   Target      20640 non-null  float64
    dtypes: float64(9)
    memory usage: 1.4 MB
    

## 당뇨병 진행률 예측

442명의 당뇨병 환자를 대상으로한 검사 결과를 나타내는 데이터이다.

타겟 데이터
- 1년 뒤 측정한 당뇨병의 진행률

특징 데이터 (이 데이터셋의 특징 데이터는 모두 정규화된 값이다.)
- Age
- Sex
- Body mass index
- Average blood pressure
- S1 (혈청 측정에 대한 6가지 특징값.)
- S2
- S3
- S4
- S5
- S6


데이터 특징 
- 곁측치가 없다.
- (441,11) 데이터


```python
from sklearn.datasets import load_diabetes
import pandas as pd
diabetes = load_diabetes()
# print(diabetes.DESCR)
X = pd.DataFrame(diabetes.data, columns=diabetes.feature_names)
y = pd.DataFrame(diabetes.target,columns=["Target"])
df = pd.concat([X, y], axis=1)
df.tail()
y = diabetes.target
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
      <th>age</th>
      <th>sex</th>
      <th>bmi</th>
      <th>bp</th>
      <th>s1</th>
      <th>s2</th>
      <th>s3</th>
      <th>s4</th>
      <th>s5</th>
      <th>s6</th>
      <th>Target</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>437</th>
      <td>0.041708</td>
      <td>0.050680</td>
      <td>0.019662</td>
      <td>0.059744</td>
      <td>-0.005697</td>
      <td>-0.002566</td>
      <td>-0.028674</td>
      <td>-0.002592</td>
      <td>0.031193</td>
      <td>0.007207</td>
      <td>178.0</td>
    </tr>
    <tr>
      <th>438</th>
      <td>-0.005515</td>
      <td>0.050680</td>
      <td>-0.015906</td>
      <td>-0.067642</td>
      <td>0.049341</td>
      <td>0.079165</td>
      <td>-0.028674</td>
      <td>0.034309</td>
      <td>-0.018118</td>
      <td>0.044485</td>
      <td>104.0</td>
    </tr>
    <tr>
      <th>439</th>
      <td>0.041708</td>
      <td>0.050680</td>
      <td>-0.015906</td>
      <td>0.017282</td>
      <td>-0.037344</td>
      <td>-0.013840</td>
      <td>-0.024993</td>
      <td>-0.011080</td>
      <td>-0.046879</td>
      <td>0.015491</td>
      <td>132.0</td>
    </tr>
    <tr>
      <th>440</th>
      <td>-0.045472</td>
      <td>-0.044642</td>
      <td>0.039062</td>
      <td>0.001215</td>
      <td>0.016318</td>
      <td>0.015283</td>
      <td>-0.028674</td>
      <td>0.026560</td>
      <td>0.044528</td>
      <td>-0.025930</td>
      <td>220.0</td>
    </tr>
    <tr>
      <th>441</th>
      <td>-0.045472</td>
      <td>-0.044642</td>
      <td>-0.073030</td>
      <td>-0.081414</td>
      <td>0.083740</td>
      <td>0.027809</td>
      <td>0.173816</td>
      <td>-0.039493</td>
      <td>-0.004220</td>
      <td>0.003064</td>
      <td>57.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.30, random_state=42)
```


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 442 entries, 0 to 441
    Data columns (total 11 columns):
     #   Column  Non-Null Count  Dtype  
    ---  ------  --------------  -----  
     0   age     442 non-null    float64
     1   sex     442 non-null    float64
     2   bmi     442 non-null    float64
     3   bp      442 non-null    float64
     4   s1      442 non-null    float64
     5   s2      442 non-null    float64
     6   s3      442 non-null    float64
     7   s4      442 non-null    float64
     8   s5      442 non-null    float64
     9   s6      442 non-null    float64
     10  Target  442 non-null    float64
    dtypes: float64(11)
    memory usage: 38.1 KB
    

## 타이타닉 생존 예측


```python
from seaborn import load_dataset
titanic=load_dataset('titanic')
titanic.head()
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
      <th>survived</th>
      <th>pclass</th>
      <th>sex</th>
      <th>age</th>
      <th>sibsp</th>
      <th>parch</th>
      <th>fare</th>
      <th>embarked</th>
      <th>class</th>
      <th>who</th>
      <th>adult_male</th>
      <th>deck</th>
      <th>embark_town</th>
      <th>alive</th>
      <th>alone</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>7.2500</td>
      <td>S</td>
      <td>Third</td>
      <td>man</td>
      <td>True</td>
      <td>NaN</td>
      <td>Southampton</td>
      <td>no</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>71.2833</td>
      <td>C</td>
      <td>First</td>
      <td>woman</td>
      <td>False</td>
      <td>C</td>
      <td>Cherbourg</td>
      <td>yes</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>3</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>7.9250</td>
      <td>S</td>
      <td>Third</td>
      <td>woman</td>
      <td>False</td>
      <td>NaN</td>
      <td>Southampton</td>
      <td>yes</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>1</td>
      <td>female</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>53.1000</td>
      <td>S</td>
      <td>First</td>
      <td>woman</td>
      <td>False</td>
      <td>C</td>
      <td>Southampton</td>
      <td>yes</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>3</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>8.0500</td>
      <td>S</td>
      <td>Third</td>
      <td>man</td>
      <td>True</td>
      <td>NaN</td>
      <td>Southampton</td>
      <td>no</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



## iris 데이터 꽃 유형예측


```python
from seaborn import load_dataset
iris=load_dataset('iris')
iris.head()
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
      <th>sepal_length</th>
      <th>sepal_width</th>
      <th>petal_length</th>
      <th>petal_width</th>
      <th>species</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5.1</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.7</td>
      <td>3.2</td>
      <td>1.3</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>setosa</td>
    </tr>
  </tbody>
</table>
</div>



## 다이아몬드 가격예측


```python
from seaborn import load_dataset
diamonds=load_dataset('diamonds')
diamonds.head()
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



# Reference

- https://datascienceschool.net/
- https://scikit-learn.org/stable/modules/generated/sklearn.datasets.make_regression.html



```python

```

