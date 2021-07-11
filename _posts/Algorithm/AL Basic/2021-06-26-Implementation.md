---
title:  "구현"
excerpt: "아이디어를 코드로 바꾸기"
categories:
  - AL_Basic
tags:
  - 1
last_modified_at: 2021-06-26

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# <center><font size="10">구현</font></center>

- 코테에서 구현이란 머릿속에 있는 알고리즘을 소스코드로 바꾸는 과정이다. 
- 어떤 문를 풀건간에, 소스코

<br>

# 거스름돈

![png](/assets/images/Python/3_1.png)

```python
M = int(input())
m = 1000 - M
lis = [500,100,50,10,5,1]
cnt = 0
for i in lis:
    if int(m) != 0 :
        cnt += m // i
        m = m % i
print(cnt)
```

- 하지만 그리디 알고리즘은 모든 문제에 적용가능한것은 아니다. 
- 왜냐하면 Local minimal 이 Global 한 답이 되지는 않기 때문이다. 

<br>

