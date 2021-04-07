---
title:  "background image"
excerpt: "배경 이미지 좌표 찾기"
categories:
  - Tab_Map
tags:
  - 3
last_modified_at: 2021-04-06

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---



시각화를 Map 위에서 하면 좋겠지만, 모든 시각화가 그렇게 진행되지는 않는다. 예를 들면 지하철 노선의 경우, 지도 위에 흩뿌리는것보다 잘 구성된 노선도 이미지 위에 정보를 뿌리는게 더 간단하고 보기 좋을때가 많다. 이러한 시각화를 위해서는, 직접 배경이미지를 추출하고, 그 위에 좌표를 매핑해야 할 것이다. 이를 위한 과정은 다음과 같은 여러 단계로 구성된다.

1. 우리가 흩뿌리고자 하는 이미지를 추출한다.
2. 이미지 위에 매핑하고자 하는 Table 을 구성한다. 이 떄, 이 테이블 위에는 각각의 이름과, 그에 해당하는 X좌표, Y 좌표열을 구성해야한다. 
   - X,Y 좌표를 어떻게 아냐고 물을 수 있는데, 이 떄에는 그냥 x,y 좌표는 빈 열로 구성하면 된다. 나중에 Tableau 에서 빈 곳을 채울것이다.
3. 데이터를 테블로에 올리' '고, 이미지를 background 로 설정한다. 
4. 태블로에서 이미지의 좌표를 하나하나 구한 뒤에, 엑셀의 x,y 좌표에 옮겨담는다.
5. 완성된 엑셀을 다시 불러와 이미지와 매핑한다.

위의 과정이 한눈에 들어오지 않을것이다. 아래 예시를 살펴보며 더 알아보자. 우선 우리가 시각화 할 그림과 데이터는 아래와 같다.

![png](/assets/images/Tab_Map/4_1.PNG)

![png](/assets/images/Tab_Map/4_2.PNG)

이제 이 데이터와 그림을 매핑할 것이다.

## 1. 좌표 테이블 만들기

아래 그림과 같이 좌표의 이름과(이름은 굳이 하나가 아니여도 됨. ) x,y 축을 생성한다. 이때 x,y 축의 좌표는 모르는게 당연하다. 여기서의 좌표값은 지구의 좌표값이 아니라, 이미지 위에서의 좌표값이기 때문이다. 그러므로 우선 모두 1로 채워넣자.

![png](/assets/images/Tab_Map/4_3.PNG)

위의 Table 을 Tableau 와 연결하자.  그리고 Map -> Background images 로 이동한다.

## 2. 테이블과 이미지 연결하기

![png](/assets/images/Tab_Map/4_4.PNG)

그러고 니서 Add image -> browse -> 우리가 매핑할 이미지 순으로 선택하자.

![png](/assets/images/Tab_Map/4_5.PNG)

그러면 아래 그림과 같이 Xfiled , y filed 값이 될 필드를 우리 데이터에서 매핑해야 한다. 이는 우리가 설정한 X, Y 값으로 넣자.

![png](/assets/images/Tab_Map/4_6.PNG)

그러고 나서 Options 에서 Always show Entire image 를 체크하자. 이미지가 작으면 뭐하겠는가? 걍 꽉 차게 보여주자~

![png](/assets/images/Tab_Map/4_7.PNG)

그 이후에 우리가 설정한 X, Y 좌표를 col / row 선반 위에 올리자. 그러면 맵이 나타나게 된다. 

![png](/assets/images/Tab_Map/4_8.PNG)

이제 아래 그림과 같이 Point 를 만들어주어야 한다. annotate 에서 POint 를 생성하자.

![png](/assets/images/Tab_Map/4_9.PNG)

그러면 아래 그림과 같이 x,y 좌표를 나타내는데, 이 값의 크기를 키워주자(좀 더 잘보이게)

# 3. 좌표 노가다 하기

![png](/assets/images/Tab_Map/4_10.PNG)

그러면 아래 그림과 같이 위치에 대한 좌표값이 매핑되는것을 볼 수 있다. 점을 옮겨가면서 다른곳의 좌표는 어떨지 알아볼 수 있다.

![png](/assets/images/Tab_Map/4_11.PNG)

옆 정거장은 어떨까? 좌표를 옮겨가면서 살펴보자.

![png](/assets/images/Tab_Map/4_12.PNG)

위와 같이 노가다로 엑셀에 한땀한땀 값을 붙여넣자. 그 이후에 데이터를 연결하면 다음과 같다.

# 시각화 하기

![png](/assets/images/Tab_Map/4_13.PNG)

이제 이 데이터를 가지고 replace data source 를 하자. (또는 그냥 앞의 전철을 그대로 밟아도 된다.)

![png](/assets/images/Tab_Map/4_14.PNG)

이제 Line 을 색깔로 올려보면 잘 구성되었음을 알 수 있다.

![png](/assets/images/Tab_Map/4_15.PNG)





