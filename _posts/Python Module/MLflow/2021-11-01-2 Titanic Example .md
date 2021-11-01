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

> ## what is mlflow? 

- MLflow 를 어떻게 사용할 수 있는지에 대해서 알아봅시다. 

```python
titanic = TitanicMain()

if is_keras:
    #ml_tf.autolog(log_models=True) # 이렇게도 저장 가능
    tf_model, model_info = titanic.run(is_keras)
    log_metrics(model_info['score'])
    log_params(model_info['params'])
    ml_keras.log_model(tf_model, 'tf_keras_model')
    print("Model saved in run %s" % mlflow.active_run().info.run_uuid)
else:
    model, model_info = titanic.run(is_keras, args.n_estimator)
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

- 위와 같이 

**Reference**

- <https://wikidocs.net/52460>
- <https://zzsza.github.io/mlops/2019/01/16/mlflow-basic/>

ing
{: .notice--success}

