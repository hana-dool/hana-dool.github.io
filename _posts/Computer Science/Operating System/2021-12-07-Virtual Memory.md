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
  - 프로세스마다 하나의 BMT 를 가집니다. (하나의 프로세스를 나누게 되므로)
- 프로세스가 나누어져 있으므로 각각 블록으로 나뉘에 됩니다.
  - 프로세는 사실 모두 스왑 디바이스에 있을것입니다. 
  - 프로세스의 일부가 메모리에 올라오면 Residence bit 이  1 로 바뀌게 됩니다. 

> 작동 예시

![jpg](/assets/images/Program/51_1.jpg)

1.프로세스의 BMT에 접근

2.BMT에서 block b에 대한 항목(entry)를 찾음

3.Residence bit 검사

- (1) Residence bit $=0$ 경우, swap device에서 해당 블록을 메모리로 가져 옴 BTM 업데이트 후3-(2) 단계 수행
- (2) Residence bit = 1 경우, BMT에서 $b$ 에 대한 real address 값 $a$ 확인

4.실제 주소 $r$ 계산 $(r=a+d)$

5.$\mathrm{r}$ 을 이용하여 메모리에 접근

> Note

- 우리가 쓰는 virtual address 는 b와 d 로 구성됩니다. 데이터가 필요하면 이 (b,d) 를 읽어달라고 요청하게 됩니다.
- 우선 우리는 BLock b 를 먼저 찾아야 하고 , Block mapping table 을 보게 됩니다.
- 이때 Block mapping Table 에서 다음과 같은 정보를 조회해 봅니다.
  - b block 이 사용중인가 ? 
  - b block 의 진짜 주소(a)  는 어디있는가?
- 이제 시작점으로부터 얼마나 떨어져있는지를 조회하기 위하여 d 를 불러옵니다. 
  - 그러면 b block 의 주소는 a+d 에 위치하게 됩니다. 

# [Virtual Storage Methods](#link){: .btn .btn--primary}{: .align-center}

- 실제로 운영체제가 사용하는 메모리 시스템을 알아봅시다.

> ## Paging System

- 프로그램을 같은 크기의 블록으로 분할 (Pages)
  - 우리가 Non continuous allocation 에서 프로그램을 같은 크기의 Block으로 분할한다고 했었습니다. 
  - 이때 나누어진것을 Paging 이라고 합니다.
- Page
  - 프로그램의 분할된 block
- Page frame
  - 메모리의 분할 영역
  - Page와 같은 크기로 분할
  - 우리가 프로그램이르 page 크기로 분할했으면, 메모리도 page 만큼 분할하면 될 것입니다.

![jpg](/assets/images/Program/51_2.jpg)

- 그림으로 표현하면 위와 같습니다. 프로세스는 같은 크기의 page 로 쭈욱 나뉘고, swap device 에 담기게 됩니다.
  - 이 swap device 를 일종의 가상메모리라고 할 수 있습니다.
- 그리고 나누어진 page 중에서 실제적으로 사용되는것들을 Main Memory 에 올리게 됩니다. 

> 특징

- 특징
  - 프로세스를 나눌때 페이지 크기(일정하게) 로 나눈것이므로 논리적 분할이 아님 (크기에 따른 분할)
  - Page 공유(sharing) 및 보호(protection) 과정이 복잡함 
    - function 별로 나누면 편할것이지만 크기별로 나누어서 관리가 힘듦
- Simple and Efficient (크기별로 나누기만 하면 되므로 편리)
  - Segmentation 대비
- 메모리와 프로그램(프로세스) 가 같은 크기로 나누어져 있으므로 No external fragmentation (단편화) 가 존재하지 않음. 
- 하지만 같은 크기로 나누다가 작은 크기가 남을 수 있습니다. 이 크기가 할당된다면 Internal fragmentation(내부 단편화) 발생 가능

> Paging System in window

![jpg](/assets/images/Program/51_3.jpg)

- 가상 메모리에서 페이징 파일을 관리할 수 있습니다.
- 사용자 지정 크기로 페이징의 크기를 조절할 수 있습니다 (윈도우에서는 기본적으로 4KB)
- 즉 만약 게임을 돌리는데 렉이 먹는다면 가상메모리를 좀 더 빠른 디스크로 올리면 전체적인 성능이 올라갈 것입니다.

> ## Address Mapping

- Virtual address : $v=(p, d)$
  - 가상 주소가 여기에서도 존재하게 됩니다. (이전에는 블록 이였다면 여기는 페이지)
  - $p$ : page number
  - $d$ : displacement(offset)
- Address mapping
  - PMT(Page Map Table) 사용
- Address mapping mechanism
  - Direct mapping (직접 사상)
  - Associative mapping (연관 사상)
    - TLB(Translation Look-aside Buffer)
  - Hybrid direct/associative mapping

> Page Map Table

![jpg](/assets/images/Program/51_4.jpg)

- BMT 와 매우 비슷하게 생김 
  - page number : 프로세스에 대한 페이지
  - residence bit : 메모리에 올라와 있는지 아닌지
  - page frame number : 메모리에 올라와 있다면 어디에 올라와 있는지
  - Seconde storage address : 현제 프로세스는 스왑 디바이스에 적혀있으므로, 스왑디바이스 어디에 저장되어있는지를 나타냄

> ## Address mapping : Direct mapping

- Block mapping 방법과 유사
- 가정
  - PMT를 커널 안에 저장
  - PMT entry size = entrySize (표도 일종의 데이터이므로, 표에서 한 줄의 사이즈를 알아야 접근할 수 있음!)
  - Page size = pagesize (프로세스가 나누는 페이지의 크기)

![jpg](/assets/images/Program/51_5.jpg)

1.처음에 virtual address 는 p,d 로 저장되고 페이지가 메모리에 있는지 아닌지부터 봐야 합니다. 

2.그러므로 해당 프로세스의 PMT가 저장되어 있는 주소 b에 접근합니다.

3.해당 PMT에서 page p에 대한 entry 찾음 ($p$ 의 entry 위치 $=b+p$ * entrySize 를 이용해 표에서 위치를 찾음)

4.찾아진 entry의 존재 비트 검사

- (1) Residence bit $=0$ 인 경우 (page fault) 
  - Asleep 상태가 되게 되는데 이때 Context switching 을 발생시킵니다.
  - swap device에서 해당 page를 메모리로 적재
  - PMT를 갱신한 후 3-(2) 단계 수행
- (2) Residence bit = 1인 경우,
  - 해당 entry에서 page frame 번호 $\mathrm{p}^{\prime}$ 를 확인

4.$\mathrm{p}^{\prime}$ 와 가상 주소의 변위 $\mathrm{d}$ 를 사용하여 실제 주소 $\mathrm{r}$ 를 형성.

- $r=p^{\prime *}$ pagesize $+d$

5.실제 주소 $\mathrm{r}$ 로 주기억장치에 접근

![jpg](/assets/images/Program/51_5.jpg)

> 문제점

- 위 그림에서처럼 원하는 메모리에 접근하기 위해서 page map table 을 보게됩니다. 근데 이것은 메모리에 있죠. 즉 메모리에 두번 접근해야 합니다. $\to$ 성능 저하 이휴
- PMT. 를 위한 메모리 공간이 추가적으로 필요 

> 해결방법

- Associative mapping (TLB)
- PMT를 위한 전용 기억장치(공간) 사용
  - Dedicated register or cache memory
- Hierarchical paging
- Hashed page table
- Inverted page table

> ## Address mapping : Associative mapping

- TLB(Translation Look-aside Buffer)에 PMT 적재 (즉 PMT 를 탐색하는 전용 하드웨어)
  - Associative high-speed memory

![jpg](/assets/images/Program/51_6.jpg)

- p 라는 페이지를 요청하게 되면, 주소를 이전처럼 찾는게 아니라 ($p$ 의 entry 위치 $=b+p$ * entrySize 를 이용해 표에서 위치를 찾기) 병렬로 동시에 p 가 어디있는지 후우욱! 탐색하게됨 
- PMT 의 탐색이 매우 빠르고, 메모리까지 가지가 않으므로 부담이 적습니다.

> 장점

- PMT를 병렬 탐색
- Low overhead, high speed

> 단점 

- Expensive hardware ( PMT 전용의 하드웨어가 넘나 비싸다는것.. )
- 큰 PMT를 다루기가 어려움

> ## Address mapping : Hybrid Direct / Associtate Mapping

- 두 기법을 혼합하여 사용 (PMT 중의 일부만 TLB 에 올리기)
  - $\mathrm{HW}$ (TLB) 비용은 줄이고, Associative mapping의 장점 활용
- 작은 크기의 TLB 사용
  - 전체 PMT 는 우선 메모리(커널 공간)에 저장
  -  PMT 중 일부 entry들을 TLB에 적재
    - 이때 최근에 사용된 page들에 대해서 entry를 TLB에 저장
- 이때 왜 하필 최근에 사용한것을 TLB 에 올릴까요? 그것은 바로 Locality (지역성) 때문입니다.
  - 프로그램의 수행과정에서 한번 접근한 영역을 다시 접근 (temporal locality) 또는 인접 영역을 다시 접근(spatial locality) 할 가능성이 높기 떄문입니다!

> 구동 방식

- 프로세스의 PMT가 TLB에 적재되어 있는지 확인하는 프로세스가 추가하게 됩니다.
- (1) PMT 의 엔트리가 TLB에 적재되어 있는 경우, Associate mapping 쓰면 됨
  - residence bit를 검사하고 page frame번호 확인
- (2) PMT 의 엔트리가 TLB에 적재되어 있지 않은 경우, Direct Mapping 쓰면 됨
  - Direct mapping으로 page frame 번호 확인
  - 최근에 사용했으므로 해당 PMT entry를 TLB에 적재함

---

**Reference**

- <https://www.youtube.com/watch?v=_gNeoGQx-Tc&list=PLBrGAFAIyf5rby7QylRc6JxU5lzQ9c4tN&index=8>



