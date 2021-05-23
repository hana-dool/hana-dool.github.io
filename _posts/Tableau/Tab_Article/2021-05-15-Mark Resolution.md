---
title:  "Shape Resolution Trick"
excerpt: "태블로의 Shape 화질 저하문제를 해결하는 Trick"
categories:
  - Tab_Article
tags:
  - 3
last_modified_at: 2021-05-23

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

<br>

> 아래 내용을  tableau 에서 Shape 를 넣게되면 해상도가 작아지는 현상을 해결하는 방법을 다룬 내용입니다. 

- <https://www.flerlagetwins.com/2018/01/image-swapping-in-tableau_97.html> 
- <https://powertoolsfortableau.com/tableau-performance-series-images-shapes>

# <center><font size="15"> Shape 의 문제점 </font></center>

- 우리는 icon 과 함께 시각화를 구성할때에, Shape 를 사용하고는 합니다.
- 하지만 이 shape 자리에 글자, 리뷰 등을 올려보고 싶을것입니다.
  - 그래야함 action 을 추가할 수 있기 뺴문입니다.
- 하지만 해상도가 높은 이미지를 shape 에 추가한다 하더라도, blurry 하게 보이는것을 볼 수 있습니다.
- 아래 이미지에서 Review 가 제가 마크에 넣은 고해상도 사진입니다만 깨져서 보이는것을 볼 수 있습니다.

![png](/assets/images/Tab_Article/7_1.png)

- 즉 위와 같이 고해상도의 이미지는 사용할 수 없는것입니다.

<br>

# <center><font size="15">해결책</font></center>

- 사실 해결책이라고는 하기 힘들고 하나의 꼼수입니다.
- "View 의 배경" 을 이용해서 바꾸는 방식입니다. 

<https://www.flerlagetwins.com/2018/01/image-swapping-in-tableau_97.html>

