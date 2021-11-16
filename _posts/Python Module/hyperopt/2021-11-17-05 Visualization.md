---
title:  "Visualization"
excerpt: "Hyperparameter 를 시각화 하는법"
categories:
  - Py_Hyperopt
last_modified_at: 2021-11-17

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 어떻게 하면 최적화 할 수 있을지에 대해서 정말정말 쉬운 예제를 통해서 알아봅시다.
{: .notice--warning}

# [Visualization](#link){: .btn .btn--primary}{: .align-center}

- 우선 아래와 같이 기본적인 경우를 생각해봅시다.

```python
from hyperopt import fmin, tpe, hp, STATUS_OK, Trials
fspace = {
    'x': hp.uniform('x', -5, 5)
}
def f(params):
    x = params['x']
    val = x**2
    return {'loss': val, 'status': STATUS_OK}
trials = Trials()
best = fmin(fn=f, space=fspace, algo=tpe.suggest, max_evals=1000, trials=trials)
```

> ## Visualization with Time

- 위에 대해서 Optimization 과정을 어떻게 시각화 할 수 있을까요? 

```python
import matplotlib.pyplot as plt
f, ax = plt.subplots(1)
xs = [t['tid'] for t in trials.trials]
ys = [t['misc']['vals']['x'] for t in trials.trials]
ax.set_xlim(xs[0]-10, xs[-1]+10)
ax.scatter(xs, ys, s=20, linewidth=0.01, alpha=0.75)
ax.set_title('$x$ $vs$ $t$ ', fontsize=18)
ax.set_xlabel('$t$', fontsize=16)
ax.set_ylabel('$x$', fontsize=16)
```

![png](/assets/images/Python/56_1.png)

- 위와 같이 시간(t) 에 따라서 변수 ($x$) 가 어떻게 변하는지를 살펴볼 수 있습니다.

> ## loss vs parameter

- 파라미터와 Loss 에 대해서 시각화를 할 수도 있습니다.

```python
f, ax = plt.subplots(1)
xs = [t['misc']['vals']['x'] for t in trials.trials]
ys = [t['result']['loss'] for t in trials.trials]
ax.scatter(xs, ys, s=20, linewidth=0.01, alpha=0.75)
ax.set_title('$val$ $vs$ $x$ ', fontsize=18)
ax.set_xlabel('$x$', fontsize=16)
ax.set_ylabel('$val$', fontsize=16)
```

![png](/assets/images/Python/56_2.png)

---

**Reference**

- <https://medium.com/district-data-labs/parameter-tuning-with-hyperopt-faa86acdfdce>
- <http://hyperopt.github.io/hyperopt/getting-started/search_spaces/>







