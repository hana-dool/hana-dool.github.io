---
title:  "Computer System Overview"
excerpt: "컴퓨터 시스템 오버뷰"
categories:
  - Operating_System
last_modified_at: 2021-11-21

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 통계를 하게되면 확률에 대한 두가지 관점인 베이지안과 Frequentist 두가지 관점에 대해서 배우게 됩니다. 두개의 차이에 대해서 짧게 알아보도록 합니다. 
{: .notice--warning}

# [Computer System Overview](#link){: .btn .btn--primary}{: .align-center}

> ## overview

- 게임을 하게 되더라도 우리는 엄청나게 많은것들이 필요합니다.
  - CPU , GPU , SSD , LAN ..... 
- 위의 구성 요소들을 효율적으로 활용할 수 있게 관리하는 OS(operating system) 이 필요하게 됩니다. 

> operating system

- 컴퓨팅 시스템 자원 (Hard ware) 를 효율적으로 관리하여 사용자에게 서비스를 제공하는 소프트웨어를 운영체제라고 할 수 있습니다. 

> ## Computer hardware

- 컴퓨터 하드웨어는 크게 3가지로 나눌 수 있습니다.

> 프로세서 (Peocessor)

- 쉽게 말해서 계산하는 장치입니다. 
- CPU, GPU , 처리장치 등 

> 메모리 (Memory)

- 어떤것을 저장하는 장치입니다.
- Disk, SSD ....

> 주변장치

- 키보드 , 마우스, 모니터 등이라 할 수 있습니다 .

# [프로세서](#link){: .btn .btn--primary}{: .align-center}

> ## 프로세서

- 컴퓨터의 두뇌 (중앙처리 장치 ) 로서, 컴퓨터의 모든 장치의 동작을 제어하게 됩니다.

![png](/assets/images/Program/11_1.png)

- 장치 안을 들여다 보면 연산 , 제어 하는 장치가 있는데요, 이때 레지스터는 어떤것일까요? 

> ## 레지스터

- 프로세서 내부에 있는 메모리입니다. (프로세서가 사용할 데이터를 저장)
- 컴퓨터에서 가장 빠른 메모리입니다. 
- 레지스터는 다양한 종류가 있습니다. 
  - 용도에 따른 분류 
    - 전용 레지스터 : 정해진 용도가 있는 레지스터
    - 범용 레지스터 : 일반적인 목적으로 사용되는 레지스터
  - 사용자가 변경 가능한지에 따른 분류 
    - 사용자 가시 레지스터 : 바꿀 수 있음
    - 사용자 불가시 레지스터 
  - 저장하는 정보의 종류에 따른 분류
    - 데이터 레지스터 : 함수 연산에 필요한 데이터 저장 
    - 주소 레지스터 : 주소, 유효 주소 등을 저장
    - 상태 레지스터

> 프로세서의 동작

- 실제로 연산할때에는 다양한 레지스터를 통해서 연산이 됩니다. 

> 운영체제와 프로세서

- 운영체제제가 프로세서에게 시키는 일은 다음과 같습니다.
  - 프로세서에게 작업을 할당하고 관리
  - 프로그램이 프로세서를 계속 쓰면 안되니까 사용시간을 관리

# [메모리](#link){: .btn .btn--primary}{: .align-center}

- 데이터를 저장하는 장치 (기억장치) 
  - 프로그램, 사용자 데이터 등을 저장합니다.

![png](/assets/images/Program/11_2.png)

- 레지스터 
- 캐시 : CPU
- 메인메모리 : DRAM (RAM)
- 보조기억장치 : HDD

> ## 메모리의 종류 : 주 기억장치 (Main mamory)

- 프로세서가 수행할 프로그램과 데이터를 저장합니다.
  - 프로세서가 어떤 프로그램을 돌리려고 한다면, 이 램에 프로그램과 데이터를 올려야 합니다.

![png](/assets/images/Program/11_3.png)

- 그런데 왜 굳이 디스크에서 램으로 올려서 그것을 프로세서가 관리할까요? 
  - 즉 왜 디스크에서 바로 프로세서에 올려서 프로그램을 관리하지 않을까요?
- 이는 위의 그래프를 보면 디스크의 스피드에 비해서 CPU 의 속도는 엄청 빠른것을 볼 수 있습니다.
  - 그러므로 이러한 갭을 좀 줄이기 위하여, 중간에 속도가 빠른 메인메모리(램) 을 놓아서 병목현상을 줄이고자 한 것입니다. 

> ## 메모리의 종류 : 캐시 (cash)

- 레지스터와 마찬가지로 CPU 안에 들어있습니다.

![png](/assets/images/Program/11_4.png)

- 이 역시, 메인 메모리와 CPU 사이에 여전히 스피드 갭이 있어서 캐시를 사용합니다.
  - 램과 같은 이유이죠. 

![png](/assets/images/Program/11_5.png)

- 그런데 위의 캐시 데이터를 보면 너무나 크기가 작습니다. (128kb???)
  - 이것만으로 병목현상을 해소할 수 있을까요? 

> 캐시의 동작

![png](/assets/images/Program/11_6.png)

- 캐시는 일반적으로 hardware (CPU) 가 알아서 관리함
- 프로세서가 일을 하다보면 데이터가 필요할 것입니다. 
  - 만일 메인 메모리의 파란색 사각형의 데이터가 필요하다고 합시다.
- 프로세서는 캐시에게 데이터가 있냐고 묻습니다. 
  - (Cache miss) 없으면 캐시가 메인 메모리에서 데이터를 가져와다가 프로세서에게 전달해줍니다.
    - 데이터가 없는 경우를 캐시 미스라 합ㅈ니다.
  - (Cache hit) 잇으면 캐시는 프로세서에게 그대로 배달해줍니다. 
    - 데이터가 있는 경우를 캐시 히트 라 합니다.
- 캐시에 데이터가 없으면 큰 손해가 될 것입니다.
  - 메인 메모리 $\to$ 캐시 $\to$ 프로세서 (시간 많이 듦)
- 캐시가 과연 효과를 낼 수 있을까요?

> 캐시와 지역성 (Locality)

- 공간적 지역성 (Spatial locality)
  - 어떤 주소를 참조 하면, 다음번에는 이 주소 근처를 참조할 확률이 높은 특성을 공간적 지역성이라 합니다.
  - 프로그램은 대게 순차적으로 진행되므로, 인접한 주소를 참조하는 확률이 높을것입니다.
- 시간적 지역성 (Temporal locality)
  - 한번 참조한 주소를 다시 참조할 확률이 높다는 것입니다. 
  - 이는 for 문을 생각하면 알 수 있습니다. 이전에 참조한것을 다시 참조할 확률이 높겠죠.
- 위와 같은 지역성 덕분에 캐시 적중률 (Cache hit ratio) 가 크다는것을 알 수 있습니다. 

> 캐시의 최적화

- 위의 행동은 어짜피 하드웨어가 한다고 했는데 왜 이렇게 캐시의 최적화를 배우는 것일까요? 

![png](/assets/images/Program/11_7.png)

- 일반적으로 캐시는 위와 같이 블록으로 메모리를 들고옵니다. 즉 

![png](/assets/images/Program/11_8.png)

- 위와 같이 격자의 값들을 모두 더하는 프로그램을 짠다고 한다면, 우리는 어떤 프로그램을 선택해야 할까요? 
  - 바로 '가로' 로 읽어내는 A 알고리즘이 캐시가 히트날 확률이 높기때문에 A 를 선택하는것이 좋을것입니다. 
- 이러한 차이는 10~100 배의 성능차이까지 날 수 있습니다.

> ## 메모리의 종류 : 보조기억장치

- 프로그램과 데이터를 저장합니다. ( HDD, CD, USB...)
- 프로세서가 직접 접근할수는 없습니다. (그래서 주변장치라고도 함)
  - 주 기억장치를 거쳐서 접근합니다.
- 하지만 만일 프로그램의 데이터가 20GB 인데 RAM 은 8GB 라 합니다. 이때에는 어떻게 사용할 수 있을까요?
  - 이때에는 가상 메모리를 사용하는데요, 이는 하드디스크의 일부를 가상메모리로사용합니다. (뒤에 자세히 알아봅시다.)

# [시스템 버스](#link){: .btn .btn--primary}{: .align-center}

> ## 시스템 버스란?

![png](/assets/images/Program/11_9.png)

- 많은 하드웨어들이(리소스) 서로 일을 하려면 통신이 필요할 것입니다.
  - 이러한 데이터및 신호를 주고받는 물리적인 통로를 시스템 버스라고 합니다. 
- 데이터 버스 : 데이터를 나르는 통로
- 주소 버스 : 주소를 나르는 통로
- 제어 버스 : 제어신호를 나르는 통로

> ## 예시

![png](/assets/images/Program/11_10.png)

1. PC 는 MAR (메모리 주소 레지스터) 에게 주소 전달 $\to$ MAR 은 주소를 주소 버스로 전달 $\to$ 그리고 그 주소는 메모리 (맨 오른쪽) 으로 전달
2. PC 는 제어장치에게 제어 신호를 전달 $\to$ 제어장치는 제어버스로 신호 전달 $\to$ 메모리로 전달
3. 메모리는 게산된 데이터를 데이터 버스에 전달 $\to$ MBR ( 메모리 버퍼 레지스터 )에 전달...

- 위와 같이 주소,데이터,제어신호 들이 버스를 타고 왔다갔다 합니다.

# [주변장치](#link){: .btn .btn--primary}{: .align-center}

> ## 종류

- 프로세서와 메모리를 제외한 하드웨어 (꼭 없어도 됨)
- 입력장치 (키보드, 마우스)
- 출력장치 (화면 , 스피커)
- 저장장치 (USB , CD)

> ## 주변장치와 운영체제

- 이때 주변장치도 결국 운영체제가 필요합니다.
- 운영체제가 하는일은 다음과 같습니다 .

>  장치 드라이버 관리

- 하드웨어를 사용할 수 있도록 인터페이스를 제공합니다.
- OS 는 이러한 인터페이스(드라이버) 를 가지고 제어할 수 있게 됩니다. 

> 인터럽트 (Interrupt) 처리

- 주변장치가 신호 (키보드의 입력 등 )이 들어왔을때 처리합니다.

> 파일 및 디스크 관리

- 파일 생성 및 삭제
- 디스크 공간 관리 등

---

**Reference**

- <https://www.youtube.com/watch?v=EdTtGv9w2sA&list=PLBrGAFAIyf5rby7QylRc6JxU5lzQ9c4tN&index=3>

