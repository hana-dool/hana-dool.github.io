---
title:  "Sympson Paradox"
excerpt: "각 집단에서의 관계는 전체 집단에서의 관계를 말해주지 않는다"
categories:
  - Stat_Paradox
tags:
  - 1
last_modified_at: 2021-08-13

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# Sympson Paradox

- 솔직히 너~무 유명한 Paradox고, 이에 관한 Article 은 넘쳐나서 그냥 하나의 사진으로 퉁치겠습니다.

![png](/assets/images/Stat/37_2.png)

![png](/assets/images/Stat/37_1.png)

- 위와 같이, 부분적으로는 모두 앞설이라도 전체적으로 합치고보면 확률이 다른경우가 있습니다. 
- 이는 각 부분에서 비율이 다르기떄문에 나타나는 에러입니다. 

<br>

# Experiment Settings 

- 이러한 에러는 실험계획에서 잘 나오지는 않습니다.
  - 왜냐하면 실험계획이 잘 된다면 'Random' 이 잘 정의된다는것이고, 그렇다면 이러한 그룹간의 불균형이 덜 생기기 때문입니다. 
- 그럼에도 조심해야하는것은, 아무리 랜덤을 설계하더라도, 한 사람에게는 많은 속성이 존재하여 불균형이 나타날 수 있다는 것입니다.
  - 사람은 성별 / 체중 / 학력 .... 등등 많은 속성이 존재합니다. 
  - 단순히 체중 , 학력 만 Random 성을 신경쓴다면 위 예시처럼 성별의 불균형이 나타날 수 있다는것입니다. 
- 즉 실험 데이터를 받는다면 그 속성들로 Groupby 를 하면서 혹시 이러한 Sympson Error 가 나타나지는 않았는지 살펴야합니다.

<br>

# Summary 

![png](/assets/images/Stat/37_3.gif)

- 정리하자면 위와 같습니다. 각 집단에서의 관계는 전체 집단에서의 관계를 말해주지 않습니다.

