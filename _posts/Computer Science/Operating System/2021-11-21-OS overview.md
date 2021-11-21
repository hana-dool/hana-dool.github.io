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

# [OS System Overview](#link){: .btn .btn--primary}{: .align-center}

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

---

**Reference**

- <https://www.youtube.com/watch?v=EdTtGv9w2sA&list=PLBrGAFAIyf5rby7QylRc6JxU5lzQ9c4tN&index=3>

