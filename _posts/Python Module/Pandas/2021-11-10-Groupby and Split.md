---
title:  "Groupby and Make Data Dict"
excerpt: "class 별로 Groupby 이후, 분할하기"
categories:
  - Py_Pandas
last_modified_at: 2021-11-10
toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

> ## Groupby and Split

```python
import pandas as pd
from sklearn.datasets import load_wine
wine = load_wine()

X = pd.DataFrame(wine.data, columns=wine.feature_names)
y = pd.Series(wine.target, dtype="category")
sy = y.cat.rename_categories(wine.target_names)
df = X.copy()
df['class'] = sy
df
```

|      | alcohol | malic_acid |  ash | alcalinity_of_ash | magnesium | total_phenols | flavanoids | nonflavanoid_phenols | proanthocyanins | color_intensity |  hue | od280/od315_of_diluted_wines | proline |   class |
| :--- | ------: | ---------: | ---: | ----------------: | --------: | ------------: | ---------: | -------------------: | --------------: | --------------: | ---: | ---------------------------: | ------: | ------: |
| 0    |   14.23 |       1.71 | 2.43 |              15.6 |     127.0 |          2.80 |       3.06 |                 0.28 |            2.29 |            5.64 | 1.04 |                         3.92 |  1065.0 | class_0 |
| 1    |   13.20 |       1.78 | 2.14 |              11.2 |     100.0 |          2.65 |       2.76 |                 0.26 |            1.28 |            4.38 | 1.05 |                         3.40 |  1050.0 | class_0 |
| 2    |   13.16 |       2.36 | 2.67 |              18.6 |     101.0 |          2.80 |       3.24 |                 0.30 |            2.81 |            5.68 | 1.03 |                         3.17 |  1185.0 | class_0 |
| 3    |   14.37 |       1.95 | 2.50 |              16.8 |     113.0 |          3.85 |       3.49 |                 0.24 |            2.18 |            7.80 | 0.86 |                         3.45 |  1480.0 | class_0 |
| 4    |   13.24 |       2.59 | 2.87 |              21.0 |     118.0 |          2.80 |       2.69 |                 0.39 |            1.82 |            4.32 | 1.04 |                         2.93 |   735.0 | class_0 |

- 위처럼 가상의 데이터 프레임을 만들어봅시다.
- 우리의 목적은 Class 별로 data frame 을 쪼갠뒤에 각각의 값을 key 로 가지는 dict 를 만드는게 목적입니다.
- 즉 이 경우에는 { class_0 : df , class_1 : df .... }의 형식이 될 것입니다.

```python
dic = {}
gb = df.groupby('class')    
# gb.groups : 그룹이 어떻게 구별되는지를 알려줌
for x in gb.groups : 
    # gb.get_group(x) : x 로 구별되는 dataframe 짝을 알려줌
    dic[x] = gb.get_group(x) 
```

- 위 처럼 수행한다면 다음과 같은 dict 가 나오게 됩니다.

```python
dic.keys()
# dict_keys(['class_0', 'class_1', 'class_2'])
```

- 각 key 에 해당하는 df 가 저장된 모습
