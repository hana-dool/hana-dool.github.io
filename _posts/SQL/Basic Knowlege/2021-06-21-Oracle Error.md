---
title:  "Oracle Error"
excerpt: "오라클에서 발생하는 에러에 대해서 알아보자"
categories:
  - SQL_Basic_Knowledge
tags:
  - 1
last_modified_at: 2021-06-21

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# ORA-00937: 단일 그룹의 그룹 함수가 아닙니다.

## 그룹함수와 일반 함수가 섞여서 들어있는 경우

![png](/assets/images/SQL/3_1.png)

- 위와 같이 에러가 발생하게 됩니다. 
- 그 이유는 간단합니다. 왼쪽은 그냥 col 인데, 오른쪽은 집계값이라 그 수준이 맞지 않는것입니다. 
- 이 경우 우리 의도에 따라서 몇가지 해결책이 있습니다. 

<br>

1. Groupby 를 통해서, 둘의 수준 맞추기 
   - 아래와 같이 Groupby 를 하게되면 ename 기준으로 sum 이 적용되고, 두 수준이 맞아집니다. 

![png](/assets/images/SQL/3_2.png)

2. over() 를 통하여 둘의 수준 맞추기
   - 아래와 같이 over 을 sum 함수에 적용합니다. 
   - over 함수는 분석함수에 적용되어, over 안의 데이터에 계속 적용됩니다. 
   - 이 경우는 over 안에 아무것도 없으므로, 각 sum 마다 모든 데이터의 합이 적용되 같은 값을 보여주고 있습니다.

![png](/assets/images/SQL/3_3.png)

<br>

# ORA-00918 : 열의 정의가 애매합니다

- 어느 테이블의 컬럼인지 정확하게 파악이 안되는경우에 발생한다. 
- 테이블 조인시에 많이 발생한다. 
- 주로 "컬럼의 이름이 겹칠때" 발생한다. 
