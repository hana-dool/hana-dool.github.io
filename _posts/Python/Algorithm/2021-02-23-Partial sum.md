---
title:  "부분집합 구하기(DFS)"
excerpt: "Algorithm"
categories:
  - Py_Algorithm
tags:
  - 3
last_modified_at: 2021-02-23

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

- 문제 및 답 출처 : [링크](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8/dashboard)

- 해당 링크에 가시면 훨씬 더 전문적인 해설 및 / 강의를 보실 수 있습니다. 

# 문제

**문제**  

자연수 N 이 주어지면 1부터 N 까지의 원소를 갖는 집합의 부분집합을 모두 출력하는 프로그램을 작성하라.

**입력설명**

첫 줄에 자연수 N이 주어진다. 

**출력 설명**

- 첫 번째 줄부터 각 줄에 하나씩 부분집합을 아래와 출력 예제와 같은 순서로 출력한다. 단 공집합은 출력하지 않습니다.

**입력 예제**

3

**출력예제**

1 2 3

1 2 

1 3

1

2 3

2

3

# 내 해답

