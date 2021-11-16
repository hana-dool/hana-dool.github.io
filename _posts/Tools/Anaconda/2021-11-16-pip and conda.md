---
title:  "Pip and Conda"
excerpt: "pip install 과 conda install 의 차이"
categories:
  - Others
last_modified_at: 2021-11-16

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 패키지를 관리하기 위한 두가지 (Conda 와 Pip) 방법과 차이점?
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

---

**Reference**

- <https://dailyheumsi.tistory.com/33>

