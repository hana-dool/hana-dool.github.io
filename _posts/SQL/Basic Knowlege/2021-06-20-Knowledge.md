---
title:  "기초 지식"
excerpt: "관계형 데이터베이스의 기초 지식"
categories:
  - SQL_Basic_Knowledge
tags:
  - 1
last_modified_at: 2021-06-20

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# <center><font size="15">뷰</font></center> 

- 뷰는 테이블과 유사하지만, 실제 데이터가 없는 테이블을 바라봅니다.
- 테이블에 직접 접근하는것이 아닌, 테이블에서 사용자가 필요로 하는 부분만 선택하여 만들어 놓은 데이터의 집합입니다. 
- 테이블이 아닌 뷰를 이용하는 이유는, 사용자의 편의와 데이터베이스 보안 때문입니다. 
  - 원본 테이블에 들어가지 않아도 사용자가 임의의 뷰를 구성하여 별도의 이름을 붙이고, 테이블을 구성할 수 있습니다.
- 이렇게 한다면 원본을 안전하게 유지하면서, 사용자에게 적절한 데이터를 제공할 수 있습니다.
- 또한 복잡한 SQL 문을 계속 작성하지 않아도 됩니다. 

<br>

