---
title:  "트렌섹션"
excerpt: "트렌섹션"
categories:
  - SQL_Basic_Knowledge
tags:
  - 1
last_modified_at: 2021-05-09

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# <center><font size="15">트렌섹션이란</font></center>

- 트랜잭션이란 데이터베이스의 DML(삽입, 갱신, 삭제) 와 관련된 논리적인 작업을 말한다.
- 데이터베이스의 데이터 무결성이 보장되는 상태에서 DML 작업을 완수하기 위한 기본 작업 단위이다.
- 다음과 같은 예시를 들어봅시다.

> -잔액이 100만원인 A 계좌가 있다. A계좌에서 B계좌로 10만원을 이체한다고  하자. 그러면 A 계좌에서는 10만원이 빠져나가고 B 계좌에서는 10만원이 더해져야한다. 하지만 계좌 이체 도중에 장애가 생기면 어떻게 해야할까? 어느 계좌에 속하고 있어야 할까?

- 위와 같은 이슈에 대해 필요한 대응 논리가 트랜잭션이다. 
- 일반적으로는 DML 의 실행과 실행에 대한 커밋/롤백까지를 트랜색션이라 하지만 실무에서는 데이터베이스에서 SELECT 문구로 데이터를 조회 / DML 실행 / 종료 까지의 모든 과정을 트랜잭션이라 부른다.

![png](/assets/images/SQL_Basic/11_1.png)

- 특징은 아래와 같다. 
