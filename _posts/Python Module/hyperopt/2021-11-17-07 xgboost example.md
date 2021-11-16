---
title:  "Example xgboost"
excerpt: "XG boost 의 예제"
categories:
  - Py_Hyperopt
last_modified_at: 2021-11-17

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 Matplotlib 객체에 대해서 Margin을 주는 여려가지 방법에 대해서 알아보자.
{: .notice--warning}

# [Hyper Optimization](#link){: .btn .btn--primary}{: .align-center}

> ## HyperOpt

- HyperOpt는 베이지안 최적화의 접근 방식을 취합니다. 
- 베이시안 최적화는 objective function(목적 함수)를 최대/최소로 하는 최적해를 찾는 기법입니다. 목적함수와 하이퍼파라미터의 Pair를 대상으로 Surrogate Model을 만들어 평가하면서 순차적으로 업데이트 하면서 최적의 조합을 찾아 냅니다.
- 여기서 Acquisition function의 개념이 추가로 나오는데 Surrogate Model은 목적 함수에 대한 확률적인 추정을 하며, Acquisition function은 Surrogate Model이 추정한 확률적 추정 결과를 바탕으로 다음 후보를 선정하는 함수입니다.

![png](/assets/images/Python/54_1.png)

- 위처럼, 베이지안 방법을 이용해 최적화를 위한 위치 (hyperparameter) 를 배워가면서 tuning 하게 됩니다. 당연히 성능이 더 좋은것은 두말할 필요가 없겠죠?

> ## HyperOpt Example

```python
pip install hyperopt
```

- 위처럼 hyperopt 를 설치합니다.

```python
from sklearn.metrics import mean_squared_error

def RMSE(y_true, y_pred):
    return np.sqrt(mean_squared_error(y_true, y_pred))
```

- 평가함수를 정의합니다.
- 그 이후에 아래와 같이 구조를 짭니다.

```python
import hyperopt
from hyperopt import fmin, tpe, hp, STATUS_OK, Trials
from sklearn.metrics import mean_squared_error

# regularization candiate 정의
reg_candidate = [1e-5, 1e-4, 1e-3, 1e-2, 0.1, 1, 5, 10, 100]

# space 정의, Hyperparameter의 이름을 key 값으로 입력
space={'max_depth': hp.quniform("max_depth", 5, 15, 1),
       'learning_rate': hp.quniform ('learning_rate', 0.01, 0.05, 0.005),
       'reg_alpha' : hp.choice('reg_alpha', reg_candidate),
       'reg_lambda' : hp.choice('reg_lambda', reg_candidate),
       'subsample': hp.quniform('subsample', 0.6, 1, 0.05),
       'colsample_bytree' : hp.quniform('colsample_bytree', 0.6, 1, 0.05),
       'min_child_weight' : hp.quniform('min_child_weight', 1, 10, 1),
       'n_estimators': hp.quniform('n_estimators', 200, 1500, 100)
      }

# 목적 함수 정의
# n_estimators, max_depth와 같은 반드시 int 타입을 가져야 하는 hyperparamter는 int로 타입 캐스팅 합니다.
def hyperparameter_tuning(space):
    model=XGBRegressor(n_estimators =int(space['n_estimators']), 
                       max_depth = int(space['max_depth']), 
                       learning_rate = space['learning_rate'],
                       reg_alpha = space['reg_alpha'],
                       reg_lambda = space['reg_lambda'],
                       subsample = space['subsample'],
                       colsample_bytree = space['colsample_bytree'], 
                       min_child_weight = int(space['min_child_weight']),
                       random_state=SEED, 
                      )
    
    evaluation = [(x_train, y_train), (x_test, y_test)]
    
    model.fit(x_train, y_train,
              eval_set=evaluation, 
              eval_metric="rmse",
              early_stopping_rounds=20,
              verbose=0)

    pred = model.predict(x_test)
    rmse= RMSE(y_test, pred)    
    # 평가 방식 선정
    return {'loss':rmse, 'status': STATUS_OK, 'model': model}
```

- 목적 함수 정의가 완료 되었다면, fmin 함수로 최적화를 지정합니다.
- fmin 에는 다양한 옵션 값들을 지정할 수 있습니다. 지정해주는 알고리즘과 최대 반복 횟수등을 변경해 보면서 성능이 달라지는지 모니터링 합니다.

 ```python
 # Trials 객체 선언합니다.
 trials = Trials()
 # best에 최적의 하이퍼 파라미터를 return 받습니다.
 best = fmin(fn=hyperparameter_tuning,
             space=space,
             algo=tpe.suggest,
             max_evals=50, # 최대 반복 횟수를 지정합니다.
             trials=trials)
 
 # 최적화된 결과를 int로 변환해야하는 파라미터는 타입 변환을 수행합니다.
 best['max_depth'] = int(best['max_depth'])
 best['min_child_weight'] = int(best['min_child_weight'])
 best['n_estimators'] = int(best['n_estimators'])
 best['reg_alpha'] = reg_candidate[int(best['reg_alpha'])]
 best['reg_lambda'] = reg_candidate[int(best['reg_lambda'])]
 best['random_state'] = SEED
 print (best)
 # {'colsample_bytree': 0.8, 'learning_rate': 0.02, 'max_depth': 10, 'min_child_weight': 2, 'n_estimators': 700, 'reg_alpha': 1, 'reg_lambda': 0.001, 'subsample': 0.65, 'random_state': 30}
 ```

- best 변수에 담긴 튜닝된 하이퍼 파라미터를 XGBoost 알고리즘에 적용하여 예측합니다.

```python
xgb = XGBRegressor(**best)
xgb.fit(x_train, y_train)
pred = xgb.predict(x_test)
print(RMSE(y_test, pred))
# 2.2171511696118538
```

---

**Reference**

- <https://teddylee777.github.io/thoughts/hyper-opt>



