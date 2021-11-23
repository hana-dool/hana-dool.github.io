---
title:  "OS overview"
excerpt: "운영체제에 대한 오버뷰"
categories:
  - Operating_System
last_modified_at: 2021-11-21

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

 운영체제에 대해서 알아봅시다.
{: .notice--warning}

# [OS System의 역할](#link){: .btn .btn--primary}{: .align-center}

> ## 운영체제의 역할

![png](/assets/images/Program/12_1.png)

- 운영체제는 위와 같이 컴퓨터 시스템 자원 (Hardware)을 효율적으로 관리하여 사용자 , 프로그램에게 서비스를 제공합니다. 
- 이때 운영체제가 하는 역할은 다음과 같이 분류할 수 있습니다.

> User Interface (편리성) 

- 사용자가 시스템을 편하게 이용할 수 있도록 인터페이스를 제공하는 역할
- CUI (Character user interface)
  - 시스템이 문자를 기반으로 사용자가 입력하고, 받아보는 경우
  - 과거에는, 거의 모든 시스템이 이러한 구현이였습니다.
- GUI (Graphical User interface)
  - 그림형태로 되어있는 유저 인터페이스 
- EUCI (End-User Comfortable Interface)
  - 특별한 목적을 통해서 만들어진 인터페이스 (특화됨)
  - MP3 가 간단히 음악을 실행하고 재생목록에 넣을 수 잇도록 특화된 SO

> Resource management (효율성)

- 리소스를 잘 관리하여 효율적으로 프로그램을 돌리는 역할
  - HW resource (processor, memory, I/O devices, Etc.)
  - SW resource (file, application, message, signal, Etc.)

> Process and Thread management

- 프로세스 , 쓰레드를 관리합니다. (자세한것은 나중에)

> System management

- 시스템을 보호하는 역할 (시스템이 손상되지 않게)

> ## 컴퓨터 시스템의 구성

![png](/assets/images/Program/12_2.png)

- 하드웨어 위에 OS (색으로 칠해져 있는 중간 부분) 가 존재합니다.
  - 하드웨어를 관리하게 됩니다.
- 그리고 그 위에 Application 이 존재하게 됩니다.

> System call interface

- 사용자가 커널을 직접 Access 하면 , 커널을 마음대로 조작할 수 있어서 문제가 발생합니다. 
- 그래서 커널을 바로 조작하는게 아니라 필요한 기능이 있으면 OS 에게 요청하게 됩니다.
  - 이때 커널과의 통로가 되는게 System call interface 입니다. 
- 그 밖에 자세한것은 나중에 차차 알아봅시다.

> ## 운영체제의 구분

> 동시 사용자 수

- 운영체제를 혼자쓰는지, 여러명이 쓰는지 입니다.
  - 대부분의 운영체제 (window pc 등) 는 혼자씁니다. 
- Single-user system 
  - 한명의  사용자만 시스템 사용 가능 
  - 개인용 장비 (PC , 모바일) 등에 사용
  - Windows 7/10, android ....
- Multi-user system
  - 동시에 여러 사용자들이 시스템 사용
  - 기본적으로 Multi-tasking 기능이 필요하고, OS 의 기능 / 구조가 복잡함
  - 서버 클러스터 장비 등에 사용

> 동시 실행 프로세스 수

- Single-tasking system 
  - 한번에 하나의 프로세스만 존재
  - 여러개의 프로그램을 쓰려면 이전의 프로그램을 삭제하고 다음 프로그램을 실행해야함
  - 요즘에는 거의 없음... (너무 구림)
- Multi-tasking system (Multiprogramming system)
  - 여러개의 프로세스를 한번에 수행 가능
  - 작업들간의 동기화, 작업스케쥴 등을 관리해야합니다. 

> 작업 수행 방식 (사용자가 느끼는 사용 환경)

- Batch processing system
- Time-sharing system
- Distributed processing system
- Real-time system

# [OS System 의 구분](#link){: .btn .btn--primary}{: .align-center}

> ## 순차처리 (~1940) 

- 운영체제 개념이 존재하지 않음
  - 사용자가 기계어로 직접 프로그램을 작성해야함
  - 사용자가  컴퓨터 작업에 필요한 모든 과정을 지정해주어야합니다.
    - 계산 대상 / 결과 저장 위치 / 출력시점 ..... 
- 실행하는 작업 별로 순차적으로 처리 
  - 차례를 기다리면서 순서대로 실행되므로 준비시간이 필요함
  - 예시로 Python $\to$ C $\to$ Java ... 순으로 프로그램 순서가 있으면 각 프로그램 실행시 언어패키지도 준비되어야함

> ## Batch Systems (1950~1960)

![png](/assets/images/Program/13_1.png)

- 서로 다른 작업을 처리하는게 너무 힘들더라! 
  - 그러므로 각각 비슷한 성격을 지닌 작업을 모아서 처리하자는 아이디어
  - C , Python , Java 로 쓰여진 프로그램을 같이 모아서 처리하면 실행시간이 줄어들것!
- 모든 시스템을 중앙에서 처리 및 운영

> 장점

- 많은 사용자가 자원을 공유
- 처리 효율이 향상 

> 단점

- 생산정의 저하 (내가 제출한 프로그램이 언제 실행되는지 모름)
- 긴 응답시간 (작업 제출 $\to$ 결과 출력까지의 시간이 오래걸림)

> ## Time Sharing Systems (1960 ~ 1970)

![png](/assets/images/Program/13_2.png)

- 시간을 나누어서 각각 프로그램에 분할하여 활용
- 여러 사용자가 자원을 동시에 사용
  - OS 가 파일 시스템 및 가상 메모리 관리
- 사용자 지향적임 
  - 대화형 시스템

![png](/assets/images/Program/13_3.png)

- 사용자는 각각의 터미널을 통해 접속한 이후 사용자의 input 을 중앙으로 보냄
  - 이를 operator 가 관리하며 프로그램 수행

> 장점

- 응답시간의 단축
- 생산성이 향상됨 (프로세서를 나눠서 쓰니까 프로세서가 쉬지않고 일함)

> 단점

- 통신 비용 증가 (시스템에 접속해야함)
- 동시 사용자 수 $\uparrow$ $\to$ 시스템 부하 $\uparrow$ $\to$ 느려짐(개인 관점에서)

> ## Personal Computing

- 개인이 시스템 전체 독점
- 중앙으로 관리시 CPU 를 쉬지않고 돌리는게 목적이였으나 (CPU 는 비쌋으므로), 개인이 혼자 쓰는 경우 고려의 대상이 아닙니다.
- CPU 를 고려하지 않아도 되니까 OS 가 상대적으로 단순해짐.

> 장점

- 빠른 응답시간.

> 단점

- 성능이 안좋음

> ## Parallel Processing System

- 이전에 '성능' 이슈를 해결하기 위해 단일 시스템 내에서 두개 이상의 프로세서를 사용
  - 동시에 둘 이상의 프로세스를 지원

![png](/assets/images/Program/13_4.png)

- 위와 같이 여러개의 프로세서를 사용하면 성능이 좋아지고, 신뢰성(하나가 고장나도 정상동작) 이 높아집니다.
- 이때 프로세서간 관계 및 역할을 관리해야 합니다. 

> ## Distributed Processing System

- CPU 를 무한정 늘리자니 이를 관리할 시스템도 많아져야되고, 하드웨어 적으로 불가능.. 
  - 그러므로 CPU 를 여러개 쓰지 말고 드냥 시스템을 여러개 쓰자! 라는 아이디어

![png](/assets/images/Program/13_5.png)

- 위처럼 네트워크 (LAN) 를 기반으로 구축된 병렬처리 시스템으로, 컴퓨터를 묶어서 씀
- 각각의 컴퓨터는 다양한 운영체제를 가지고 있을것
  - 이를 관리하기 위해 분산운영체제(Cluster system...) 이용

> 장점

- 자원 공유를 통한 높은 성능 + 신뢰성

> 단점 

- 구축 및 관리가 어려움 (다른 컴퓨터를 연결하는거 자체가 쉽지가 않음..)

> ## Real Time Systems

- 작업 처리에 제한을 갖는 시스템
  - 제한 시간 내에 서비스를 제공하는것이 중요할때에 사용 (원자력 시스템 등)

# [OS System Structure](#link){: .btn .btn--primary}{: .align-center}

> ## 운영체제의 구조

> 커널 (Kernel)

- OS 의 핵심 부분 
- 가장 빈번하게 사용되는 기능을 담당합니다. (시스템 관리)
  - 프로세서 관리, 메모리 관리 등. 
  - 계속 사용해야하므로 메모리에 늘 상주해 있습니다. 
- 동의어 : 핵, 관리자 프로그램, 상주 프로그램, 제어 프로그램

> 유틸리티 (Utility)

- 운영체제에서 커널을 제외한 다른 부분
- UI 등 서비스 프로그램 (비상주이므로 메모리에 늘 있지는 않음)

> 구조 Summary

![png](/assets/images/Program/13_6.png)

- 시스템 콜 : 운영체제가 kernel 에게 관리를 요청할떄 쓰는거

> ## 단일 구조

![png](/assets/images/Program/13_7.png)

- 운영체제 기능을 하나의 거대한 커널로 모아놓은것. 즉 메인 안에 다 넣은것입니다.

> 장점 

- 같은 커널로 모아놓음으로서, 커널간 직접 통신이 가능하여 효율적인 자원 관리 및 사용 가능

> 단점

- 점점 프로그램이 추가됨에 따라서, 커널이 거대화됨
  - 즉 오류 및 버그가 생길 가능성이 커짐 (점점 복잡한 구조가 되므로)
  - 유지보수가 어려움 (복잡해서 어디에서 버그가 나왔는지 모름)
  - 모두가 하나에 모여있어, 한 모듈이 문제가 생기면 다른쪽에 문제가 생길 수 있음

> ## 계층구조

![png](/assets/images/Program/13_8.png)

- 위와 같은 에러 이슈로, 기능별로 따로따로 만들어놓는 아이디어 (모듈화)

> 장점

- 계측간 검정 및 수정이 용이함
- 설계 및 구현이 단순함!

> 단점

- 원하는 기능 수행을 위해서라면 여러 계층을 거쳐야되서 단일 구조 대비 성능이 떨어질 수 있습니다.

> ## 마이크로 커널 구조

![png](/assets/images/Program/13_9.png)

- 커널이 점점 커지니까 문제가 되니까, 커널에는 필수 기능만 포함하고자 하는 아이디어
- 기타 기능은 사용자 영역에서 실행

# [OS System 의 기능](#link){: .btn .btn--primary}{: .align-center}

- 한마디로 말하면 '관리' 임
  - 프로세스(Process) 관리
  - 프로세서(Processor) 관리
  - 메모리(Memory0 관리
  - 파일(File) 관리
  - 입출력(1/0) 관리
  - 보조 기억 장치 및 기타 주변장치 관리 등

> ## Process Management

> Process

- Process : 프로세스 
  - 커널에 등록된 실행 단위 (실행중인 프로그램)
  - 사용자의 요청을 처리하고, 기능을 처리하는 프로그램의 수행 주체가 됩니다. 
- OS 의 프로세스 관리
  - 생성 / 삭제 / 상태관리 / 자원할당 등을 관리
  - 여러 프로세스 등을 중재하고 동기화

> Processor (CPU)

- Processor : 중앙 처리 장치(CPU)
  - 프로그램을 실행하는 핵심적인 자원
- OS 의 프로세서 관리
  - Process 에 대해 프로세서(CPU) 할당을 관리함

> Memory management

- Memory : 주 기억장치 
  - 작업을 위한 프로그램 및 데이터를 올려놓는 공간
- OS 의 메모리 관리
  - 프로세스에 대한 메모리 할당 / 회수
  - 메모리 여유공간을 관리

> File management

- File : 파일 (데이터 저장 단위)
- OS 의 파일 관리
  - 파일 및 디렉토리 생성/ 삭제 / 관리

> I/O management

- I/O : 입출력 과정
- OS 의 입출력 관리
  - 프로세스가 요구한 입출력을 OS 가 수행해줌 (모니터에 띄워준다던지...)

> 그 밖

- 보안, 네트워크 등.... 

---

**Reference**

- <https://www.youtube.com/watch?v=EdTtGv9w2sA&list=PLBrGAFAIyf5rby7QylRc6JxU5lzQ9c4tN&index=3>

