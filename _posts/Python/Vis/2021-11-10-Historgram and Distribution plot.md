---
title:  "Histogram and Distribution plot"
excerpt: "데이터에 대한 히스토그램과, 그 위에 FItting 되는 분포 그리기"
categories:
  - Py_Visualization
last_modified_at: 2021-11-10

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

math_use: true
---

 내가 가지는 데이터가 과연 진짜 어떤 분포를 따르는지에 대해서 알려주는 분포를 그려봅시다. 
{: .notice--warning}

> ## Histogram and Distribution

```python
# 준비 작업
import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import norm

# 임의의 데이터를 Generating 해 봅시다.
data = norm.rvs(10.0, 2.5, size=500)

# 저희가 보고자 하는 distribution 의 fit 메서드를 활용하여 parameter 를 뽑아냅니다.
mu, std = norm.fit(data)

# 히스토그램을 그립니다. 
plt.hist(data, bins=25, density=True, alpha=0.6, color='g')

# plt.xlim() 은 plt 객체의 min , max 정보를 출력해줍니다. 
# 즉 앞에서의 hist 에서 data 를 fitting 했으므로, 그 데이터의 min , max 를 범위로 지정하는 것입니다.
xmin, xmax = plt.xlim() 
x = np.linspace(xmin, xmax, 100)
p = norm.pdf(x, mu, std)

# density plot 그리기
plt.plot(x, p, '--',color = 'r', linewidth=2)
title = f"Normal Fit results: mu = {mu : .2f}, str = {std : .2f}"
plt.title(title)

plt.show()
```

![png](/assets/images/Python/52_1.png)

