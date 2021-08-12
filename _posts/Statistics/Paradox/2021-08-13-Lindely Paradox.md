---
title:  "Lindley's Paradox"
excerpt: "베이즈와 Frequentist 결과가 다르다?"
categories:
  - Stat_Paradox
tags:
  - 1
last_modified_at: 2021-08-11

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# Lindely Paradox

- 한 가게 주인이 전구를 대량으로 받았다고 합시다. 
- 배송을 보낸 회사는 두 유형의 전구 패키지를 보냅니다. 
  - 첫번째 유형 : 50% 는 빨간 전구 
  - 두번째 유형 : 25% 는 빨간 전구
- 이 두종류의 배송은 똑같은 확률로 배송된다고 생각됩니다. 
- 내가 받은 패키지가 어떤 유형인지 알기 위해서 48개의 전구를 검사하였습니다.
  - 이중 36개의 전구가 빨간 전구였습니다. 
- 이 경우에 가게 주인은 어떠한 결론을 내려야 할까요? 
- 직관적으로 생각한다면 당연히 첫번쨰 유형의 패키지일 확률이 높습니다. 

<br>

# Frequentist View 

- 먼저 위 가설을 테스팅 하기 위해서는 귀무가설을 설정해야합니다. 
- 그런데 어떤것을 귀무가설로 설정할지에 따라서 테스트가 2개 있을 수 있으므로 각각을 선택해 보겠습니다. 

<br>

## 귀무가설 : 25% 는 빨간전구

![png](/assets/images/Stat/36_1.png)

- 위와 같이 25% 가 빨간전구라는 가정 하에서는 48개중에서 36개가 빨간 전구라는 사실은 받아들이기 힘듭니다.
- 위처럼 99% Significant range 가 (3,21) 이고 이는 귀무가설 하에서는 우리가 얻은 데이터는 엄청나게 받아들이기 힘들다는 뜻입니다.
- 그러므로 기각하게 됩니다.

![png](/assets/images/Stat/36_2.png)

- 위 그림에서 보다시피, 36 개가 빨간 전구라는 사실은 받아들이기 힘듭니다. 

<br>

## 귀무가설 : 50% 는 빨간전구

![png](/assets/images/Stat/36_3.png)

- 위와 같이 50% 를 가정한 상태에서도 99% 신뢰구간은 (13.5, 34.5 ) 가 됩니다.

![png](/assets/images/Stat/36_4.png)

- 위 그림에서 보다시피 50% 의 귀무가설도 기각하게 됩니다. 

<br>

## 둘다 기각..?

- 위를 보게되면 우리는 25% / 50% 두가지 경우 모두 기각을 하게 되었습니다.
- 이는 결국 아무것도 결정할 수 없다는 것일까요? 

![png](/assets/images/Stat/36_6.png)

- 이는 위 그림에서 보다시피 우리가 얻은 48개중 36개의 빨간 전구 데이터는 어떠한 귀무가설에서도 일어나기 힘든 사건이였습니다. 
- 이는 NHST 의 p-value 는 단지 'Null Hypothesis' 입장에서만 바라보면서 얻은 값일뿐 Alternative Hypothesis 의 입장은 하나도 고려하지 않았기 떄문에 일어나는 현상입니다. 

<br>

# Bayesian View

![png](/assets/images/Stat/36_7.png)

- 베이즈 정리에서는 위와 같이 Test 를 수행할 수 있습니다. 
- 데이터를 만나 우리의 Posterior 데이터가 업데이트되고 나면 , 두번쨰 유형 (50% 가 빨간전구) 일 확률이 99.99999% 가 되는것을 볼 수 있습니다.
- 이는 베이즈의 경우는 'Alternative' 의 정보까지 Inference 에 넣기 때문에 더 정확한 결과가 나온것 입니다.
- 이러한 결과때문에 베이즈 통계학자들이 NHST 를 공격하기도 합니다. 

<br>

# Summary

![png](/assets/images/Stat/36_8.png)

![png](/assets/images/Stat/36_9.png)

<br>



# Reference

- https://jonathanweisberg.org/vip/chlindley.html
- https://www.youtube.com/watch?v=ynfHFClgwOo
- https://en.wikipedia.org/wiki/Lindley%27s_paradox

