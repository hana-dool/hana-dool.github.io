---
title:  "지역별 매출 DashBoard"
excerpt: "기본으로 제공하는 슈퍼스토어 데이터에 대한 대시보드"
categories:
  - Tab_Dash
tags:
  - 3
last_modified_at: 2021-05-08

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

# Intro

벌써 태블로를 조금씩 공부한지 약 4개월이 되었다. (처음 사용은 훨씬 전이지만, 꾸준히 공부하게된건 4개월) 이제 슬슬 대시보드를 구성하기 위한 준비가 다 되었다고 생각해서, 태블로에서 제공하는 기본 Super Store 에 대한 시각화를 진행해 보았다. 처음부터 대시보드를 구성하기에는 무리가 있기 떄문에, 다른사람이 미리 만들어놓은 대시보드의 구성을 최대한 활용하였다.

- https://www.youtube.com/channel/UCdXTfbW26jVkQzqjsRO6JOg # 대시보드 구성
- https://icooon-mono.com/ # 아이콘
- https://www.figma.com/ # 레이아웃
- https://public.tableau.com/profile/lovelytics#!/ # 대시보드 디자인 아웃라인

<br>

<br>

# Template 구성

먼저 figma.com 에서 태블로 대시보드의 기본이 될 Template 을 생성해야 한다. 아래와 같이 구성을 해보자. 먼저 사각형을 생성해 준다.

![png](/assets/images/Tab_Article/4_1.png)

그 이후에 모서리를 깎아준다. 이 설정은 노랗게 칠한 부분을 움직이거나, 값을 조정함으로서 해볼 수 있다.

![png](/assets/images/Tab_Article/4_2.png)

색을 조절해준다. 우리의 대시보드에 맞게 색을 구성하자.

![png](/assets/images/Tab_Article/4_3.png)

그 이후에 Shadow 효과를 넣어보자. 

![png](/assets/images/Tab_Article/4_4.png)

여러 작은 상자들을 구성하고, 색을 바꾸자.

![png](/assets/images/Tab_Article/4_5.png)

![png](/assets/images/Tab_Article/4_6.png)

규격을 맞추며 대시보드를 생성해보면 이 그림과 같아진다. 

![png](/assets/images/Tab_Article/4_7.png)

그리고 옆에 '지역' 별로 필터를 걸어서 결과를 보고싶기 때문에, 구역을 나누어보자. 

![png](/assets/images/Tab_Article/4_8.png)

그 이후에 "선택" 하였을때에, 모양이 바뀌게 하고싶기 떄문에 아래와 같이 모서리를 세밀하게 다듬어주자.

![png](/assets/images/Tab_Article/4_9.png)

그 이후에 모양을 추가한 이후 회전시키고 겹친다. 그 이후에 Group Selection 을 통해 하나의 모양으로 합친다.

![png](/assets/images/Tab_Article/4_10.png)

![png](/assets/images/Tab_Article/4_11.png)

![png](/assets/images/Tab_Article/4_12.png)

![png](/assets/images/Tab_Article/4_13.png)

이제 위와 같이 페이지를 하나 더 만들고, 형성한 아이콘들을 이곳으로 옮긴다. 

![png](/assets/images/Tab_Article/4_14.png)

![png](/assets/images/Tab_Article/4_15.png)

이제 우리가 형성한 탬플릿을 밖으로 내보낼 차례이다. 아래와 같이 Export 를 통해서 이미지 파일로 내보낸다. 

![png](/assets/images/Tab_Article/4_16.png)

모양의 경우에 각각 따로 내보내자. 모양을 선택한 후에 각각 내보내면 된다. 

![png](/assets/images/Tab_Article/4_17.png)

그리고 내보낸 아이콘을 아래와 같이 내 Tableau 리포지토리에 추가한다. 

![png](/assets/images/Tab_Article/4_18.png)

![png](/assets/images/Tab_Article/4_19.png)

그리고 내 탬플릿을, 대시보드위에 올려놓자. 그 이후에 우리가 이미지를 만들때 사용했던 사이즈와 똑같게 사이즈를 조절하자. 

![png](/assets/images/Tab_Article/4_20.png)

![png](/assets/images/Tab_Article/4_21.png)

그 이후에 아래와 같이 Layout 에서 Margin 을 조절하자. 

![png](/assets/images/Tab_Article/4_22.png)

<br>

<br>

# View 구성

아래와 같이 다양한 시각화들을 구성해보자. 텍스트의 경우, Entire view 의 상태에서 Text Mark 를 선택하고, 시각화하고 싶은 정보를 넣으면 된다. 이 떄에 아래와 같이 column 의 격자, Row divisor 등의 구분선은 없앤 상태이다. 

![png](/assets/images/Tab_Article/4_23.png)

그리고 표도 구성해 보았다. 이 떄에 중요한것은 "각각의 View 는 깔끔" 해야한다는 것이다. 그러므로 Row divisor 정도만 남기고, 다른 부분은 모두 깔끔하게 수정하였다.

![png](/assets/images/Tab_Article/4_24.png)

그리고 제일 중요한 "지역 구분" 의 VIew 를 구성해 보겠다. 아래와 같이 지역을 올려놓고, Shape 를 선택하자.

![png](/assets/images/Tab_Article/4_25.png)

그 이후 우리가 추가한 Custom 의 마크에 추가한 모양을 추가하자. 

![png](/assets/images/Tab_Article/4_26.png)

이 구분되는 Mark 위에 지역 이름을 넣고싶기 때문에 아래와 같이 Text 에 지역을 추가하자. 

![png](/assets/images/Tab_Article/4_27.png)

그리고 Text 의 Format 을 조절하자. Header 를 숨기고, 텍스트는  왼쪽 정렬로 구성하였다. 이런식으로 하게되면, 이 View 를 대시보드에 추가할때에 지역이 왼쪽으로 잘 보일것이다. 

![png](/assets/images/Tab_Article/4_28.png)

현재 만들어 놓은 모든 View 들을 추가하면 아래와 같다. 이떄에 주의할 점은 각각의 View 에 대해서 , Layout 에서 워크시트의 색깔은 하얀색이 아니라 None 이여야한다는 것이다.

![png](/assets/images/Tab_Article/4_29.png)

<br>

<br>

# 세부 텍스트 조절

위에서 지역의 텍스트를 보면, 나는 왼쪽 위에 오게 하고 싶다. 이럴 경우에 아래와 같이 띄어쓰기, 공백, Alignment 등을 활용하여서 조절하는게 좋다.

![png](/assets/images/Tab_Article/4_30.png)

그렇게 하면 아래와 같이 텍스트가 원하는 위치에 오게 된다.

![png](/assets/images/Tab_Article/4_31.png)

그 이후 총 매출도 추가하면 아래와 같다. 

![png](/assets/images/Tab_Article/4_32.png)

<br>

<Br>

# 매출막대 추가

이 막대는 다른 다양한 DashBoard 구성에도 잘 쓰일만한 것이라 이렇게 주제를 구분하였다. 먼저 아래와 같이 둥근 Barh 그래프를 구성한다. (Tab View 참조) 그리고, Text 에서 Alignment 와 색상 등을 조절하면 된다. 

![png](/assets/images/Tab_Article/4_33.png)

![png](/assets/images/Tab_Article/4_39.png)

그 이후에 위치를 잘 조절하면서 옮기면 아래와 같이 나오게 된다.

![png](/assets/images/Tab_Article/4_34.png)

<br>

<Br>

# 지역 선택창 설정

먼저 아래와 같이 워크시트를 새로 만든다음 검게 설정한다. 이 이유는 '지역 선택' 시 지역구분되는 모양이 변하게 해주고 싶은데, 이 떄에 하얀색 모양으로 구성할 것이기 때문이다. 

![png](/assets/images/Tab_Article/4_35.png)

마크를 추가하고, 우리의 Custom 모양을 추가한다. (하얀색이라 MArk 가 없는것같지만, 있는것이다.)

![png](/assets/images/Tab_Article/4_36.png)

![png](/assets/images/Tab_Article/4_37.png)

![png](/assets/images/Tab_Article/4_38.png)

이 떄에 크기를 조절하고, 텍스트를 검은색으로 수정하자. (우리가 이전에 지역 구분을 만들떄와 똑같이 진행한다고 생각하면 된다. )

![png](/assets/images/Tab_Article/4_41.png)

이제 이를 이쁘게 겹쳐넣으면 아래와 같다.

![png](/assets/images/Tab_Article/4_42.png)

<br>

<br>

# 선택 액션 추가

이제 선택 액션을 추가하고 싶다. 우리는 "투명 선택창" 을 이용해 이를 구현할것이다. 먼저 파워포인트를 키자. 그리고 사각형을 만든다. 

![png](/assets/images/Tab_Article/4_43.png)

이 sheet 를 복사한 뒤에, 같은 모양에 대해서, 채우기가 모두 없는 "투명한 사각형" 을 만든다.

![png](/assets/images/Tab_Article/4_44.png)

그 이후에 그림을 저장하자. (두 사각형 모두)

![png](/assets/images/Tab_Article/4_45.png)

그리고 태블로 모양에 추가한다. (검게 보이는것은, 컴퓨터가 투명한 모양은 기본적으로 검게 출력하기 때문이다.)

![png](/assets/images/Tab_Article/4_46.png)

그리고 아래와 같이 투명 선택장이라는 시트를만들고, 여기에다가 사각형을 추가한다. 

![png](/assets/images/Tab_Article/4_47.png)

이를 필터 액션이 들어갈 부분에 겹쳐넣는다. 파란색 사각형의 영역이 클릭시에 바뀔 영역이다. 즉 이 사각형을 어느정도 기존의 View 와 호환되게 위치를 잡아보자. 

![png](/assets/images/Tab_Article/4_48.png)

그 이후에 투명한 사각형으로 바꾸어준다. 

![png](/assets/images/Tab_Article/4_49.png)

그러면 아래와 같이 사각형도 보이지 않는 투명한 View 가 형성된다. 하지만 여전히 사각형의 영역은 남아있다는것에 주목하자. 

![png](/assets/images/Tab_Article/4_50.png)

이제 대시보드에 Action 을 추가하자.

![png](/assets/images/Tab_Article/4_51.png) 

Source 에 투명선택창만 선택한다. 그리고 Target Sheet 에는, 변해야 되는 시트들만 선택하자. (매출 추이, Total sales 등은 변해야겠지만, 지역별 매출(가로 검은색 바) 는 변하지 말아야 할 것이다.)

![png](/assets/images/Tab_Article/4_52.png)

그러면 최종적으로 아래와 같아진다. 선택된 지역에 대해서 잘 Filtering 이 되고있다. 

![png](/assets/images/Tab_Article/4_53.png)

만약 위가 잘 되지 않는다면 그것은 계층 순서 조절의 문제일것이다. 

<br>

<br>

# 계층 순서 조절

- 아래와 같이 Layout 에서 Item Hierachy 를 보자. 이 경우 투명 선택창이 제일 위에 위치해야한다. 왜냐하면 필터링 되어지는 View 이기 떄문에 '선택이 되어야 하기 때문' 이다. 

- 그리고 지역별 매출(검은색 가로바 )은 그 아래에 위치해야한다. 우리가 어떤 지역을 선택하게 되어서 모양이 바뀌더라도, 지역별 매출은 늘 바뀌지 말아야 하기 떄문이다.
- 그리고 하얀 선택창은 기존의 지역구분(회색 알약 모양) 위에 위치해야한다. 그래야만 선택했을때, 기존의 모양 위에 위치하게 되기 때문이다.
- 기존 선택창(회색모양) 은 맨 아래에 위치한다.

![png](/assets/images/Tab_Article/4_54.png)

<br>

<br>

# icon 추가

아래와 같이 새로 Calculated Field 를 만든다. 이를 만드는 이유는, View 가 아무 차원값 없이는 형성되지 않기 때문

![png](/assets/images/Tab_Article/4_55.png)

이를 View 에 추가하자. 그 이후 Custom icon 을 추가하자. (흰색이라 없는것처럼 보인다. 추가한 순서를 잘 고려해서 감으로 잘 넣자.)

![png](/assets/images/Tab_Article/4_56.png)

![png](/assets/images/Tab_Article/4_57.png)

아래와 같이 커서로 훑다보면 잘 추가된것을 볼 수 잇다.

![png](/assets/images/Tab_Article/4_58.png)

이를 잘 조절하면서 위에 붙여넣는다. 

![png](/assets/images/Tab_Article/4_59.png)

<br>

<br>

# Final Result



<iframe seamless frameborder="0" src="https://public.tableau.com/views/_16204069893480/Dashboard1?:embed=yes&:display_count=yes&:showVizHome=no" width = '954' height = '704' scrolling='yes' ></iframe>

