---
title:  "Data(Panel)"
excerpt: "태블로의 데이터페널에 대해서"
categories:
  - Tableau
tags:
  - 3
last_modified_at: 2021-02-14

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

# 설명글 추가

- 각 필드에 필드를 설명하는 설명글을 추가할 수 있다.

  - Default property -> Comment 를 들어가자.

  ![png](/assets/images/Tableau/9_1.PNG)

- 그 이후에 추가할 내용을 써 넣는다.

  ![png](/assets/images/Tableau/9_2.PNG)

- 그러면 마우스를 올려놓기만 해도, 내가 써 놓은 내용을 볼 수 있다.

  ![png](/assets/images/Tableau/9_3.PNG)

---

# 폴더화

- 필드 항목들을 폴더로 grouping 해서 가시성을 높힐 수 있다.

- 데이터 페널은 기본적으로 가나다 순 정렬이 되어있다.

  ![png](/assets/images/Tableau/9_4.PNG)

- 이제 데이터 페널의 ▼를 클릭한 이후 folder 정렬을 선택한다.

  ![png](/assets/images/Tableau/9_5.PNG)

- 그 이후 데이터 페널의 이름이 Table 에서 Folder 로 변경된 것을 볼 수 있다.

  - 이 상태에서 묶고싶은 변수들을 모아서 폴더를 만든다.

  ![png](/assets/images/Tableau/9_6.PNG)

  ![png](/assets/images/Tableau/9_7.PNG)

- 그러면 아래와 같이, 변수들이 폴더로 묶여 구분되는것을 볼 수 있다.

  ![png](/assets/images/Tableau/9_8.PNG)

---

# 숨기기/숨기기취소

- 쓰이지 않는 필드의 항목들을 숨겨서 깔끔하게 만들 수 있다.

**숨기기**

- 다음과 같이 고유 id는 쓰이지 않기 때문에 숨기고 싶다고 하자.

  - 우선 필드를 오른쪽 마우스로 클릭 후(Mac 은 crtl 클릭) Hide 를 하자.

  ![png](/assets/images/Tableau/9_9.PNG)

- 그러면 다음과 같이 없어진것을 볼 수 있다.

  ![png](/assets/images/Tableau/9_10.PNG)

<br>

**숨기기 취소**

- 데이터 페널의 ▼를 클릭한 이후 show Hidden field 를 클릭한다.

  ![png](/assets/images/Tableau/9_11.PNG)

- 그러면 아래와 같이 숨겼던 필드가 연한 회색의 슬씨로 드러난다.

  ![png](/assets/images/Tableau/9_12.PNG)

- 이제 이 필드에 대해서 Unhide 를 지정하자.

  - 그러면 다시 색이 진해지며 숨겨짐이 풀리게 된다.

  ![png](/assets/images/Tableau/9_13.PNG)

---

# 계층

- 필드가 서로 상하관계가 명확한 경우(시/도 와 시군구) 계층을 만들어서 시각화를 할 떄에 각 수준을 빠르게 드릴다운 할 수 있도록 할 수 있다.

**생성**

- '제품' 들에 대해서 계층을 형성하고 싶다고 하자. 

  - 계층을 만드는것은 쉽다. 마우스로 끌어서 겹치게만 하면 된다.

  ![png](/assets/images/Tableau/9_14.PNG)

- 그러면 아래와 같이 계층이 형성된다.

  ![png](/assets/images/Tableau/9_15.PNG)

- 계층의 순서는 위로 갈수록 큰 범위여야 한다. 

  - 그래야한 드릴다운을 할 때에 점점 하위 개념으로 수준을 바꾸게 되기 때문
  - 순서를 바꾸는것도 필드를 클릭한뒤 옮기기만 하면 된다.

  ![png](/assets/images/Tableau/9_16.PNG)

<br>

**제거**

- 데이터 패널에서 마우스 오른쪽을 클릭하고 계층 제거를 하면 된다.

  ![png](/assets/images/Tableau/9_17.PNG)

---

# 그룹

- 그룹이란 어떤 차원에 속하는 값 중 둘 이상의 결합을 의미한다.
  
  - 위에서 '폴더' 는 차원을 묶은것이고, 그룹은 '차원 안의 값들' 을 묶은것다.
  
- 그룹은 어느때에 사용할까?
  
  - 시각화를 할 때 구분되는 범주가 너무 많으면 색을 많이 써야되서 난잡하다. 이럴때에 그룹을 사용해서 범주를 통합한다.
  
- 아래에서 제품 중분류의 범주가 너무 많아 그 경향이 제대로 보이지 않고있다.

  - 그래서 제품 중분류에서 Group 을 생성하자.

  ![png](/assets/images/Tableau/9_18.PNG)

- 전기제품과 나머지로 Group 을 생성했다.

  ![png](/assets/images/Tableau/9_19.PNG)

- Grouping 의 제목을 맞게 붙여준다.

  ![png](/assets/images/Tableau/9_20.PNG)

- 이때 나머지것들을 모두 통합할 때 Include 'Other' 을 쓰면 손쉽게 가능하다.

  ![png](/assets/images/Tableau/9_21.PNG)

- 이제 우리가 새로 만든 그룹이 클립 모양으로 데이터 페널에 나타난다.

  - 이를 Marks 에서 Color 에 넣게되면 한눈에 그 추이가 보이게 된다.

  ![png](/assets/images/Tableau/9_22.PNG)



- (note) 아래처럼 뷰 안에서 바로 Grouping 이 가능하다.

  ![png](/assets/images/Tableau/9_23.PNG)

---

# 집합

- 집합도 그룹핑과 비슷하다. 많은 범주들을 통합해서 간단하게 만들 수 있다.
  - 하지만 집합은 좀 더 자유롭게 선택이 가능하다. Top 10 매출만 고르거나 , 상위 20% 값만 선택 등이 가능.

- 집합은 '차원(파란색)' 변수에 대해서만 적용이 가능하다.

**list 에서 선택**

- 아래와 같이 제품명에 대해서 차원을 생성해 보자.

  - list 에서 선택하는 방법이다.
  - select from list : 손수 하나하나 지정해주는것
  - Costom value list : 들어가는 값, 문자를 이용해 지정 가능

  ![png](/assets/images/Tableau/9_24.PNG)

**Condition 으로 선택**

 - field 에 대해서 Min, Max, larger 등의 조건을 통해 선택 가능

   ![png](/assets/images/Tableau/9_25.PNG)

**Top/Bottom 선택**

 - Top/Bottom 으로 n 개의 데이터를 볼 수 있다.

   ![png](/assets/images/Tableau/9_26.PNG)

<br>

- 새로운 집합을 형성하고, 필터로 적용하게 되면 in/out 이 옆에 나타나게 된다.

  - in : 내가 설정한 조건(선택) 에 맞는 집합
  - out : 내가 설정한 조건에 맞지 않는 집합

- 아래의 경우 매출이 100만 이상이라는 조건을 건 집합을 이용한 표이다.

  ![png](/assets/images/Tableau/9_27.PNG)

  







