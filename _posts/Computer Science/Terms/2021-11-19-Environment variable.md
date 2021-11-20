---
title:  "Environment variable"
excerpt: "환경 변수란?"
categories:
  - Terms
last_modified_at: 2021-11-19

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true

---

 환경 변수에 대해서 정리해 봅시다!! 맥은 왜이렇게 귀찮은거에요 도대체가...
{: .notice--warning}

# [Environment Variable](#link){: .btn .btn--primary}{: .align-center}

> ## 환경 변수의 필요성

- 리눅스도 그렇고 이런 CMD도 마찬가지지만 이런 텍스트 기반 환경은 모든 행동들을 **명령어**를 통해 이루어집니다.
  - 예를 들어 현재 나의 위치(디렉터리 경로)를 c:\내문서 로 이동해라 라든지 현재 위치에 있는 notepad 프로그램을 실행해라 라든지 등이 그것입니다.
- 우리가 사용하는 Windows 도 보여지는 것은 그래피컬하지만 더블클릭 등으로 경로를 이동하면 내부적으로는 명령어들이 실행된다고 생각하면 조금 더 이해가 가실겁니다.
- 경로 이동의 경우 cd 명령어(change directory) 를 사용하는데 이러한 기본 명령어들은 기본적으로 내장되어 있는 내장 명령어 들입니다.
  - 때문에 운영체제만 설치하면 기본적으로 명령어를 이용할 수 있습니다.
- 그러나 우리가 설치한 응용 프로그램들은 어떻게 실행할 수 있을까요? 
  - 간단하게 cmd를 실행하고 프로그램의 이름을 입력하면 다음과 같은 말이 뜰 것입니다.

```
프로그램은(는) 내부 또는 외부 명령, 실행할 수 있는 프로그램, 또는  배치 파일이 아닙니다
```

- 이는 우리가 실행하고자 하는 프로그램을 찾아서 실행할 수 없다는 것입니다.
- 즉 컴퓨터가 우리 프로그램을 잘 찾아 실행할 수 있게 Path 변수에 프로그램이 있는 bin 디렉터리를 잡아주게 되면 운영체제는 다음과 같이 행동합니다.

1. python 을 입력 후 엔터를 누릅니다. 

2. 운영체제는 python 라는 내부 명령어가 있는지 검사합니다.

3. 없는 경우 Path 환경변수를 검색합니다.

4. Path에 설정된 경로들 (; 세미콜론으로 구분된)을 모두 검사합니다.

5. python.exe를 발견하면 실행합니다.

> 환경 변수의 사전적 정의

- 환경 변수란 프로세스가 컴퓨터에서 동작하는 방식에 영향을 미치는, 동적인 값들의 모임이다. OS(ex) 윈도우, 리눅스 등)의 **환경변수는 시스템의 실행 파일이 놓여 있는 디렉터리의 지정 등 OS 상세서 동작하는 응용소프트웨어가 참조하기 위한 설정이 기록**된다.
- 응용소프트웨어는 시스템콜(system call)이나 OS의 표준 API 등을 통하여 간단히 값을 얻을수록 되어있다. 쉽게 이야기해서 각자 깊숙이 있는 응용프로그램을 쉽게 꺼내쓰기 위해서 미리 변수로 등록해 놓는 것을 말한다.

> ## 시스템 변수와 환경변수

- 시스템변수내에 사용자 변수가 들어있다.
- 시스템변수에 변수를 지정해 놓으면 사용자에 상관없이 변수값을 이용할수있고
- 사용자변수에 넣어놓으면 해당 사용자계정만 변수를 사용할수 있다.

> ## 환경변수의 지정

- **she="my love"** 처럼 프로그래밍을 하게 된다면, she 라는 변수에 my love 라는 문장을 매핑한 것입니다.
- 여기에서 변수에 환경이란 말을 더하여 콘솔에서의 '환경변수'를 절대적으로 정한다고 한다면 터미널에 그저 **'export'**를 앞에 갖다 붙히기만 하면 되게 됩니다.

```
// 환경변수를 지정한다.
root@test:~$ export she="my love"

// 지정된 환경변수를 불러온다.
root@test:~$ echo $she
my love
-> 'she'에 대한 환경변수가 출력 되는데 성공했다.
```

- 위처럼 환경변수를 입력하는게 가능합니다.
- 하지만 위와 같은 단순한 지정은 열려있는 터미널에서만 지속되며, 다른 터미널 콘솔에서는 변수로 지정되지 않습니다.
- 그렇다면 이러한 설정이 계속 유지되도록 하면 어떻게 해야될까요? 

```
// 먼저 만일을 대비해서 bashrc의 백업을 만든다. (물론 부팅시를 기준으로 한 백업 파일인 '$HOME/.bashrc~'가 존재 한다.) 
root@test:~$ cp ~/.bashrc ~/.bashrc.bak

// .bashrc 파일에 추가할 환경변수를 삽입 한다.
root@test:~$ echo 'export she="my love"' >> ~/.bashrc

// 재부팅 할 필요 없이 '~/.bashrc' 파일의 소스를 로드한다.
root@test:~$ source ~/.bashrc

// 지정된 환경변수를 불러온다.
root@test:~$ echo $she
my love
-> 'she'에 대한 환경변수가 출력 되는데 성공했다.
```

# [Environment 관리](#link){: .btn .btn--primary}{: .align-center}

> ## 모든 환경변수 확인

- 터미널에서 printenv 입력

```
gorany@goranys-MacBook-Air / % printenv
TERM_PROGRAM=Apple_Terminal
SHELL=/bin/zsh
TERM=xterm-256color
......
```

> ## 특정 환경 변수값 확인

- 터미널에서 echo $환경변수명 입력

```
userMacBookPro:~ username$ echo $TERM_PROGRAM
Apple_Terminal
```

# [Environment 설정](#link){: .btn .btn--primary}{: .align-center}

> ## 임시 환경변수

- 터미널에서 export 새임시환경변수명=새임시환경변수값 을 실행하면 됩니다.

```
userMacBookPro:~ username$ export ENVIRONMENT_VARIABLE=value
```

> ## 유저 환경변수

- 리눅스,맥 환경변수 설정은 ~/.bash_profile 에 설정합니다.
- 기본적으로 유저 홈에 .bash_profile이 존재하며 터미널을 처음 실행시켰을때 기본 위치는 유저홈 입니다.
- 터미널을 열고 아래 명령어를 실행하세요

```
$ vi ~/.bash_profile
```

- 첫 테스트로 아래와 같이 입력한후 저장합니다.

```
export TEST = "first test"
```

- reboot 하거나 터미널을 새로 열지 않는다면 환경변수는 바로 적용되지 않습니다.
- 하지만 아래 명령어로 현재 shell에 바로 적용할수 있습니다.

```
$ source ./bash_profile
```

- 방금 입력한 TEST 변수가 잘 작동되는지 검사해봅시다

```
$ echo $TEST
```

```
gorany@goranys-Air ~ $ source ./bash_profile
gorany@goranys-Air ~ $ source $TEST
first test
```

- 잘 실행되었다면 두번째 스텝으로 변수를 복합적으로 적어봅니다.

```
export TEST="first test"
export TEST2=$TEST"second test"
```

- 저장후에 아래 명령어들로 어떤 결과가 나오는지 확인합니다.

```
$ source ./bash_profile 
$ echo $TEST 
>> first test
$ echo $TEST2
>> first testsecond test
```

> ## 전역 환경변수

- 지금까지 작성했던 ~/.bash_profile 설정은 각 유저별로 적용이 됩니다.
- 만약 모든 유저가 사용할 환경 변수(전역 환경변수)를 지정하고싶다면 /etc/profile 을 수정해야합니다.

```
$ vi /etc/profile
```

- 작성후에 이전에 실행한것처럼 아래 명령어를 실행합니다.

```
$ source /etc/profile
```

- 나머지는 그대로 위와 같이하시면 됩니다.

# [PATH 에 추가 및 확인](#link){: .btn .btn--primary}{: .align-center}

> ## 새로운 PATH 에 디렉터리 추가하기

- 우리가 새로운 프로그램을 설치할떄 , 그 위치 (디렉토리) 를 환경변수로 추가하고 싶을 것입니다.
- 그럴떄에 다음과 같은 방식을 사용합니다. 

```
PATH=/추가할 경로1:/추가할 경로2:/경로 3:$PATH
```

- 기존의 `$PATH` 값에 새로운 디렉터리를 추가할 때 위와 같은 방식을 사용합니다.

- =(등호) 왼편에는 변수명(대문자), 오른편에는 변숫값을 적어줍니다. 이때 등호 양 옆에는 공백이 있으면 안 됩니다.

- 추가되는 디렉렉터리는 : (쌍점, 콜론)으로 구분합니다. 즉 ::(쌍점, 콜론)이 굽ㄴ자 역할을 하는 것이지요.

- 또한 기존의 `$PATH`값은 `$PATH`를 붙여줌으로써 유지해줍니다. 
- 만약 이 `$PATH`가 붙지 않는다면 기존 `$PATH`값이 유지되지 않습니다.

> ## 환경변수 확인

```
echo $PATH
```

- 터미널에 echo `$PATH`를 실행하면 현재 등록되어 있는 환경 변수 `$PATH`값을 확인할 수 있습니다

> ## 영구적인 경로 추가

```
export PATH=/추가할 경로1:/추가할 경로2:/경로3:$PATH
```

> ## Tip : 환경설정 백업하기

- 늘 환경변수를 추가하거나 수정할 경우, 이상하게 추가하면 다 꼬이므로 백업하는것을 추천합니다.

```
study@study-VirtualBox:~$ cp ~/.bashrc ~/.bashrc.bak
# 환경설정 파일을 백업!
```

# [Procedure](#link){: .btn .btn--primary}{: .align-center}

- 위에서 본 것들을 총 집합하여, 어떻게 하면 환경변수를 추가하는지 알아봅시다.

> ## Procedure

> 1.터미널을 실행합니다.

> 2.bash_profile 이 있는지 확인하고 없으면 만들어줍니다. 

-  터미널에서 아래를 입력하여 .bash_profile 파일이 있는지 확인하고 있으신 분들은 다음단계로 넘어가시면 됩니다. 

  ```
  ls 
  ```

- 없으신 분들은

 ```
 touch .bash_profile
 ```

- 를 입력하여 .bash_profile 파일을 직접 생성합니다.

> 3.bash_profile 파일을 열어서 경로를 추가한 뒤 저장합니다

```
open .bash_profile
```

- 위를 입력하여 .bash_profile 파일을 에디터로 엽니다
-  열린 에디터에 다음과 같이 경로를 추가합니다.
  -   *export PATH=${PATH}:(추가할 경로)*
  -   *예) export PATH=${PATH}:~/Downloads/flutter/bin*
- Note : 왜 위와 같이 추가하나요?
  - 환경변수를 새로 등록하거나 편집하는 명령어는 **export PATH=새로 등록할 프로그램의 주소**이다.
  - 그런데 한가지 주의해야 할 점은 위의 명령어처럼 바로 해버리면 **기존 환경변수에 덮어쓰기**가 된다는 점이다.
  - 따라서 기존 환경변수에 이어서 새 환경변수를 등록하기 위한 명령어는 **export PATH=$PATH:새로 등록할 프로그램의 주소** 를 사용한다.

> 4.source .bash_profile을 입력하여 변경된 .bash_profile 파일을 적용합니다 

- 근데 위는 bash 를 사용할때의 예시로, zsh 를 사용한다면 `source ~/.zshrc` 를 쓰도록 합시다. (?)
  - 이 명령어는 설정을 다시 불러온다는것을 의미합니다.

```
source .bash_profile 
```

> 5.환경 변수가 잘 적용되었는지 확인합니다.

```
echo $PATH
```

> ## Example 1 

- JAVA 의 설치 예시

```
vi ~/.bash_profile  //vi 에디터로 해당 디렉토리를 연다.
 
 
// i를 누르고 ---INSERT--- 뜬다면 입력할수 있다. 이 두가지를 입력하자.
export JAVA_HOME=/Library/Java/JavaVirtualMachines/[jdk 설치 버전].jdk/Contents/Home
export PATH=${PATH}:$JAVA_HOME/bin
 
// 이후 ESC를 누른후 :wq 로 에디터를 빠져나오자
:wq
 
// vi에디터가 종료된후의 원경로에서 입력해준다
source ~/.bash_profile
```

- 위에서 설치 위치는 /Library/Java/JavaVirtualMachines/[jdk 설치 버전].jdk/Contents/Home 입니다. 
- 즉 .bash_profile 에서, JAVA_HOME 이라는 변수에, 자바가 깔린 위치를 지정한 뒤 `export PATH=${PATH}:$JAVA_HOME/bin` 에서는, 그 위치의 상위 위치인 bin 으로 path 를 지정해주는 작업을 했다는것을 알 수 있습니다.

---

**Reference**

- <https://dololak.tistory.com/20>
- <https://velog.io/@psj0810/%ED%99%98%EA%B2%BD%EB%B3%80%EC%88%98%EB%9E%80>
- <https://life-of-panda.tistory.com/41>
- <https://wnw1005.tistory.com/264>
- <https://hymndev.tistory.com/5>
- <https://whitepaek.tistory.com/28>





