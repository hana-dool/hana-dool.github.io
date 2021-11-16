---
title:  "Trials Object"
excerpt: "optimization 과정을 시각화 하여 저장하기"
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

# [Trials](#link){: .btn .btn--primary}{: .align-center}

> ## Trials

- 이제 우리는 hyperorp 라는 블랙박스에서 어떻게 최적화가 이루어지고 있는지 궁금해할 수 있을것입니다. 
- 이때 `Trial` 객체를 이용하면 이러한 블랙박스를 엿볼 수 있게 도와줍니다.

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
best = fmin(fn=f, space=fspace, algo=tpe.suggest, max_evals=50, trials=trials)
print(f'best :{best}')
print('trials:')

# 오로지 2개만 출력합니다.
for trial in trials.trials[:2]:
    print(trial)
```

- 이때 위의 trials 객체를 fmin 에 넣어서, Optimization Procedure 를 저장할 수 있습니다.

```
100%|██████████| 50/50 [00:00<00:00, 833.78trial/s, best loss: 0.0006354990350066602]
best :{'x': 0.025209106192141367}
trials:
{'state': 2, 'tid': 0, 'spec': None, 'result': {'loss': 16.515765043440087, 'status': 'ok'}, 'misc': {'tid': 0, 'cmd': ('domain_attachment', 'FMinIter_Domain'), 'workdir': None, 'idxs': {'x': [0]}, 'vals': {'x': [4.063959281715318]}}, 'exp_key': None, 'owner': None, 'version': 0, 'book_time': datetime.datetime(2021, 11, 16, 17, 35, 36, 552000), 'refresh_time': datetime.datetime(2021, 11, 16, 17, 35, 36, 552000)}
{'state': 2, 'tid': 1, 'spec': None, 'result': {'loss': 4.42367094548546, 'status': 'ok'}, 'misc': {'tid': 1, 'cmd': ('domain_attachment', 'FMinIter_Domain'), 'workdir': None, 'idxs': {'x': [1]}, 'vals': {'x': [2.103252468317929]}}, 'exp_key': None, 'owner': None, 'version': 0, 'book_time': datetime.datetime(2021, 11, 16, 17, 35, 36, 553000), 'refresh_time': datetime.datetime(2021, 11, 16, 17, 35, 36, 553000)}
```

- 이때 Trials 가 가지는 Attributes 는 다음과 같습니다. 

> ## Attributes

> `trials.trials` 

- a list of dictionaries representing everything about the search
  - 어떤것을 Search 했는지에 대해서 알려줍니다.

```python
trials.trials
```

```
[{'state': 2,
  'tid': 0,
  'spec': None,
  'result': {'loss': 16.515765043440087, 'status': 'ok'},
  'misc': {'tid': 0,
   'cmd': ('domain_attachment', 'FMinIter_Domain'),
   'workdir': None,
   'idxs': {'x': [0]},
   'vals': {'x': [4.063959281715318]}},
  'exp_key': None,
  'owner': None,
  'version': 0,
  'book_time': datetime.datetime(2021, 11, 16, 17, 35, 36, 552000),
  'refresh_time': datetime.datetime(2021, 11, 16, 17, 35, 36, 552000)},
...........
```

- 위의 trial object 가 가지는 대표적인 값은 다음과 같습니다. 

```
['spec'] - the specification of hyper-parameters for a job
['result'] - the result of Domain.evaluate(). Typically includes:
['status'] - one of the STATUS_STRINGS
['loss'] - real-valued scalar that hyperopt is trying to minimize
['idxs'] - compressed representation of spec
['vals'] - compressed representation of spec
['tid'] - trial id (unique in Trials list)
```

> `trials.results` 

- a list of dictionaries returned by 'objective' during the search
  - 즉 objective 가 죄는 값 (주로 loss) 의 리스트를 출력합니다. 

```python
trials.results
```

```
[{'loss': 16.515765043440087, 'status': 'ok'},
 {'loss': 4.42367094548546, 'status': 'ok'},
 {'loss': 3.2956862852556097, 'status': 'ok'},
 {'loss': 22.14665994599703, 'status': 'ok'},
 {'loss': 4.991205356411717, 'status': 'ok'},
 {'loss': 17.418325083695798, 'status': 'ok'},
 {'loss': 8.109085998211324, 'status': 'ok'},
 {'loss': 23.936946919503015, 'status': 'ok'},
...........
```

> `trials.losses()`

- a list of losses (float for each 'ok' trial)
  - 로스만 출력합니다. 

```python
trials.losses()
```

```
[16.515765043440087,
 4.42367094548546,
 3.2956862852556097,
 22.14665994599703,
 4.991205356411717,
 17.418325083695798,
 8.109085998211324,
 23.936946919503015,
 14.30668945589039,
 14.410712722617223,
 ............
```

> `trials.statuses()`

- a list of status strings

```python
trials.statuses()
```

```
['ok',
 'ok',
 'ok',
 'ok',
 'ok',
 'ok',
 'ok',
......
```

---

**Reference**

- <https://medium.com/district-data-labs/parameter-tuning-with-hyperopt-faa86acdfdce>
- <http://hyperopt.github.io/hyperopt/getting-started/search_spaces/>







