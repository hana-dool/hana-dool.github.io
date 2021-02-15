---
title:  "View(Tooltip)"
excerpt: "Tooltip 을 통해 도구설명 안에 View 를 만들어보자"
categories:
  - Tableau
tags:
  - 3
last_modified_at: 2021-02-15

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

- 뷰를 만들고 난 이후에, 데이터에 대한 자세한 정보를 마우스 오버를 통해 바로 알려주고 싶다면 도구설명 Visualization 을 추가하면 된다.

- Tooltip 은 일종의 필터로서, 마우스 오버로 올린 범주에 대해 필터를 추가한 Visualization 을 보여주는 형식이다.

  ![png](/assets/images/Tableau/13_1.png)

# How to?

- 1.테블로의 워크시트 뷰에서 도구설명 Visualization 이 될 뷰를 만든디.
  - 이때 도구로 이용된다는것을 알려주기 위해, 도구설명 Vis 가 되는 워크시트임을 알려주기 위한 제목을 설정하는것이 좋다.
- 2.원본 워크시트에서 마크카드에서 Tooltip 을 클릭한다.
  - 도구 설명 에디터에서 도구설명 Vis 가 되는 워크시트에 대한 참조를 삽입한다.
- 3.잘 나오는지 테스트 하며 높이/크기 등을 변경하며 조절한다.



# Tooltip 구성하기

- 1.tooltip 이 될 Vis 만들기

  ![png](/assets/images/Tableau/13_2.png)

- 2.시각화가 올라올 원본 시트에서 tooltip 구성하기

  - tooltip을 클릭한다.

  ![png](/assets/images/Tableau/13_3.png)

  - tooltip 에서 Sheet 를 추가로 넣는다.

  ![png](/assets/images/Tableau/13_4.png)

- 3.마우스를 올렸을 때에 우리가 원하는 느낌으로 Tooltip 이 구성되었음을 볼 수 있다.

  ![png](/assets/images/Tableau/13_5.png)



# Tooltip 크기변경

- 사실 위의 Visualization 에을 보면 view is too large to show 라고 해서, view 는 큰데, 그것을 보여주는 tooltip 이 너무 작다고 하는것을 볼 수 있다.

- 즉 이를 조절하기 위해서 새로 tooltip 으로 들어가서 maxwidth 와 maxhight 를 조절하자.

  ![png](/assets/images/Tableau/13_6.png)

- 이제 비로소 경고 메세지가 뜨지 않도 모든 Visualization 이 잘 나옴을 볼 수 있다.

  ![png](/assets/images/Tableau/13_7.png)



# 뒤처리

- 이제 tooltip 에 쓰인 워크시트를 Hide 처리한다.

- 워크시트를 다시 보이게 하려면, 아무 워크시트나 선택한 이후, 오른쪽 클릭 후 Unhide 를 해 주면 된다.



# Ex

- Tooltip 도 아무 관련없는 데이터를 놓으면 되는게 아니라 관련있는 데이터를 놓아야 한다.

- 다른 세부 수준의 데이터

  ![png](/assets/images/Tableau/13_8.png)

- 관련이 있는 다른 데이터

  ![png](/assets/images/Tableau/13_9.png)

- 시간따라 변화하는 양상

  ![png](/assets/images/Tableau/13_10.png)

- 여러개의 tooltip 추가

  ![png](/assets/images/Tableau/13_11.png)

- 다양한 세부정보(table)

  ![png](/assets/images/Tableau/13_12.png)