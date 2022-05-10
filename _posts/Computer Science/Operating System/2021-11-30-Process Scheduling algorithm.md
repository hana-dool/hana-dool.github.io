---
title:  "Process Scheduling Algorithm"
excerpt: "프로세스 스케쥴링 알고리즘"
categories:
  - Operating_System
last_modified_at: 2021-11-25
toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
author_profile: true

use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 운영체제에 대해서 알아봅시다.
{: .notice--warning}

# [Basic Scheduling algorithm](#link){: .btn .btn--primary}{: .align-center}

> ## Basic scheduling algorithm

- FCFS (First-Come-First-Service)
- RR (Round-Robin)
- SPN (Shortest-Process-Next)
- SRTN (Shortest Remaining Time Next)
- HRRN (High-Response-Ratio-Next)
- MLQ (Multi-level Queue)
- MFQ (Multi-level Feedback Queue)
- 위와 같이 매우 많은 알고리즘이 있는것을 알 수 있습니다. 하나씩 알아보도록 해요

> ## FCFS

![jpg](/assets/images/Program/23_1.jpg)

- 한마디로 말하면 선착순 알고리즘
  - 그냥 먼저 오는 프로세스에게 먼저 프로세서(CPU) 를 할당해줌

> 스케쥴링의 기준

- 스케쥴링의 기준은 이전에 말했듯이 아래와 같습니다.
  - 도착 시간 (먼저 도착한 프로세스를 먼저 처리)

> 장점

- 이렇게 처리할 경우, 오는데로 프로세서에게 던져주면 되니까 CPU 는 쉬지않고 일할 수 있습니다. 
  - 즉 sceduling overhead 가 매우 적습니다! 
- 이러한 서비스는 배치시스템 (일괄처리 시스템) 에 적합합니다.
  - 배치 시스템은 오는대로 빨리빨리 처리하는게 목적이기 때문입니다.

> 단점

- 대화형 시스템에서는 부적합합니다. (내가 넣은 인풋이 언제 output 이 나올지 알 수 없음)
- 내가 처리할 프로그램은 1초면 끝나는데, 앞에 1분짜리가 있다면 나는 1초를 위해 1분이나 기달려야 함...
  - 이런이유때문에 평균적으로 큰 대기시간을 가지게 됩니다.

> ## RR ( Round - Robin)

![jpg](/assets/images/Program/23_2.jpg)

- 너무 순서대로만 일을 시키니까, 다른애들이 불만이 생김! 그러므로 돌아가면서 CPU 를 쓰자는 아이디어 

> 스케쥴링의 기준

- 우선 도착시간(ready queue) 기준
  - 하지만 자원 사용 제한시간 (time quantum) 이 있음! 
- 제한시간이 지나면 자원을 반납하고 다음 프로세스가 일을 하게됨
  - 이는 특정 프로세스의 자원 독점을 방지합니다.
- 하지만 빈번하게 프로세스를 바꿔야 하므로 Context switch overhead 가 큽니다. 
- 대화형, 시분할 시스템에 적합합니다.

> 핵심

- Time quantum (제한시간) 이 성능을 결정하는 핵심 요소 
  - 제한시간이 infinite 면 이전 FCFS 와 같음
    - 제한시간이 매우 작으면 프로세서를 동시에 쓰는 느낌을 받음 (하지만 체감속도는 프로세스의 수를 n 이라 할때에 1/n 임)

> ## SPN ( Shortest - Process - Next)

- 이전에 선착순은 , 빨리 끝나는 Process 들이 오래 기달려야해서 불공평하다고 했었습니다.
  - 그러므로 짧은 (Burst time 이 짧은) 애들 먼저 처리하자는 아이디어!

> 스케쥴링 기준

- 실행시간 ( Burst time ) 이 제일 적은 프로세스를 먼저 처리하게 됨

> 장점

- 평균 대기시간이 최소화 (빨리 끝나는애들부터 다 처리하니까)
- 시스템 프로세스 수 최소화 (빨리 끝나는 애들을 먼저 처리하니까)
  - 프로세스가 적으므로 시스템 입장에서 부하가 적고 메모리가 절약됨!
- 많은 프로세서들에게 빠른 응답 시간 제공

> 단점

- 오래 걸리는 프로세스는 자원을 할당받지 못할 수 있음 (Starvation : 무한대기) 현상이 발생할 수 있습니다.
- 정확한 실행시간을 에측할 수 없음 

> ## STRN (Shortest Remaining Time Next)

- SPN 의 변형. SPN 과 다른점은 잔여 실행시간이 더 적은 프로세스가 ready 상태가 되면 그 프로세스가 CPU 를 선점
  - 즉 '제일 짧은 프로세스' 를 계속 찾음으로서 그 효과를 극대화

> 장점

- SPN 의 장점 극대화

> 단점

- 프로세스 생성시 총 실행시간 예측이 필요하고 ( 왜냐면 실행시간이 기준이니까 ) 잔여시간을 계속 추적해야함
- Context switching overhead

> ## HRRN

- SPN 의 문제점은 기아현상 (Starvation ) 이 문제였음! 
  - 프로세스의 대기시간 (wT) 를 고려하여 기회를 제공
  - Aging concepts 로서, 대기시간이 긴 녀석들에게 우대사항을 주겠다는 것임

> 스케줄링 기준

- Response ratio 가 높은 프로세스를 우선
  - Response ratio $=\frac{W T+B T}{B T}$ (응답률)  (WT : Waiting time , BT : Burst Time)
  - 오래 기달리면 Response Ratio 가 높아짐! 

> 특징

- SPN의 장점 + Starvation 방지 
- 하지만 여전히 실행 시간 예측 기법 필요 (overhead)

> ## 중간 서머리

![jpg](/assets/images/Program/23_3.jpg)

- FCFS , RR 은 공평한 스케쥴링
- SPN , SRTN , SRRN 은 시스템에서의 성능, 효율성을 높히는 스케쥴링
  - 이때 실행시간 예측의 부하가 문제가 되는데 이를 해결하는 방법은 MLQ , MFQ

> ## MLQ (Multi - level Queue)

![jpg](/assets/images/Program/23_4.jpg)

- 작업 ( or 우선순위 ) 별 별도의 ready queue 를 가집니다.
  - 최초 배정된 queue 를 벗어나지 못함 
  - 각각의 queue 는 자신만의 스케쥴링 기법을 사용
- Queue 사이에는 우선순위 기반의 스케쥴링을 사용함

> 장점

- 중요한 애들은 (우선순위가 높은 queue) 빨리 처리 가능

> 단점

- 여러개의 Queue 관리 등 스케쥴링 overhead
- 우선순위가 낮은 queue 는 stavation 현상이 발생

> ## MFQ ( Multi - level Feedback Queue)

![jpg](/assets/images/Program/23_5.jpg)

- 프로세스의 Queue 간 이동이 허용된 MLQ
  - 피드백을 통해서 우선순위를 조정합니다. ( 즉 큐들의 우선순위가 변할 수 있음 )
- 프로세스의 사전 정보 없이 (즉 Burst time 에 대한 예측 없이 ) 어느정 SPN ,SRTN 등과 같은 기법의 효과를 낼 수 있습니다.

> 단점

- 설계 및 구현이 복잡함, 스케쥴링 오버해드가 큼
- Starvation 문제 

> 변형

- 각 큐마다 시간 할당량을 다르게 배정
- 입출력 위추의 프로세스 (CPU 를 조금만 쓰고 나오는 애들!) 를 우선순위 높힐 수 있음
- 대기시간이 지정된 시간을 넘은경우 (Aging) 우선순위를 높힐 수 있음 (상위큐로 이동)

---

**Reference**

- <https://www.youtube.com/watch?v=_gNeoGQx-Tc&list=PLBrGAFAIyf5rby7QylRc6JxU5lzQ9c4tN&index=8>



