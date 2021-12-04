---
title:  "Deadlock"
excerpt: "프로세스가 막힌 상태"
categories:
  - Operating_System
last_modified_at: 2021-11-30
toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
author_profile: true

use_math: true
---

 운영체제에 대해서 알아봅시다.
{: .notice--warning}

# [Deadlock](#link){: .btn .btn--primary}{: .align-center}

> ## Deadlock

- 어느 프로세스도 자기가 원하는 일을 할 수 없는 상태

> Blocked / Asleep state

- 프로세스가 특정 이벤트를 기다리는 상태
- 프로세스가 필요한 자원을 기다리는 상태

> Deadlock state

- 프로세스가 발생 가능성이 없는 이벤트를 기다리는 경우
  - 프로세스가 deadlock 상태에 있음 (계속 기다리기만 하고 일을 못함)
- 시스템 내에 deadlock에 빠진 프로세스가 있는 경우
  - 시스템이 deadlock 상태에 있음

> Deadlock vs Starvation

- Starvation 과 Deadlock 은 둘다 매우 유사해 보입니다. 어떤 차이가 있을까요? 

![jpg](/assets/images/Program/29_1.jpg)

- Deadlock 은 asleep 상태에서 자원 또는 이벤트를 기다리는데, 가능성이 제로인 상태입니다.
- Starvation 은 CPU 를 기다리는것입니다. 그런데 앞에서 자꾸 다른 프로그램이 있어서 (운이 없거나 우선순위가 밀려서) 계속 기다리는 것입니다. 

> ## 자원의 분류

- 위에서 저희는 자원이 여러개가 있음을 알 수 있습니다. 자원은 어떤것이 있을까요 

> 일반적인 분류

- Hardware resources 
- Software resources

> 다른 분류 법 (Deadlock 입장에서)

- 선점 가능 여부에 따른 분류
- 할당 단위에 다른 분류
- 동시 사용 가능 여부에 따른 분류
- 재사용 가능 여부에 따른 분류

> 선점 가능 여부에 따른 분류 

- Preemptible resource
  - 선점당한 후 돌아왔을때에도 , 내가 일을 하는데에 문제가 발생하지 않는 자원
  - Processor(CPU 를 뺏겼을때는 잠시 멈출뿐 Context Switch , Saving 등 덕분에) 잘 작동함, 
  - memory( Swap device 등을 통해서) 도 뻇겼다돌아와도 잘 작동

- Non-preemptible resources
  - 선점 당하면, 이후 진행에 문제가 발생하는 자원
    - Rollback, restart등 특별한 동작이 필요
  - E.g., disk drive 등 (내가 데이터를 기록하고 있는데 다른사람이 뻇어버리면 문제가 발생 (데이터 날라감))

> 할당 단위에 따른 분류

- Total allocation resources (전체를 다 줌)
  - 자원 전체를 프로세스에게 할당
  - Processor (하나의 CPU 는 한번에 하나의 프로그램이 선점 가능)
  - disk drive 등

- Partitioned allocation resources
  - 하나의 자원을 여러 조각으로 나누어, 여러 프로세스 들에게 할당
  - Memory 등 (메모리는 프로세스별로 나누어서 할당이 가능)

> 동시 사용가능 여부에 따른 분류

- Exclusive allocation resources
  - 한 순간에 한 프로세스만 사용 가능한 자원
  - Processor, 
  - memory (잘라서 다른것들과 같이 쓸 수 있기는 하지만 '잘린 메모리들' 은 하나의 프로그램에게만 할당됨) 
  - disk drive 
- Shared allocation resource
  - 여러 프로세스가 동시에 사용 가능한 자원
  - Program(sw) (창 여러개 띄워서 사용할 수 있음! 즉 프로그램은 여러 프로세스가 동시에 사용 가능하다는 것임)
  - shared data 등 (여러 프로그램이 나눠쓰는 데이터)

> 재사용 가능 여부에 따른 분류

- SR (Serially-reusable Resources)
  - 시스템 내에 항상 존재 하는 자원
  - 사용이 끝나면, 다른 프로세스가 사용 가능
  - E.g., Processor, memory, disk drive, program 등
- CR (Consumable Resources)
  - 한 프로세스가 사용한 후에 사라지는 자원
  - E.g., signal, message 등

> ## Deadlock 과 자원의 분류

- Deadlock을 발생시킬 수 있는 자원의 형태
  - Non-preemptible resources (한번 할당받으면 절대 안뻇기려고 하므로)
  - Exclusive allocation resources (자원을 혼자 쓰게 되므로)
  - Serially reusable resources  
  - 할당 단위는 영향을 미치지 않음

- CR을 대상으로 하는 Deadlock model은 다루지 않음! ( 없어지는 자원이라 다루기가 어려움 )



---

**Reference**

- <https://www.youtube.com/watch?v=_gNeoGQx-Tc&list=PLBrGAFAIyf5rby7QylRc6JxU5lzQ9c4tN&index=8>



