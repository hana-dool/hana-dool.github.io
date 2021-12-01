---
title:  "Process Synchronization and Mutual Exclusion"
excerpt: "프로세스 동기화와 상호배제"
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

# [Process Synchronization](#link){: .btn .btn--primary}{: .align-center}

> ## Process Synchronization

> 다중프로그래밍 시스템 

- 여러개의 프로세스들이 존재하는 시스템
- 이러한 다중 프로그래밍 시스템에서는 프로세서들이 독립적으로 동작함
- A와 B 가 동시에 프로세스를 사용하려고 할때에 문제 발생 가능 (서로 겹치므로)

> 동기화 (Synchronization)

- 위와 같이 겹치는 경우처럼 프로세스들은 유기적으로 작동해야할 필요가 있음!
  - 그래서 프로세스들이 서로 동작을 맞추고 정보를 공유하는것을 동기화라고 함

> ## Asynchronous and Cocurrent P's

> 비동기적(Asynchronous)

- 프로세스들이 서로에 대해서 모르는 경우

> 병행적 (Cocurrent)

- 여러개의 프로세스들이 동시에 시스템에 존재하는 경우

> Note 

- 병행 수행중인 비 동기적인 프로세스들이 공유 자원에 동시 접근할때에 문제가 발생할 수 있습니다.
  - 즉 '서로에 대해 모르는 프로세스가' '동시에' 자원을 쓰려고 하면 문제가 되기 떄문입니다.

> ## Terminology

- Shared data (공유 데이터)
  - 여러 프로세스들이 공유하는 데이터 
  - 공유하므로 건드리면 큰일이 난다고 해서 Critical data 라고도 함
- Critical selection (임계영역)
  - 공유 데이터를 접근하는 코드 영역 
- Mutual Exclusion (상호배제)
  - 둘 이상의 프로세스가 동시에 Critical section 에 진입하는것을 막는것 

> ## Critical Section (Example)

![jpg](/assets/images/Program/27_1.jpg)

- sdata 에 1을 더하는 연산을 두개의 프로세서가 동시에 작업하고 있습니다.
  - 우리는 이때에 2가 되기를 기대합니다! 
- 하지만 기계어 명령어의 특성( 한 기계어 명령의 실행 도중에 인터럽트를 받지 않음!) 때문에 위의 기대대로 실행되지가 않습니다.

![jpg](/assets/images/Program/27_2.jpg)

- s = s+1 의 연산은 세개로 나누어짐 
- 왼쪽 프로세스
  - (1) : 레지스터 R 에 shared data (sdata) 를 불러옵니다.
  - (2) : 레지스터 값에 1을 더하라 
  - (3) : 레지스터를 sdata 에 저장한다.
- 오른쪽 프로세스도 위와 동일

> Note

- CPU 는 안에 레지스터를 가지고 있음! 
  - CPU 의 작업은 레지스터에서 이루어짐. 
- 실제 동작은 메모리상의 데이터를 레지스터에서 막 계산한 다음 , 이를 다시 메모리로 보내는 작업으로 이루어짐

> 계산 결과

- CPU 할당 받음(ready) $\to$ Running 상태로 올라갔다가 메모리를 뻇길 수 있다는것을 기억합시다.
  - 그러므로 명령 수행 과정이 (1) (2) (3) $\to$ (A) (B) (C) 가 되는게 아니라 중간중간 멈추면서 실행될 수 있다는 뜻입니다.
- 그래서 그림과 같이 sdata 가 다른값을 가질 수 있다는 것입니다.

> ## Mutual Exclusion (상호배재)

- 그러므로 우리가 원하는 결과를 보장하려면 '다른 프로세스의 영향을 받을 수 있는 과정을 수행중에는 다른 프로세스의 진입을 막아야' 할 것입니다.
  - 이렇게 다른 프로세스의 진입을 막는것을 상호배재 라고 합니다.

![jpg](/assets/images/Program/28_1.jpg)

> ## Mutual Exclusion Methods

- 이제 위와 같은 상호배재를 구현하는법을 알아봅시다.

> Mutual exclusion primitives (기본이 되는 연산)

- enterCS() primitive
  - Critical section 진입 전 검사
  - 다른 프로세스가 critical section 안에 있는지 검사
  - 안에 프로세서 누가 있는지 검사를 하는 과정입니다.
- exitCS() primitive
  - Critical section을 벗어날 때의 후처리 과정
  - Critical section을 벗어남을 시스템이 알림
  - 연산 끝내고 나올때 다른 프로세스가 들어와도 된다는것을 알려주는 과정입니다.

> 구현 (Requirements for ME primitives)

- 이러한 계산을 시스템에서 구현하려면 어떻게 할까요? 우선 아래와 같은 조건이 있습니다.
- Mutual exclusion (상호배제)
  - Critical section (CS) 에 프로세스가 있으면, 다른 프로 세스의 진입을 금지
- Progress (진행)
  - $\mathrm{CS}$ 안에 있는 프로세스 외에는, 다른 프로세스가 $\mathrm{CS}$ 에 진입하는 것을 방해 하면 안됨
  - 즉 A,B 프로세스가 CS(Critical section) 에 들어가려고 경쟁하고 있는데, A 가 아직 CS 에 들어가지 않았는데도 불구하고 B 가 CS 에 못들어가게 방해하는 작업을 하면 안된다는 것입니다.
- Bounded waiting (한정대기)
  - 프로세스의 CS 진입은 유한시간 내에 허용되어야 함
  - (즉 언젠가는 진입할 수 있어야 한다는 것입니다.)

> ## Version1

![jpg](/assets/images/Program/28_2.jpg)

- Turn 이라는것을 줌.  즉 프로세스들은 turn 이 어떤것인지에 따라서 우선권을 다르게 가집니다.
- 이때 위와 같은 구현은 3가지 조건 (Mutual exclusion , Progress , Bounded Wating) 을 만족할까요? 

> Counter Example 1

- 위 그림은 0번 trun 입니다. 즉 0번 프로그램이 먼저 우선권을 가지죠
- 그런데 0번 프로그램이 계속 계산되다가 예기치 않게 ( 즉 trun = 1 로 돌려주지 못하고) 죽어버렸다고 합시다. 그러면 이 때에는 비어있지만 프로세스 0은 계속 대기하게 됩니다. 

> Counter Example 2

- 0 번 프로그램이 일을 다 했다고 합시다. 아직 한번 더 일해야 되고, 프로그램 1번은 아직 오지 못했다고 합니다.
- 이 경우에 turn 이 1이여서 0번 프로그램은 일을 못하는 상태입니다. 즉 계속 대기하게 됩니다. (비효율적)

> ## Version 2

![jpg](/assets/images/Program/28_3.jpg)

- 버젼 2 는 플레그(깃발) 을 정의합니다.
  - 즉 이는 프로그램 1이 들어와 있으면 1번의 깃발을 들고, 1번이 나갈때는 1번의 깃발을 내리자는 것입니다. 
- 이 경우에 상대편의 깃발이 없을때에만 작동할 수 있습니다. 

> Counter Example ( Mutual Exclusion 위배 )

- 위 그림에서처럼 $P_0$ 은 $P_1$ 보다 빨리 도착해서 while 문 (깃발이 들려있는지 아닌지를 검사하는 부분) 을 통과하고 endwhile 부분에서 아쉽게 preemption (잠깐 멈춤)가 되었다고 합시다. 
- 그 사이에 $P_1$ 이 도착했는데, 아무도 없으므로 (깃발상에서는 깃발이 모두 내려가 있으니까요) CS 에 들어가게 됩니다.
- $P_1$ 이 수행되던 도중에 $P_0$ 이 다시 돌아와서 연산되면 CS 에 두개가 겹치게 됩니다! 

> ## Version 3 

![jpg](/assets/images/Program/28_4.jpg)

- 위처럼 처음 플그램을 시작할때에 깃발을 들면 되지 않을까요?  

> Counter Example  (Bounded Waiting 조건 위배)

- $P_0$ 도착 이후 깃발을 든 이후에 preemption 
- $P_1$ 도착 이후 깃발을 든 이후에 Preemption
- $P_0$ 이 다시 시작했는데, 상대편 깃발이 들려있어서 계속 대기 ($P_1$도 마찬가지)

# [Process Solution](#link){: .btn .btn--primary}{: .align-center}

> ## Solutions

- SW solutions
  - Dekker's algorithm (Peterson's algorithm)
  - Dijkstra's algorithm, Knuth's algorithm, Eisenberg and McGuire's algorithm, Lamport's algorithm
- HW solution
  - TestAndSet (TAS) instruction
- OS supported SW solution
  - Spinlock
  - Semaphore
  - Eventcount/sequencer
- Language-Level solution
  - Monitor

> Note 

- 위의 Solution 에 대한 자세한 설명은 생략하겠습니다.

---

**Reference**

- <https://www.youtube.com/watch?v=_gNeoGQx-Tc&list=PLBrGAFAIyf5rby7QylRc6JxU5lzQ9c4tN&index=8>



