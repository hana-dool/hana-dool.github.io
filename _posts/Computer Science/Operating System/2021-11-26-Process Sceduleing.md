---
title:  "Process Scheduling"
excerpt: "프로세스 스케쥴링"
categories:
  - Operating_System
last_modified_at: 2021-11-25
toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
author_profile: true

use_math: true
---

 운영체제에 대해서 알아봅시다.
{: .notice--warning}

# [Process Scheduling](#link){: .btn .btn--primary}{: .align-center}

> ## Process Scheduling

- 우리가 쓰는 프로그램은 많은 프로세스를 가지고 있습니다.
  - 프로세스가 여러개이므로 자원을 나누어 사용해야함. (CPU 가 하나면 이것을 프로세스들이 나누어서 사용해야..)
  - 이렇게 자원을 할당 할 프로세스를 정하는것을 스케쥴링 이라고 함

> 관리하는것

- 시간 분할 (Time Sharing) 관리
  - CPU 는 한번에 하나만 들어갈 수 있으므로, 언제 누가 사용할지에 대해서 정해야 합니다. 
  - 이를 프로세스 스케쥴링 이라고 함
- 공간 분할 (Space shaeing)
  - 메모리 공간이 있는 경우, 반씩 나누어서 프로그램이 각각 사용할 수 있습니다.

> ## 스케쥴링의 목적

- 시스템의 성능 향상
- 이러한 성능은 사실 상당히 모호한 개념.. 어떤것 성능이라고 할끼요? 

> 성능

- 응답 시간 (response time)
  - 우리 요청에 대해 얼마나 빨리 응답해주는가?
- 작업 처리량 (throughput)
  - 주어진 시간동안 얼마나 일을 했는가?
- 자원 활용도 ( resource utilization)
  - 얼마나 주어진 자원을 효율적으로 계속 사용했는지?
  - 주어진 시간 $T_c$ 동안 자원이 활용된 시간 
- 등등등... 엄청 많은 지표가 존재

> 어떤게 제일 중요할까?

- 목적에 따른 지표를 고려하여 스케쥴링 기법을 선택해야함
- 대화형 시스템 $\to$ 응답시간이 중요
- 일괄 처리 시스템  $\to$ 작업 처리량이 중요

> ## 용어정리 : 대기시간, 응답시간, 반환시간

![png](/assets/images/Program/21_1.png)

- 대기시간 : 프로세스가 실행하기까지 기다리는 시간을 대기시간이라고 함
- 응답시간 : 작업이 수행되다가 처음 출력 (즉 화면에 나오거나 등..) 하기까지 시간
- 실행시간 : 프로세스가 실행된 시간
- 반환시간 : 일을 수행했을때 걸린 모든 시간

> ## 스케쥴링의 기준

- 스케쥴링 기준이 고려하는 항목들은 다음과 같습니다.
- 프로세스의 특성
  - I/O bounded , Computed Bounded
- 시스템의 특성 
  - Batch 인지 interactive system 인지에 따라 누구를 먼저 처리할지가 달라질 수 있음
- 프로세스의 긴급성 
  - 긴급한 녀석을 먼저 처리하려고 합니다.

> Note CPU burst vs I/O burst(Bounded)

- 어떤 프로세스가 작업하는것은 CPU 를 써서 계산 $\to$ 입출력 대기 $\to$ CPU 사용 ...... 처럼 계속 반복되어서 작업이 수행하게 됩니다.
  - 즉 프로세스 수행은 CPU 사용 + I/O 대기 하는것을 반복하면서 수행됩니다.

- CPU burst (Compute Bounded)
  - CPU 사용 시간 > I/O 대기시간인 프로그램
  - 즉 이러한 프로그램의 경우 최적화를 위해서라면 CPU 사용 시간이 더 중요한 요소!
- 1/O burst ( I/O Bounded)
  - CPU 사용시간 < I/O 대기시간인 프로그램
- Burst time은 스케줄링의 중요한 기준 중 하나 

> ## 스케쥴링의 단계

- 발생하는 빈도 및 할당 자원에 따라 구분이 가능
- Long-term scheduling
  - 장기 스케줄링
  - Job scheduling
- Mid-term scheduling
  - 중기 스케줄링
  - Memory allocation
- Short-term scheduling
  - 단기 스케줄링
  - Process scheduling

> Long - Term Scheduling

![png](/assets/images/Program/21_2.png)

- 이름에서 보다시피, 긴 시간에 한번씩 일어나는 스케쥴링입니다.
- Job scheduling 
  - job 들이 시스템에 등록되려고 줄을 서 있을것입니다. 이 중에서 시스템에 제출할 (즉 커널에 등록 할) 작업을 결정하는 작업(스케쥴링) 입니다.
- 다중 프로그래밍의 정도를 조절합니다.
  - 즉 프로그램을 무제한 시스템에 넣을 수 없으므로 시스템 내에 프로세스의 수를 조절합니다. 
- 그렇다면 이제 누구를 시스템에 올릴까? 가 고민될 것입니다.
  - I/O Bounded 와 Compute Bounded 프로세스중 누구를 올릴까요?
  - 정답은 바로 잘 섞어서 등록해야합니다. 
    - CPU , I/O Device 두개가 있는데, Compute Bounded 만 넣는다면 CPU 만 일하게 되기 때문입니다. 즉 잘 섞어서!

> Mid - Term scheduling 

![png](/assets/images/Program/21_3.png)

- 메모리 할당을 결정
  - Suspended ready $\to$ ready 로 작업을 올릴때 메모리를 할당하게 됩니다.
  - 이때 기다리고 있는 많은 애들중에서 어떤것을 올릴지가 바로 미드텀 스케줄링입니다.

> Short-term Scheduling

![png](/assets/images/Program/21_4.png)

- CPU 를 기다리고 있던 (ready) 애들을 CPU 로 할당해주는 스케쥴링
  - 프로세서를 할당할 프로세스를 결정
- 프로세스 스케쥴링이라고도 함
- 매우 빈번하게 발생하므로 매우 빨라야합니다.

> ## 스케쥴링의 단계

![png](/assets/images/Program/21_5.png)

# [Scheduling Policy](#link){: .btn .btn--primary}{: .align-center}

> ## 스케줄링의 정책 (Policy)

- 스케쥴링을 어떤 방법을 사용할것인지? 에 대한 것입니다.
- 두가지의 기준에 의거하여 살펴보겠습니다.
  - 선점 vs 비선점 방법
  - 우선순위 정책

> ## Preemptive(선점) vs Non-Preemptive scheduling(비선점)

> 비선점 스케쥴링 (자원을 뻇을 수 없다!)

- 어떤 프로세스가 자원을 할당 받으면 스스로 반납할때까지 사용함
- 장점 : Context switch overhead 가 적음 (작업을 자기가 다 쓰니까)
- 단점 : 급한일을 먼저 처리 못함 / 평균 응답시간 증가(다른애들은 게속 기다림)

> 선점 스케쥴링 (자원을 뻇을 수 있음)

- 프로세스가 자원을 빼앗길 수 있음 (할당시간이 종료되거나, 우선순위 때문에)
- 장점 : 응답성이 높아짐 , 급한일을 빨리 처리 가능(응답성 향상)
- 단점 : Context switch overhead 가 큼 (시스템의 부하가 큼)

> ## Priority

- 프로세스의 중요도에 따른 정책을 알아봅시다. 

> Static Priority (정적인 우선순위)

- 프로세서 생성시에 결정된 Priority 가 유지됩니다.
- 구현이 쉽고 오버해드가 적음 (우선순위가 안변하니까)
- 시스템 환경 변화에 따른 대응이 어려움...

> Dynamic Priority (동적 우선순위)

- 프로세스의 상태 변화에 따라 Priority 가 변경됩니다.
- 구현이 복잡하고, Priority 를 재계산해야되서 오버해드가 큼
- 시스템 환경 변화에 유연한 대응이 가능

![png](/assets/images/Program/21_6.png)

- 위와 같이 우선순위(Priority) 를 바꾸는것을 볼 수 있습니다.

---

**Reference**

- <https://www.youtube.com/watch?v=_gNeoGQx-Tc&list=PLBrGAFAIyf5rby7QylRc6JxU5lzQ9c4tN&index=8>



