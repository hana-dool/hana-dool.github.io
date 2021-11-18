---
title:  "Terminal (ZSH)"
excerpt: "맥의 터미널(ZSH)과, 그와 관련된 명령어"
categories:
  - OtherTools
last_modified_at: 2021-11-18

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 터미널은 어떤 명령어를 사용할까요
{: .notice--warning}

# [Terminal 이란?](#link){: .btn .btn--primary}{: .align-center}

> ## 운영체제와 커널

![png](/assets/images/Program/1_1.png)

- 운영체제는 컴퓨터 사용자와 컴퓨터 하드웨어 간의 인터페이스로서 동작하는 시스템 소프트웨어의 일종으로, 다른 응용프로그램이 유용한 작업을 할 수 있도록 환경을 제공해 줍니다.
- 컴퓨터와 전원을 켜면 운영체제는 이와 동시에 수행된다. 한편 소프트웨어가 컴퓨터 시스템에서 수행되기 위해서는 메모리에 그 프로그램이 올라가 있어야 한다. 
- 마찬가지로 운영체제 자체도 소프트웨어로서 전원이 켜짐과 동시에 메모리에 올라가야 한다. 하지만, 운영체제처럼 규모가 큰 프로그램이 모두 메모리에 올라간다면 한정된 메모리 공간의 낭비가 심할것이다. 따라서 운영체제 중 **항상 필요한 부분**만을 전원이 켜짐과 동시에 메모리에 올려놓고 그렇지 않은 부분은 필요할 때 메모리에 올려서 사용하게 된다. 
- 이 때 **메모리에 상주하는 운영체제의 부분을 커널**이라 한다. 또 이것을 좁은 의미의 운영체제라고도 한다. 즉 커널은 메모리에 상주하는 부분으로써 운영체제의 핵심적인 부분을 뜻한다. 
- 이에 반에 넓은 의미의 운영체제는 커널뿐 아니라 각종 시스템을 위한 유틸리티들을 광범위하게 포함하는 개념이다. (보통은 운영체제라고 하면 커널을 말하게 된다.)

> ## 셸(Shell) 이란? 

- 운영체제에서 커널과 이용자 사이에 끼어서 이용자의 명령을 해석하고 그 처리 결과를 뿌려주는 시스템 프로그램. 

![png](/assets/images/Program/1_2.png)

- Shell의 사전적 의미인 조개/소라 껍데기에서 따온 말로 내부의 커널이 있고 사용자는 이를 감싸고 있는 껍데기를 통해 커널에 접근한다는 개념으로 컴퓨터 초창기인 60년대부터 사용된 단어이다.
- 이때 커널 과 운영체제가 궁금할 수 있는데요 차근차근 알아봅시다. 

> ## 셸의 기능

1. 사용자와 커널 사이에서 명령을 해석해 전달하는 **명령어 해석기 기능** 

2. 셸은 자체 내에 **프로그래밍 기능**이 있어서 프로그램을 작성할 수 있습니다. 셸 프로그래밍 기능을 이용하면 여러 명령을 사용해 반복적으로 수행하는 작업을 하나의 프로그램으로 제작 할 수 있습니다. 셸 프로그램을 셸 스크립트라고 불러요

3. **사용자 환경 설정의 기능** - 초기화 파일 기능을 이용해 사용자의 환경을 설정할 수 있습니다. 로그인 할 때 이 초기화 파일이 실행되서 사용자의 초기 환경이 설정돼요. 셸을 공부하는데 가장 중요한 것 중 하나가 환경변수의 이해입니다.

> ## 종류

- 셸은 흔히 두 종류로 구분하는데, 명령 줄 셸과 그래픽 셸이다. 전자는 [CLI](https://namu.wiki/w/CLI)이고 후자는 [GUI](https://namu.wiki/w/GUI)라 부른다. CLI는 때때로 CUI(character 또는 console user interface)라고 부르기도 한다.
- 즉 정리하면 (GUI : 그래픽 사용자 인터페이스 / CLI : 명령 줄 인터페이스(텍스트)) 라고 이해하시면 됩니다.

![png](/assets/images/Program/1_4.png)

- 위처럼 Finder 도 대표적인 GUI 라고 할 수 있습니다!
- 이때 셸의 종류를 저수준에서, 바라보게 된다면 아래와 같습니다.

![png](/assets/images/Program/1_3.png)

- 셸은 커널에서 분리된 별도의 프로그램이어서 다양한 종류의 셸이 존재하고 현재까지도 지속적으로 개발되고 있습니다.
- (개발된 순서는 다음과 같습니다 : 본쉘 → C쉘 → tcsh → ksh → bash쉘)
  - 이후에 다루게 될 zsh 도 

> ## Z Shell (zsh)

- zsh 는 bash, ksh, tcsh의 일부 기능을 포함하여 수많은 개선 사항이 갖추어진 확장형 본 셸이다.
- 현재 맥의 기본 Shell 이며, 다양한 기능이 추가되어있고, 간편한 점이 많아서 웬만하면 zsh 를 사용하는것을 추천드립니다. 
- Zshell 의 주요 특징
  1. 실행 중인 모든 Shell은 명령어의 history를 쉘 끼리 공유합니다.
  2. 간단한 설정을 통해 문법 오류를 정정해줍니다. (e.g. `gut` → `git`)
  3. 다양한 테마를 지원합니다.

# [Terminal 기타 명령어](#link){: .btn .btn--primary}{: .align-center}

> ## pwd : 현제 어디 디렉토리 있는지 표시

- 제가 위치하는 디렉토리의 경로를 표시해줍니다. 

```python
gorany@goranys-MacBook-Air ~ % pwd
/Users/gorany
```

> ## ls : 현재 디렉토리 안의 파일을 보여줌

- 지금 제가 위치하고 있는 디렉토리 안의 파일을 모두 출력합니다.

```
gorany@goranys-MacBook-Air ~ % ls  
Applications	Documents	Library		Music		Public
Desktop		Downloads	Movies		Pictures	seaborn-data
```

> ## touch : 파일 생성하기

- 파일( 폴더가 아닙니다!) 을 만들어 줍니다. 

```
gorany@goranys-MacBook-Air R % touch haha.png
```

- 위와 같이 실행하면 haha 라는 png 를 생성하게 됩니다.

> ## mkdir : 폴더 생성

- 폴더를 생성하는 명령어입니다.

```
gorany@goranys-MacBook-Air R % mkdir new_dir 
```

- "web" 폴더(Directory)를 현제 경로에 생성합니다.

# [cd : 이동](#link){: .btn .btn--primary}{: .align-center}

> ## cd [경로] : 경로로 이동 

- 저희가 원하는 경로로 이동하게 해 줍니다.

```
gorany@goranys-MacBook-Air ~ % cd Desktop
gorany@goranys-MacBook-Air Desktop % 
```

> ## cd / : 최상위 폴더로 돌아가기

- 최상위 폴더로 바로 돌아갈 수 있습니다.

```
gorany@goranys-MacBook-Air Desktop % cd /
gorany@goranys-MacBook-Air / % 
```

> ## cd ../ : 상위 폴더로 돌아가기

- 위처럼 실행하면, 상위 폴더로 돌아갈 수 있게됩니다.

```
gorany@goranys-MacBook-Air R % cd ../
gorany@goranys-MacBook-Air Desktop % 
```

# [mv : 파일 옮기기 및 변경](#link){: .btn .btn--primary}{: .align-center}

> ## mv : 파일 이동 

```
mv ./aa.pdf /Users/mainmac/Downloads/
```

- 현재 폴더의 aa.pdf 파일을 Downloads 폴더로 이동

> ## mv : 파일 이름 변경

- 기본적으로 `mv A B` : 는 A 를 $\to$ B 의 이름으로 바꾸게 됩니다.

```
gorany@goranys-MacBook-Air R % mv new1.py old.py
```

- 위와 같이 실행할 경우 new1.py $\to$ old.py 로 이름을 바꾸게 됩니다. 

> ## mv A Folder/ : A 를 폴더로 이동

- A 파일을 폴더로 이동할때 쓰입니다.

```
gorany@goranys-MacBook-Air R % mv p.py 기러기/ 
```

- p.py 라는 파이썬 파일을 기러기 폴더로 옮깁니다. 

> ## mv *.txt Folder/ : txt 확장자를 모두 폴더로 이동

- 특정한 확장자를 가지는 파일을 모~두 폴더로 옮깁니다. 

```
gorany@goranys-MacBook-Air R % mv *.py 기러기/
```

- py 파일을 모두 기러기에 옮깁니다. 

# [cp : 복사 및 덮어쓰기](#link){: .btn .btn--primary}{: .align-center}

> ##  cp A B :  A 를 B 로 파일 복사

- 파일을 복사합니다. (즉 원본은 그대로입니다.)

```
gorany@goranys-MacBook-Air R % cp haha.png hoho.png
```

- 위는 haha.png $\to$ hoho.pnh 로 복사합니다.

> ## cp A folder/ : A 를 folder 로 복사

- 파일을 복사하여 옮깁니다. (원본은 그대루)

```
gorany@goranys-MacBook-Air R % cp haha.png temp/
```

- 위와 같이 실행하면 temp 로 haha 가 이동합니다. 

# [rm : 파일 삭제](#link){: .btn .btn--primary}{: .align-center}

> ## rm : 파일 삭제 

- 파일을 삭제합니다.
  - 이때 주의해야할점은 directory 는 삭제할 수 없다는 것입니다. 

```
gorany@goranys-MacBook-Air R % rmdir new.py
```

- 위와 같이 실행시 new.py 를 삭제할 수 있습니다. 

```
gorany@goranys-MacBook-Air R % rm tempdir
rm: tempdir: is a directory
```

- 위처럼 directory 를 삭제할 경우에, 폴더의 삭제를 거부하고 있습니다.

> ## rmdir : (비어있는) 폴더 삭제

- 비어있는 폴더를 삭제합니다. 
  - 하지만 주의하셔야 될 점은, 폴더가 비어있을때가 한정이기 때문에, 폴더 안에 파일이 있을 경우에는 삭제하지 않습니다.

```
gorany@goranys-MacBook-Air R % rmdir tempdir
```

- 위의 경우는 폴더가 비어있어서 잘 작동하고 있습니다. 

```
gorany@goranys-MacBook-Air R % rmdir tempdir
rmdir: tempdir: Directory not empty
```

> ## rm -r [디렉토리]

- 데렉토리를 삭제합니다. 이때에는 안에 어떤게 차있어도 삭제됩니다.

```
gorany@goranys-MacBook-Air R % rm 기러기
```

- 기러기 라는 이름을 가지는 폴더를 삭제합니다.

---

**Reference**

- <https://mentha2.tistory.com/211>
- <https://jhnyang.tistory.com/57>
- <https://byebyeblue.tistory.com/5>
- <https://wiseworld.tistory.com/47>
- <https://jh-make.tistory.com/category/%EB%A7%A5%20%ED%84%B0%EB%AF%B8%EB%84%90%20%EB%AA%85%EB%A0%B9%EC%96%B4>
  - 요기가 짱인것 같아요. 더 알고싶으면 여기를 보도록 합시다.








힘들어...
{: .notice--success}

