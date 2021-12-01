---
title: "ML Flow with Titanic Example" 
excerpt: "ML flow 실습하기"
categories:
  - Py_mlflow

last_modified_at: 2021-11-01
date : 2021-11-01 12:00:00 +0900

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

MLflow 를 실제 코드와 함께 알아봅시다. from <https://github.com/lsjsj92/python_mlflow_example>
{: .notice--warning}

# [ML Flow](#link){: .btn .btn--primary}{: .align-center}

> ## ML flow 사용법

- MLflow 를 어떻게 사용할 수 있는지에 대해서 알아봅시다. 

```
(base) C:\Users\goran\Desktop\Python\mlflow>tree /f
```

- 우선 위와 같은 경로에 lsjsj92 님의 파일을 모두 옮겨 놓았습니다. 
- 그 결과는 아래와 같습니다.

```
C:.
│  .gitignore
│  config.py
│  dataio.py
│  main.py
│  ml_experiment.py
│  model.py
│  predict.py
│  preprocess.py
│  README.md
│  titanic.py
│
└─mlflow-env
        conda.yaml
        config.py
        dataio.py
        main.py
        MLproject
        model.py
        preprocess.py
        titanic.py
```

> ## main.py

- main.py 에서는 MLflow  와 함께 전체 코드를 실행하는 main 을 담당하게 됩니다.

```python
import argparse
import sys

import mlflow
from mlflow import sklearn as ml_sklearn
from mlflow import keras as ml_keras
from mlflow import log_artifacts
from mlflow import log_metric, log_metrics
from mlflow import log_param, log_params


from titanic import TitanicMain


def _str2bool(v):
    if isinstance(v, bool):
        return v
    if v.lower() in ('yes', 'true', 't', 'y', '1'):
        return True
    elif v.lower() in ('no', 'false', 'f', 'n', '0'):
        return False
    else:
        raise argparse.ArgumentTypeError('Boolean value expected.')

def start(is_keras, n_estimator):
    mlflow.set_experiment('soojin')
    
    titanic = TitanicMain()

    if is_keras:
        #ml_tf.autolog(log_models=True) # 이렇게도 저장 가능
        tf_model, model_info = titanic.run(is_keras)
        log_metrics(model_info['score'])
        log_params(model_info['params'])
        ml_keras.log_model(tf_model, 'tf_keras_model')
        print("Model saved in run %s" % mlflow.active_run().info.run_uuid)
    else:
        model, model_info = titanic.run(is_keras, n_estimator)
        '''log metric을 하나하나 등록할 때는 아래와 같이 진행
            #log_metric("rf_score", score_info['rf_model_score'])
            #log_metric("lgbm_score", score_info['lgbm_model_score'])
        '''
        # metrics를 한 번에 등록 -> json 형태가 되어야 함
        log_metrics(model_info['score'])
        log_params(model_info['params'])
        ml_sklearn.log_model(model, 'ml_model')
        print("Model saved in run %s" % mlflow.active_run().info.run_uuid)


if __name__ == "__main__":
    
    argument_parser = argparse.ArgumentParser()

    argument_parser.add_argument(
        '--is_keras', type=str,
        help="please input 1 or 0"
    )
    argument_parser.add_argument(
        '--n_estimator', type=int, default=100
    )

    args = argument_parser.parse_args()
    try:
        is_keras = _str2bool(args.is_keras)
    except argparse.ArgumentTypeError as E:
        print("ERROR!! please input is_keras 0 or 1")
        sys.exit()

    start(is_keras, args.n_estimator)
```

- 이 때에 main.py 에서는 model.py 에서 넘어온 model 정보를 받아서 mlflow 에서 제공하는 log_metric , log_param, log_model 등에 정보를 주입합니다.
  - 그 뒤로 위에서 설정한 정보들이 출력할 수 있게 합니다. 
- 이제 위에서 main 이 어떻게 구성되어있는지에 대해서 살펴보도록 합시다.

> import module

```python
from mlflow import sklearn as ml_sklearn
from mlflow import keras as ml_keras
from mlflow import log_artifacts
from mlflow import log_metric, log_metrics
from mlflow import log_param, log_params
```

- 위에서 처럼 mlfloe 에서 다양한 모듈들이 업데이트 되고 있습니다. 
  - 여기에서 

> ## model.py

- model.py 에서는 텐서플로우 (2.X) 의 딥러닝 모델과 사이킷렁 (Sklearn) 라이브러리의 머신 러닝 모델을 가지고 데이터를 훈련하게 됩니다. 
- 그리고 training 된 모델과 model 의 하이퍼 파라미터 정보를 main.py 에 return 해줍니다.

```python
import sys

import numpy as np
from sklearn.ensemble import RandomForestClassifier
#from lightgbm import LGBMClassifier

from tensorflow.keras.layers import Dense, Dropout, Input
from tensorflow.keras.models import Model


class TitanicModeling:
    def __init__(self):
        pass

    def run_sklearn_modeling(self, X, y, n_estimator):
        model = self._get_rf_model(n_estimator)
        #lgbm_model = self._get_lgbm_model(n_estimator)

        model.fit(X, y)
        #lgbm_model.fit(X, y)

        model_info = {
            'score' : {'model_score' :  model.score(X, y)},
            'params' : model.get_params()
        	}

        return model, model_info

    def run_keras_modeling(self, X, y):
        model = self._get_keras_model()
        model.fit(X, y, epochs=20, batch_size=10)
        #predictions = model.predict(X)
        #print('keras prediction : ', predictions[:5])

        model_info = {'score' : {'model_score' :  np.float64(  round(model.evaluate(X, y)[1], 2))}
                      ,'params' : {'epochs':20, 'batch_size':10}}

        return model, model_info

    def _get_rf_model(self, n_estimator):
        return RandomForestClassifier(n_estimators=n_estimator, max_depth=5)

    #def _get_lgbm_model(self, n_estimator):
    #    return LGBMClassifier(n_estimators=n_estimator)

    def _get_keras_model(self):
        inp = Input(shape=(3, ), name='inp_layer')
        dense_layer_1 = Dense(32, activation='relu', name="dense_1")
        dense_layer_2 = Dense(16, activation='relu', name="dense_2")
        predict_layer = Dense(1, activation = 'sigmoid', name='predict_layer')

        dense_vector_1 = dense_layer_1(inp)
        dense_vector_2 = dense_layer_2(dense_vector_1)
        predict_vector = predict_layer(dense_vector_2)

        model = Model(inputs=inp, outputs=predict_vector)
        model.compile(loss = 'binary_crossentropy', optimizer='adam', metrics=['acc'])
        return model
```

- Training 된 모델되 이 model 의 하이퍼 파라미터 정보를 main.py 에서 return 합니다. 
- run_sklearn_modeling 함수가 어떻게 정의되었는지에 대해서 살펴봅시다. 

```python
def run_sklearn_modeling(self, X, y, n_estimator):
    model = self._get_rf_model(n_estimator)
    #lgbm_model = self._get_lgbm_model(n_estimator)

    model.fit(X, y)
    #lgbm_model.fit(X, y)

    model_info = {
        'score' : {'model_score' :  model.score(X, y)},
        'params' : model.get_params()
    }

    return model, model_info
```

- 보이시나요? Dictionary 를 return 하는데, fitting 한 model 과 model 정보인 model_info 를 출력하고 있습니다.
  - 이떄에 각각의 info 는 아래의 main.py 에서 다음과 같이 전달된다는것을 기억합시다! 

```python
    if is_keras:
        #ml_tf.autolog(log_models=True) # 이렇게도 저장 가능
        tf_model, model_info = titanic.run(is_keras)
        log_metrics(model_info['score'])
        log_params(model_info['params'])
        ml_keras.log_model(tf_model, 'tf_keras_model')
        print("Model saved in run %s" % mlflow.active_run().info.run_uuid)
    else:
        model, model_info = titanic.run(is_keras, n_estimator)
        '''log metric을 하나하나 등록할 때는 아래와 같이 진행
            #log_metric("rf_score", score_info['rf_model_score'])
            #log_metric("lgbm_score", score_info['lgbm_model_score'])
        '''
        # metrics를 한 번에 등록 -> json 형태가 되어야 함
        log_metrics(model_info['score'])
        log_params(model_info['params'])
        ml_sklearn.log_model(model, 'ml_model')
        print("Model saved in run %s" % mlflow.active_run().info.run_uuid)
```

- 즉! main 에서 훈련을 시키고 나서 나온 결과를 String 으로 반환해주면 된다는 것입니다. 
  - 또는 model 을 전달해주기도 합니다. 

> ## MLFLow - Tracking

- 이 떄에 ML flow 는 다음과 같은 값들을 받을 수 있습니다
- log_metric (혹은 log_metrics)
  - 머신러닝 혹은 딥러닝 모델의 metric(평가 지표)를 logging
  - metric이라고 하면 정확도(accuarcy), f1-score, precision, recall 등임
- log_param(혹은 log_params)
  - 모델에서 사용되는 파라미터 값을 저장
  - log_param은 하나하나 저장할 때 사용하며 json 형태로 한 번에 저장하고 싶으면 log_params를 사용
- log_model
  - machine learnnig model이나 deep learnnig model을 저장
  - 본 포스팅에서는 tensorflow2.X keras 딥러닝 모델과 scikit-learn의 머신러닝 모델을 저장함

> ## 실행



**Reference**

- <https://wikidocs.net/52460>
- <https://zzsza.github.io/mlops/2019/01/16/mlflow-basic/>

ing
{: .notice--success}

