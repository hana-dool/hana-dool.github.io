---
title:  "XGboost"
excerpt: "xgboost classification"
categories:
  - Py_Classification
last_modified_at: 2021-12-15

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 파이썬의 예외 처리 방법에 대해서 작게나마 알아봅시다.
{: .notice--warning}

# [XG boost example](#link){: .btn .btn--primary}{: .align-center}

> ## Example

```python
from xgboost import XGBClassifier
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score
from sklearn.datasets import load_wine
```

- 필요한 모듈 import 합니다.

```python
X, y = load_wine(return_X_y=True, as_frame=True)
```

- 위와 같이 필요한 데이터를 가져옵니다.

---

**reference**

- <https://dojang.io/mod/page/view.php?id=2399>





