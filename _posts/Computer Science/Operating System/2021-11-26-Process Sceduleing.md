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

---

**Reference**

- <https://www.youtube.com/watch?v=_gNeoGQx-Tc&list=PLBrGAFAIyf5rby7QylRc6JxU5lzQ9c4tN&index=8>



