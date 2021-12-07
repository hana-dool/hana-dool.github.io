---
title:  "Virtual Memory"
excerpt: "가상메모리"
categories:
  - Operating_System
last_modified_at: 2021-12-03
toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
author_profile: true

use_math: true
---

 메모리에 대해서 알아봅시다.
{: .notice--warning}

# [Virtual Storage](#link){: .btn .btn--primary}{: .align-center}

> ## Not Continuous Allocation

- 사용자 프로그램을 여러개의 Block 으로 분할한 뒤, 필요한 block 들만 메모리에 적재합니다.
  - 프로세스를 통쨰로 올려놓는게 아니라 필요한 일부만 메모리에 적재하는 것입니다.
  - 필요하지 않은 block 들은 swap device 에 존재하게 됩니다.

- 기법들
  - Paging system
  - Segmentation system
  - Hybrid paging/segmentation system

> ## Address Mapping

- Continuous allocation 에서는 Address mapping 이란 상대주소를 물리적인 배치로 할당하는것
  - Relative address (상대 주소)
    - 프로그램의 시작 주소를 0 으로 가정한 주소
    - 코딩할때에는 0부터 시작한다고 가정하되, 실제 메모리에 적재될때에는 빈 메모리의 시작점이 v 라면, v 를 0 으로 생각하고 메모리가 적재됨
  - Relocation (재배치)
    - 메모리 할당 후, 할당된 주소(allocation address)에 따라 상대 주소들을 조정하는 작업
- Non-continuous allocation 에서 Address mapping 이란 가상 주소를 물리적인 주소로 할당하는것
  - Virtual address (가상주소)  = relative address
    - Logical address (논리주소)
    - 연속된 메모리 할당을 가정한 주소 (메모리 자체는 나뉘어지는것을 가정하지 않음!)
      - 나뉘어져 있는 메모리를 가정하면 구현이 어려움...
  - Real address (실제주소) = absolute (physical)
    - 실제 메모리에 적재된 주소

![jpg](/assets/images/Program/46_1.jpg)

- 사용자 / 프로세스는 실행 프로스램 전체가 메모리에 연속적으로 적재되었다고 생각하면서 작동할 수 있음
  - 하지만 실제로는 원하는 부분을 실행하려 할때에 Virtual address $\to$  Address Mapping $\to$ Real Address 로 변환되는 과정을 거치며 각 부분이 메모리에 적재됨

> ## Bock Mapping

- 사용자 프로그램을 Block 단위로 분할하고 관리함
  - 각 Block 에 대한 Address mapping 정보를 유지

- Virtual address : $v=(b, d)$
  - b = block number
  - $d$ = displacement(offset) in a block

![jpg](/assets/images/Program/46_2.jpg)

- b 는 주황색깔 블록을 의미합니다. 
- d 는 블록의 시작점으로부터 얼마나 떨어져 있는지를 의미합니다.

> Block map Table (BMT)

![jpg](/assets/images/Program/46_3.jpg)

- BMT 라는 Table 을 통해서 Affress mapping 의 정보를 관리됩니다.

---

**Reference**

- <https://www.youtube.com/watch?v=_gNeoGQx-Tc&list=PLBrGAFAIyf5rby7QylRc6JxU5lzQ9c4tN&index=8>



