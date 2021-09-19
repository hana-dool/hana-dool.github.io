---
title:  "1-3 Class inheritance and Overiding"
excerpt: "클래스를 상속하거나, 메서드를 다시 정의하기"
categories:
  - Py_Advanced
last_modified_at: 2021-09-19

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"

use_math : true
---

 아마 비전공자라면, 파이썬의 Class 까지 심도있게 다룬 사람은 별로 없을것입니다. 하지만 파이썬에서 Class 는 매우 중요한 위치를 가집니다. 이러한 Class 에 대해서 알아보고 어떻게 활용할 수 있는지 알아봅시다.
{: .notice--warning}

# [클래스의 상속](#link){: .btn .btn--primary}{: .align-center}

- 클래스의 상속이란, 물려받는다는 의미로, 다른 클래스의 기능을 물려받는것입니다. 

> class 클래스 이름(상속할 클래스 이름)

- 위와 같이 실행하게 된다면, 상속할 클래스의 모든 기능을 사용할 수 있게됩니다.

```python
class newcal(FourCal):
    pass
a = newcal(4,2)
a.add() # 6
```

- 위처럼, newcal 은 아무런 method 를 정의하지 않았음에도, add 같은 메서드를 쓸 수 있습니다. 

> 왜 해야되나요?

- 보통 상속은 기존 클래스를 변경하지 않는 선에서 기존 기능을 변경하고자 할 때에 사용합니다. 
- 기존의 Class 를 변경하고싶지 않는 선에서 시험하고싶을떄에 사용하게 됩니다.

<br>

# [메서드 오버라이딩](#link){: .btn .btn--primary}{: .align-center}

```python
class SafeFourCal(FourCal):
    def div(self):
        if self.second == 0:  # 나누는 값이 0인 경우 0을 리턴하도록 수정
            return 0
        else:
            return self.first / self.second
```

- 기존의 FourCal 에 div 라는 메서드를 구현했엇는데, 0으로 나누는 경우를 고려하지 않아 에러가 났다고 합시다.

- 위처럼 기존의 div 메서드를 동일한 이름으로 '다시' 만드는것을 메서드 오버라이딩(덮어쓰기) 라고 합니다.

<br>

# 클래스 변수

- 객체변수는 다른 객체들에 영향받지 않고 독립적으로 그 값을 유지합니다.
  - 이 이유는 독립된 Name Space 에서 행동하기 떄문입니다.

```python
class ex:
    name = 'han'
```

- 위와 같이, class 안에서 self. 을 통해서 이름을 정의한게 아니라 바로 정의했다고 합시다.

```python
a = ex()
b = ex()
print(a.name) # han
print(b.name) # han 
ex.name = 'park'
print(a.name) # park
print(b.name) # park 
```

- 위처럼, 클래스 변수값을 변경하니 모두 값이 바뀌는것을 볼 수 있습니다. 

---

**reference**

- <https://wikidocs.net/85>

