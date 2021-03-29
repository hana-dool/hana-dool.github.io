---
title: "local/global 변수에러"
excerpt: "UnboundLocalError local variable referenced before assignment"
categories:
  - Py_Basic
tags:
  - 3
last_modified_at: 2021-02-18

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

# 에러

![png](/assets/images/{Error}/2_2.jpg)

- 위와 같이 global 변수를 쓸 때에 에러가 나는 경우가 있다.
- 그런데 위쪽 cell 과 아래쪽 cell 을 보면 위와 아래가 거의 같아 보이는데 아래쪽만 에러가 나고있다 왜 그럴까?
- 이런 에러가 나는 이유는 변수 할당에 있다.

![png](/assets/images/{Error}/2_1.jpg)

- 위 그림을 보면 파이썬의 Namespace 공간이 나온다.

- 여기서 주의깊게 봐야하는것은 할당이다.

  - z += 100 이라는 할당이 이루어지는데 기존 global 변수 z 에 대해 새로운 값을 할당하는 셈이다. 그런데 컴파일러는 이 연산이 def 안에서 이루어지고 있으므로 이를 로컬 변술 인식하게 된다. 

  - 즉 add 함수 안에서(local name space) 초기화 되지 않은 로컬변수 z 를 할당하려고 하기 떄문에 오류가 발생한다.

# 해결

![png](/assets/images/{Error}/2_3.jpg)

- 위와 같이 global 을 선언해 주어서, namespace 가 헷갈리지 않게 지정을 해 주어야 한다. 

