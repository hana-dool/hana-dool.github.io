---
title:  "Python Fixing Randomness"
excerpt: "파이썬에서 랜덤 픽스하기"
categories:
  - Py_Advanced
last_modified_at: 2021-11-11

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"

use_math : true
typora-root-url: ../../../../hana-dool.github.io
---

 random seed 를 고정하여 Reproductive 한 파이썬 코딩하기
{: .notice--warning}

# [Fix Seed in python](#link){: .btn .btn--primary}{: .align-center}

> ## Prepare 

```python
class config:
    seed = 42
    device = "cuda:0"    
        
    lr = 1e-3
    epochs = 25
    batch_size = 32
    num_workers = 4
```

- 위와 같이 config 라는 클래스에 우리가 미리 어떻게 Default 로 변수나 Hyperparameter 들을 설정할지에 따라서 정해놓으면, 뒤에서 이를 이용하기가 편합니다.
- 즉 위에서 값을 설정만 하고, 뒤에서는 다음과 같이 이용만 하면 됩니다.

```python
random.seed(config.seed)
```

> ## Normal

```python
import numpy as np
import random
import torch
import os

def seed_everything(seed: int = 42):
    random.seed(seed)
    np.random.seed(seed)
    os.environ["PYTHONHASHSEED"] = str(seed)

seed_everything(config.seed)
```

- 위와 같이 이용할 수 있습니다.

> ## Pytorch

```python
def seed_everything(seed: int = 42):
    random.seed(seed)
    np.random.seed(seed)
    os.environ["PYTHONHASHSEED"] = str(seed)
    torch.manual_seed(seed)
    torch.cuda.manual_seed(seed)  # type: ignore
    torch.backends.cudnn.deterministic = True  # type: ignore
    torch.backends.cudnn.benchmark = True  # type: ignore
seed_everything(config.seed)
```

> ## Tensorflow

```python
def seed_everything(seed: int = 42):
    random.seed(seed)
    np.random.seed(seed)
    os.environ["PYTHONHASHSEED"] = str(seed)
    tf.random.set_seed(seed)
seed_everything(config.seed)
```

**reference**

- <https://yganalyst.github.io/data_handling/memo_1/>

