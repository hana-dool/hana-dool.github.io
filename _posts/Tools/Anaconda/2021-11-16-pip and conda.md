---
title:  "Pip and Conda and install Rule"
excerpt: "Anaconda 를 이용해서 패키지 관리를하자"
categories:
  - Anaconda
last_modified_at: 2021-11-16

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 패키지를 관리하기 위한 두가지 (Conda 와 Pip) 방법과 차이점에 대해서 좀 자세하게 알아봅시다.
{: .notice--warning}

# [Python Packages Tools](#link){: .btn .btn--primary}{: .align-center}

> ## pip vs pip3

- 터미널에서 다음과 같이 명령어를 치면 `pip`와 `pip2`, `pip3` 가 실제로 어디에 설치되어있는지 알 수 있다.

 ```
 $ ls -l `which pip`
 -rwxrwxr-x  1 heumsi  staff  234  3 26 18:25 /Users/heumsi/anaconda3/bin/pip
 $ ls -l `which pip2`
 lrwxr-xr-x  1 heumsi  admin  34  5 13 19:49 /usr/local/bin/pip2 -> ../Cellar/python@2/2.7.16/bin/pip2
 $ ls -l `which pip3`
 lrwxr-xr-x  1 heumsi  admin  33  3 19 20:49 /usr/local/bin/pip3 -> ../Cellar/python/3.7.2_2/bin/pip3
 ```

- 위를 살펴보자. 
  - `pip` : Anaconda 3 에서 관리하는 전역 pip
  - `pip2` : local 내에 깔린 pip2 (python2 버젼)
  - `pip3` : local 내에 깔린 pip3 (python3 버젼)

> ## pip install

- anaconda 로 다음과 같은 가상 환경을 만든 후, 들어갔다고 해보자.

```
$ conda create -n py36 python=3.6  
...  
$ source activate py36  
$ (py36) ~
```

- 이렇게 진입한 콘다 가상환경 안에서 pip 명령어의 차이를 보면,

```
$ ls -l `which pip`
-rwxrwxr-x  1 heumsi  staff  244  3 26 18:27 /Users/heumsi/anaconda3/envs/py36/bin/pip
$ ls -l `which pip2`
lrwxr-xr-x  1 heumsi  admin  34  5 13 19:49 /usr/local/bin/pip2 -> ../Cellar/python@2/2.7.16/bin/pip2
$ ls -l `which pip3`
lrwxr-xr-x  1 heumsi  admin  33  3 19 20:49 /usr/local/bin/pip3 -> ../Cellar/python/3.7.2_2/bin/pip3
```

- 이번엔 `pip` 입력한 경우, 이전과 다르게 `py36` 환경의 `pip`에 깔리는 것을 알 수 있다.
  한편, `pip2` 와 `pip3` 는 이전과 동일하게 **local pip** 에 들어가게되는 것을 알 수 있다.

- 즉, 가상환경 내에서만 패키지를 설치하려면, 그냥 `pip install ~` 만 해야한다.
  (혹여나 헷갈려서 `pip3 install` 로 하게되면, 그냥 전역 local에 깔리는 것이다)

> ## conda install vs pip install

- conda install 은 현재 가상환경에만 패키지를 설치한다. pip도 동일하다. 예를 들어,

```
$ (py36) conda env list  

# conda environments:  
#  
base                      /Users/heumsi/anaconda3  
py36                  *   /Users/heumsi/anaconda3/envs/py36
```

- 현재 가상환경은 py36 이고, 이 상태에서 아래와 같이 입력하면,

```
$ (py36) conda install jupyter
```

- Py36 에만 jupyter 가 설치되고, 그 외 다른 환경(여기서는 base) 에는 설치되지 않는다.
- 즉, 일반적으로 원하는 패키지를 현재 환경에만 설치하기 위해, `conda install` 로 하나 `pip install` 로 하나 상관없다.

# [Then.. Pip or Conda?](#link){: .btn .btn--primary}{: .align-center}

> ## conda 를 쓰세요

- 아나콘다에서는 pip 보다 conda 로 패키지를 관리하는 편이 좋은데요 그 이유를 살펴보겠습니다. 

> conda 가 pip보다 패키지 의존성을 더 잘 관리해 준다.

- 애초에 conda 로 설치하게 되면, 운영체제나 플랫폼에 맞추어 이미 빌드된 패키지가 깔리기 때문에 서로간의 충돌이나 의존성 이슈가 없습니다. 
- 하지만 pip 에서는 미리 관리되고, 빌드된 패키지가 아니라 소스 패키지가 내려와서 가끔 에러가 발생하는 경우가 있습니다. 

> conda 와 pip 을 섞어쓰면 서로 제어가 안됩니다.

- pip 이후에 conda 를 실행하면 pip 을 통해 설치된 패키지를 덮어쓰고 손상시킬 수 있습니다.
  - 마찬가지로 conda 이후에 pip 을 실행한다하더라도 마찬가지 입니다. 
- 이럴 경우에는 서로 안정성이 검증되지 못한 상태에서 패키지들이 깔리기때문에 문제가 될 수 있습니다 ! 

> Conda 는 버전관리를 잘 해준다.

- conda 패키지는 어떤 한 패키지를 업그레이드 또는 다운그레이드 하면, 해당 버전에 따라 의존되는 패키지까지 같이 업그레이드 다운그레이드를 해 준다.
- conda update --all 같은 명령을 내리면, 해당 가상환경에 깔린 모든 패키지를 한꺼번에 최신으로 올려주기까지 한다.

> ## conda 에 없어요.. 

- 그러나 여전히 아나콘다 환경에서 pip 로 패키지 설치를 하라는 튜토리얼이나 강좌가 많이 습니다.
- 한가지 이유는 conda 패키지는 미리 빌드된 패키지를 만들고 패키지 의존성까지 맞추기 때문에, pip의 pypi 서버만큼 빨리 최신버전이 올라오지 않습니다. 그래서 tensorflow 의 아주 최신 버전이 pip 로는 설치가 되는데, conda 로는 설치가 안되는 상황이 발생하기도 하고, 이런 때에는 부득이 pip 로 설치해야 할 것이다. 
- 하지만, 부득이 pip 로 어떤 패키지를 설치하게 되면, 이후에 conda update나 conda install, uninstall 등으로 패키지를 변경할 경우에 pip 로 설치되었던 패키지는 업데이트에서 누락이 되거나, 다른 버전이 두가지가 깔려있는 것처럼 보이거나 하는 경우가 발생할 수 있으니 주의해야 합니다.

> ## conda-forge 를 하는게 어때? 

- conda forge 는 conda channel 에서 설치한다는 것입니다.
  - 이때 conda channel 은 뭘까요? 
- 아래와 같이 아나콘다의 가상환경 설정을 볼 수 있습니다.

> Conda Channel 이란? 

```
--------------

environment.yaml <= 환경설정 파일로 .yaml 이라는 확장자를 사용하는 파일입니다.

--------------
name: post
channels:
  - default
  - conda-forge
dependencies:
  - python=3.8
--------------
```

- Anaconda Inc.에서 관리 하는 Anaconda Cloud 의 기본 채널 외에도 패키지를 설치할 수있는 다른 채널이 있는데요. 
- 인기있는 채널은 커뮤니티 주도 패키지 컬렉션을 포함하는 conda-forge 입니다. 
- 아래가 conda-forge 페이지인데요. 아래 저장소에 가면 conda-forge 저장소에 있는 패키지를 보실 수 있습니다
  - [conda-forge :: Anaconda.org](https://anaconda.org/conda-forge)
- conda chnnel은 패키지들이 저장되어있는 위치이다. 패키지들을 호스팅하고 관리하기 위한 방법으로 사용됩니다. 

> **`-c conda-forge`**  의 뜻

- `-c` 는 --channel 과 같은 의미입니다.
- conda-forge 는 conda-forge 의 체널에서 설치하겠다는 의미겠지요! 
- 그러므로 -c conda-forge 를 이용하여 설치하면, 기존 체널에 없던 패키지를 설치할 수 있습니다. 

> conda-forge 의 장점!

1. 패키지들이 더 최신 버전일 가능성이 높다.
2. 패키지 수가 더 많다.
3. openblas로 의존성 관리 하는 것이 좋다. (defaults는 mkl)
4. C extension, C wrapper 패키지 같은 컴파일된 라이브러리가 필요한 패키지들을 설치할 때 호환성이 안맞을 가능성을 낮춰준다.

# [Conclusion](#link){: .btn .btn--primary}{: .align-center}

> ## Anaconda 설치 원칙

- 그러므로 아래와 같은 개발 원칙을 가지는게 좋을것입니다. 

1. conda install 로 설치해본다.
2. conda install -c conda-forge 명령으로 설치해 본다.
3. 인터넷에서 anaconda + 패키지명 으로 검색하여, anaconda.org 사이트 페이지가 검색되면, 검색페이지에서 소개하는 채널을 이용하여 conda install -c <channal> 명령으로 설치한다.
4. 위 모든 것이 실패하였을 때에, pip install 한다.
   - pip install 시 디펜던시로 설치된 패키지들 중에 conda install 이 가능한 패키지가 있다면, pip uninstall 한 후에 conda install 로 다시 설치한다.

> ## 가상환경 이용!

- 그리고 base 는 작업용으로 사용하지 않고, 작업용으로는 반드시 conda create 로 새로운 가상환경을 만들어 사용한다. 
- 패키지끼리 충돌이 발생하였을 때에 테스트도 용이하고, 특정 패키지의 버전차이 테스트도 가능하고, 불가피하게 충돌되는 두가지 환경을 분리하여 작업환경을 설치할 수 있다.

---

**Reference**

- <https://dailyheumsi.tistory.com/33>
- <https://daewonyoon.tistory.com/359>
- <https://www.anaconda.com/blog/using-pip-in-a-conda-environment>
- <https://velog.io/@prayme/conda%EB%9E%80>





