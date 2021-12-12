---
title:  "Experiments Settings"
excerpt: "환경 구성하기"
categories:
  - DBeaver
last_modified_at: 2021-12-06

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

# [Experiment Settings](#link){: .btn .btn--primary}{: .align-center}

> ## 단축키 수정하기

- Dbeaver 를 실행할때 대표적으로 짜증나는게 실행 (Ctrl + Enter) 입니다. 맥의 경우 Option + Enter 를 잘못 누르는 경우가 많은데, 이 경우에 두개가 충돌이 일어나는 경우도 있죠...
- Deveaber $\to$ Preference $\to$ User Interface $\to$ 키

.![jpg](/assets/images/Program/42_1.jpg)

- 위와 같이 표시되는 hotkey 들을 

> ## 라인 표시

.![jpg](/assets/images/Program/42_2.jpg)

- 위와 같이 라인 표시될 행에 대해서 행 번호 표시를 누르면 됩니다.

> ## 자동으로 소문자 $\to$ 대문자 로 고치기

- 파일 > 설정 > 편집기 > SQL 편집기 > SQL 포맷 설정 > Keyword case > Upper를 Default에서 Upper로 변경합니다.

![jpg](/assets/images/Program/42_3.jpg)

- 위처럼 Upper 로 고치면 자동으로 SQL 쿼리를 대문자로 변형해줍니다.

> ## 테이블 별칭 자동완성

- SQL 의 경우 자동 테이블 별칭 기능이 있긴 한데, 이게 여간 귀찮은게 아닙니다. 
  - 왜냐하면 아래와 같이 SQL 을 작성하다보면 자꾸 새롭게 별칭이 붙게 되는데 이는 우리가 원하는 별칭이 아닐 수 있거든요

```sql
SELECT *
FROM employees e ; -- 엥? 자동으로 별칭이 붙었네
```

- 그러므로 아래와 같이 이러한 별칭을 수정할 수 있습

![jpg](/assets/images/Program/42_4.jpg)

---

**reference**

- <https://goddaehee.tistory.com/284>





