---
title:  "Framework Comparison"
excerpt: "Python Bayesian Framework 를 비교해보기"
categories:
  - Py_Pymc
last_modified_at: 2021-10-23
toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 주력을 파이썬으로 사용하는 만큼 Bayesian Frame work를 알아볼떄도 되도록이면 파이썬을 찾아보려고 했습니다. 대부분의 서술은 https://m.blog.naver.com/PostList.naver?blogId=2feelus (IDEO) 님이 너무 정리를 잘해놓으셔서, 이 블로그를 그대로 옮긴것이므로 여기를 참고하시면 좋을것 같습니다.
{: .notice--warning}

# [Probabilistic Programming](#link){: .btn .btn--primary}{: .align-center}

> ##  결정론적 프로그래밍과 확률론적 프로그래밍

- 일반적인 소프트웨어 프로그래밍은 어떠한 함수가 실행되면 그 출력값이 동일한것을 전제로 한다. 
- 이러한 식으로 프로그램을 작성하는것을 결정론적(Deterministic) 프로그래밍이라고 한다. 
  - 이런 결정론적 프로그래밍이 소프트웨어서는 일반적이다.
- 그런데 실제 세상에서는 이렇게 입력과 출력이 항상 기대한대로 동작 하지는 않는다. 
  - 예를 들어 날씨 예보를 떠 올려봐도 내일 비가 올것인지를 명시적으로 판단할수는 없다. 
  - 단지 우리는 확률적으로 내일 비가 올 확률이 몇%인지를 예측할 뿐이다. 
- 이런 식의 예측성 함수를 작성할때는 비가 올만한 단서들을 잘 추려내어 통계적인 기법으로 예측을 해내게 되는데, 이를 일반적인 프로그래밍적인 방법으로 구현 하기는 매우 어렵다. 

- 이런 예측성 문제들을 함수로 구현해 내려면 예측값을 추론하기 위한 수학적 과정들이 필요하다. 
  - 이런 수학적 과정으로는 통계적 가설수립, 확률 분포 모형 함수생성, 데이터 시뮬레이션을 통한 통계적 추론 , 데이터 샘플링, 확률분포간의 비교과정등이 있다. 
  - 또한 이러한 확률적 프로그래밍 방법에는 컴퓨팅 자원도 많이 필요해 OS와 프레임워크수준에서 CPU병렬처리나 GPU등의 사용도 효과적으로 지원도 되어야 한다.

- 위 처럼 다양한 추론 과정들을 쉽고 효율적으로 작성하도록 도와주는 프로그래밍 방법을 Probabilistic Programming이라고 한다.

> ## Probabilistic Programming frameworks 특징

> 확률 변수의 범용성

- 확률적 파라미터 
  - Probabilistic Programming의 특징중 하나는 함수의 파라미터로 확률적 변수(stochastic variables)를 전달할수 있다는 점이다. 
  - 확률변수는 확률분포함수로 나타낼수 있으며 다른 확률분포함수와 연산이 가능하다. 이것이 왜 확률론적 프로그래밍이라고 불리는 이유라고 볼수 있다.

> recursion지원 여부

- 확률기반 함수가 자신을 다시 호출하는 경우, 프레임웍에 따라 Recursion이 지원되지 않는 단점이 있다.

> 추론 알고리즘

- 샘플링 (Sampling) 추론 방법
  - 데이터를 적절하게 추출해내어 확률 분포함수를 추론하는 방법으로 HMC, NUTS등이 있다. 
- 변분추론(Variational Inference)방법
  - 샘플을 뽑아낼 필요없이, 추론문제를 Transform이라는 방식을 통해 최적화방식으로 변형하여 확률분포추론을 하는 방법이다.

> 백엔드

- 대부분의 구현체들이 GPU를 적극적으로 활용하기 위해 기존의 딥러닝 프레임워크들을 백엔드로 사용하고 있다.
- 행렬 연산을 위한 Computational Graph
  - 대부분의 통계및 확률론적 연산은 linear Algebra(선형대수)를 근간으로 하며 결국 확률연산은 배열 혹은  Tensor라고 불리는 고차원 배열간의 \+ - / * 연산들을 통해 이루어진다. 
  - 이 계산은 자원을 많이 소모하는 과정이며 머신러닝 프레임웍들은 효율화와 분산처리등을 위해 Computational Graph라는 개념으로 관리한다.

- 자동 미분
  - differentiation, autograd , gradient decent등으로 불리는 자동 미분을 통한 최적화방식을 제공하고 있다.
- 종류
  - Tensorflow, PyTorch, Theano등이 많이 사용되는 백엔드이다. 본인에게 익숙한 백엔드가 좋을수 있다.
  - Tensoflow와 Theano는 Computational Graph를 정적으로 세팅한후 한번에 컴파일하여 실행되는 방식이다. 
    - 그래서 행렬 연산이 즉시 일어나지 않고, lazy하게 실행된다.
  - PyTorch는 Dynamic하게 Computational Graph를 생성한다. 그래서 즉시 행렬 연산이 수행된다. 
  - 디버깅시에 PyTorch가 유리하지만 빌드속도및 최적화 성능은 Static Computational Graph계열등이 좋다. 
    - 2018년 현재는 텐서플로우에서도 배열의 즉시 연산이 가능하다.

# [Frameworks](#link){: .btn .btn--primary}{: .align-center}

> ##  1.Stan (https://mc-stan.org/)

- 언어: R, Python
- 확률함수내 Recursion : 지원
- Sampling Inference: HMC, NUTS지원
- Variational Inference: ADVI지원
- 백엔드: 없음
- 특징:최초의 Probabilistic Programming 방식이다. MCMC, HMC등의 샘플링 추론이 잘 지원된다. 
- 문서화:문서화가 잘되어있는 장점이 있다. (R 테스트 링크 - https://rstudio.cloud/project/56157 )
- 문법: R기반 Stan 자체문법. 단순하고 표현성이 좋다.아래와 같이 확률분포 모형을 기술할수 있다.
- GPU: X
- 장점: 응용사례풍부, 샘플링 추론에 강점
- 장래성: 통계분야의 프로토타입은 R에서 출발하기에 신규 기능 프로토타이핑에 좋다.

> ## 2.PyMC3 (https://docs.pymc.io/)

- 언어: Python
- 확률함수내 Recursion : 미지원
- Sampling Inference: 처음에는 Sampling Inference만 지원했다. 그래서 이름에 MC(Monte Carlo)가 붙어있다. 하지만 요즘은 다양한 방법 (HMC,NUTS)이 지원된다.(사용하기 쉽다)
- Variational Inference: automatic differentiation variational inference (ADVI) and operator variational inference (OPVI)
- 백엔드: theano
- 특징: 대단위 데이터를 사용한 샘플링 통계추론에 강하다. 응용사례풍부, 유저커뮤니티
- 문서화 : stan만큼 문서화가 잘되어있지는 않다. 
- 문법: stan에 비해서는 syntax가 좀더 매끄럽지는 않은 면이 있다.
- GPU: O
- 장점: 응용사례풍부, 샘플링 추론에 강점
- 단점: Theano의 지원이 약화되면서 차후 다른 DL 프레임워크에 포팅되어야 할것으로 보인다.

> ## 3.Edwards (http://edwardlib.org/tutorials/)

- 언어 : Python
- 확률함수내 Recursion : 미지원
- Sampling Inference:Monte Carlo 시뮬레이션이 지원됨
- Variational Inference: 주로 내세우는 장점. 추론간의 조합이 가능하다.
- 백엔드 : Tensorflow
- 특징: 성능평가(criticism)가 지원된다. 텐서플로우를 사용하기 때문에 프로덕션레벨에서 볼때는 분산환경에서 가장 빠른 성능을 낼것으로 보인다. 
- Tensorflow session기반이기 때문에 디버깅은 어렵다.
- 문법: Tensorflow를 사용하기때문에 좀 Verbose하다.
- 문서화: 문서화가 가장 안되어있는 편이다. 
- GPU: O
- 장점: 텐서플로우 커뮤니티에 힘입어 기대할만한 성장세. 학습성능 빠르다. 변분추론에 강세
- 단점: 아직 API나 문서화가 풍부하지 않은 편

> ## 4.Pyro (https://docs.pyro.ai/en/stable/)

- 언어 : Python
- 확률함수내 Recursion : 지원
- Sampling Inference: MCMC/NUTS/HMC지원
- Variational Inference: AVDI, ELBO 지원, 추론 조합 쉽다.
- 백엔드: PyTorch
- 특징: 디버깅에 좋다. Uber에 내놓음. 
- 문법: 표현성이 좋은편이다. 
- 문서화: 잘되어있는 편이다. 주피터 노트북예제가 git 워크스페이스안에 잘 준비되어있다.
- GPU: O
- 장점: 디버깅 용이성 높아 당장 개발해보기가 용이하다. 확률함수 Recursion지원으로 보편성 높다, 변분추론에 강세
- 단점: 아직 많이 성숙하지는 않은 프레임웍.

> ## Comparison

- 최근 트렌드인 Variational Inference는 데이터가 적은 경우에 유리하다. 이런 경우에는 Pyro나 Edwards가 좀더 유리할것으로 보인다. 
- 확률함수내에서 자체적으로 recursion이 필요한 경우 Pyro가 자연스럽게 지원되고, PyMC3나 Edwards에서는 다른 트릭들을 써야 한다.
- 전통적인 MCMC계열의 Sampling 추론은 PyMC3나 Stan이 응용사례가 많아 더 안정적일 듯 하다.

- 옛날 Pymc 사이트이지만 개념이나 설명이 잘 되어있음

> ## Conclusion

- 우선 제일 범용적으로 쓰이는 Pymc 를 사용하기로 결정
  - 물론 이미 개발이 중지된 Theano 를 사용하는점은 아쉽다.
  - 하지만 여전히 다양한 분야에서 잘 사용되고 있고 꾸준히 업데이트 되고 있다는점
  - 그리고 문서화가 그나마 다른것들에 비해서 어느정도 되어있다는 점에 비추어 Pymc 를 먼저 공부하기로 결정하였습니다. 
- Done ! 

---

**Reference**

- <https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=2feelus&logNo=221435835604>
