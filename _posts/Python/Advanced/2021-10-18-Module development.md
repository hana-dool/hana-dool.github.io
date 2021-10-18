---
title:  "Module development"
excerpt: "Module 을 이용하여 develope 할떄의 팁"
categories:
  - Py_Advanced
last_modified_at: 2021-10-18

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"

use_math : true
---

 module 을 수정하면서 작업하는 방법에 대해서 알아봅시다.
{: .notice--warning}

# [Custom Module](#link){: .btn .btn--primary}{: .align-center}

> ## reimport module function 

- Custom module 을 만들때, py 를 수정하면서 불러오기를 반복하면서 작업하게 됩니다.
  - 이때에 module 을 계속 다시 불러오면서 작업하기 위해서는 어떻게 해야 할까요? 

```
.
└── utility/           
    ├── README.md 
    ├── __init__.py
    ├── augment.py                     # Data augmentation function
    ├── eda.py                         # EDA: Easy Data Augmentation Techniques └── main.py 
```

- 위와 같이 main 에서 작업하게 되면, 다른 파일안에 있는 py 파일에서 함수를 import 하여 사용할 수 있습니다.

```python
from utility.eda import processing
```

- 하지만 eda 의 함수를 수정하여, 다시 불러오면서 작업하고 싶다면 어떻게 해야할까요? 
  - 그럴때에는 아래와 같이 해주면 됩니다. 

```python
del sys.module[processing.__module__]
```

- 위와 같이 system 에서 processing 함수의 모듈을 삭제한 뒤 재실행 하면 됩니다.



---

**reference**

- [https://datascienceschool.net](https://datascienceschool.net/01%20python/02.15%20%ED%8C%8C%EC%9D%B4%EC%8D%AC%EC%97%90%EC%84%9C%20%EB%82%A0%EC%A7%9C%EC%99%80%20%EC%8B%9C%EA%B0%84%20%EB%8B%A4%EB%A3%A8%EA%B8%B0.html)
- <https://dojang.io/mod/page/view.php?id=2463>

