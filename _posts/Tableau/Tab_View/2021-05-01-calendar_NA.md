---
title:  "1년 달력(누락없는)"
excerpt: "날짜값이 누락없는 1년 달력 차트"
categories:
  - Tab_View
tags:
  - 3
last_modified_at: 2021-05-01

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

<br>

# 달력 차트 게시글과 비교

이전의 달력차트 시각화를 보면, 우리의 데이터가 있는 부분만 차 있는것을 볼 수 있다.

![png](/assets/images/Tableau/18_63.PNG)

또한 단일 월 에 대한 데이터이기때문에 전체 1년의 추이를 살펴보기가 힘들다는 단점이 있다. 이럴 경우에 어떻게 해야할까? 

# 1년 달력 형태 만들기

우선 데이터는 슈퍼스토어 2019 를 사용하겠습니다. 이 데이터에 대해서, 달력 시각화를 만들기 위해서 weekday 를 columns 으로, 주문일자의 주에 대해서 rows 로 설정하였습니다.  

![png](/assets/images/Tab_Vis/10_1.png)

이와 같은 구성은 저희가 원한것이 아닙니다. 1년 달력처럼 가로,세로에 월별로 구성되어있는것을 원합니다. 이를 위해서 다음과 같이 주문일자의 데이터에서 Custom date 를 생성합시다. 

![png](/assets/images/Tab_Vis/10_2.png)

![png](/assets/images/Tab_Vis/10_3.png)

위와 같이 Month date 를 추출하게 되면, 날짜에 대해 월의 데이터만 있는 데이터가 생성됩니다. (즉 2014-03-01 의 데이터에 대해서 3ㅇ이 됩니다.)

![png](/assets/images/Tab_Vis/10_4.png)

이제 이 데이터에 대해서 Grouping 을 합니다. Group 을 통해서 '열' 별로 나눠지게 됩니다. 저희는 가로가 3, 세로가 4 인 달력을 구성하고 싶으므로, Group 은 아래 그림과 같이 됩니다.

![png](/assets/images/Tab_Vis/10_5.png)

이제 만든 그룹을 columns 에 올려놓습니다. 그러면 처음 Col 이 나누어질때에 그룹(1,2,3) 별로 나누어지고 그에 따라서 시각화는 아래와 같이 이루어집니다. 

![png](/assets/images/Tab_Vis/10_6.png)

이제 비어있는 칸들을 지워버리고 싶습니다. 저희는 Week Number 라는 변수를 만들것입니다. 주문일자의 주 - month 를 고정하였을때에, minimum 주 로 정의합시다. 

![png](/assets/images/Tab_Vis/10_7.png)

위 의미는 뭘까요? 1,2,3 월의 경우를 생각해봅시다. 저희는 '월' 과는 상관없이 첫쨰주,  둘쨰주 .. 에 대해서 같이 정렬하고 싶습니다. (즉 2월 첫째주와 3월 첫쨰주는 같은 Row 에 있기를 바랍니다.) 하지만 주의 경우, 1~53주까지 길게 되어있습니다. (그러므로 2월 첫쨰주는 5, 3월 첫쨰주는 10의 값을 가집니다.)

이럴 경우에 위와 같이, month 에 고정시키고 난 뒤, 선택된 주 값 - 최소 주값 을 하게 된다면, 3월 첫쨰주의 경우 10 - 10 = 0 이 되고 1월 첫쨰주의 경우 1-1 = 0 이 됩니다. 즉 '다른 월 에 대해 n째주는 같은 값을 가지게 됩니다.'

즉 위에서 정의한 Week Number 라는 Calculated Field 를 rows 에 집어넣게 되면 우리가 원하는대로, 분류가 되는것을 볼 수 있습니다.

![png](/assets/images/Tab_Vis/10_8.png)

 0 값이 첫쨰주인데, 맨 아래에 위치합니다. 이를 돌리기 위해 Axis 를 Reversed 로 고치고 그 다음에, SCale 을 -2~6 으로 수정합니다! 그러면 날짜 위에 공백이 2 값 만큼 생길것입니다. (월의 첫 시작이 0 이므로) 이렇게 생긴 공백에 , 저희는 '몇월' 인지의 정보값을 넣을 것 입니다.

![png](/assets/images/Tab_Vis/10_9.png)

그리고 CNT 라는 변수를 정의하는데, 1만 넣습니다. 여기서 얻고자 하는것은 Count of records 입니다. 

![png](/assets/images/Tab_Vis/10_10.png)

이후에 이 값을 AVG 시킨 후에, SIze 에 넣도록 합시다. 그렇게 된다면 '값이 존재 한다면 1' 을 가지는 agg 값이 됩니다. 그러므로 아래와 같이 달력처럼 균일한 사이즈로 배치된것을 볼 수 있습니다. 

![png](/assets/images/Tab_Vis/10_11.png)

그 이후에 사이즈를 늘려주고, 외곽선을 추가합니다. 

![png](/assets/images/Tab_Vis/10_12.png)

![png](/assets/images/Tab_Vis/10_13.png)

그 이후에, 매출을 올려넣게 되면 1차적으로 저희가 원하는 시각화가 완성됩니다 .

![png](/assets/images/Tab_Vis/10_14.png)

<br>

<br>

# 빈 값에 날짜 추가하기

이제 날짜를 추가해 봅시다. 주문 일자를 Label 로 추가합시다.

![png](/assets/images/Tab_Vis/10_15.png)

크기가 작아서 잘 보이지 않는것입니다. 이런 경우에는 다음과 같이 Text 의 설정에서 Allow label to overlap 을 클릭한다면 모두 겹치게 할 수 있습니다. 

![png](/assets/images/Tab_Vis/10_16.png)

그리고 배열을 정렬합시다. 

![png](/assets/images/Tab_Vis/10_17.png)

하지만 여전히, 비어있는 칸에 대해서는 데이터가 없으므로, 시각화를 하지 않고있는 (비어있는) 모습입니다. 이런 경우에는 저희가 '새로 데이터를 만들어야' 합니다. 아래와 같이 엑셀로 2019 년의 모든 날짜를 생성합니다.

![png](/assets/images/Tab_Vis/10_18.png)

그 이후 데이터 패널로 가서 날짜 데이터를 불러옵니다. 

![png](/assets/images/Tab_Vis/10_19.png)

![png](/assets/images/Tab_Vis/10_20.png)

그 이후 Full outer join 을 통해서 주문일자와 2019 full 날짜를 join 합니다. 그러면 모든 날짜가 있는 데이터를 새로 얻을 수 있습니다. (물론 Null 값이 섞여있을것입니다.)

![png](/assets/images/Tab_Vis/10_21.png)

join 을 한 이후에 다시 view 로 돌아가봅시다. 

![png](/assets/images/Tab_Vis/10_22.png)

이제 주문일자에 대해서  Replace Reference 를 해봅니다. 이 의미는 '이 데이터가 참조된 모든식에 대해서 대체' 하는것 입니다. 즉 존재를 아예 바꿔치기하는것입니다. 

![png](/assets/images/Tab_Vis/10_23.png)

2019 년의 모든 날짜의 경우, 열의 이름이 F1 이였습니다. 이 값으로 바꾸겠습니다.

![png](/assets/images/Tab_Vis/10_24.png)

그러면 아래와 같이 누락된 데이터에 대해서도, 날짜표시를 할 수 있었습니다. 비록 Null 값이지만, 데이터가 있어서 색이 칠해지고 있는 모습입니다.

![png](/assets/images/Tab_Vis/10_25.png)

![png](/assets/images/Tab_Vis/10_26.png)

<Br>

# 색상 조정하기

다음과 같이 Real Sale 이라는 변수를 정의합니다. 이 변수는 매출이 NULL 일떄에 (2019 Full date를 붙여넣기 해서 생기는 에러입니다.) -1 을 출력합니다. 다른 경우는 일반적으로 매출을 출력합니다.

![png](/assets/images/Tab_Vis/10_27.png)

그리고, 매출값에 대해서, Real Sale 이라는 변수로 바꿔치기 합니다. (Replace Reference)

![png](/assets/images/Tab_Vis/10_28.png)

그러면 아래와 같이 Real sale 이라는 변수로 바꿔치기가 된것을 볼 수 있습니다. Legend 를 보시면, -1 이라는 값이 생긴것을 볼 수 있습니다. 

![png](/assets/images/Tab_Vis/10_29.png)

이제 Color 를 edit 합니다. 다음과 같이 Use Full Color Range 를 사용하고, 흰색 색상을 사용합니다. 

![png](/assets/images/Tab_Vis/10_30.png)

그러면 아래와 같이, 값이 없는 날에도, 색상이 하얀색으로 제대로 나온것을 볼 수 있습니다. 

![png](/assets/images/Tab_Vis/10_31.png)

<Br>

# 월 표시하기

이제 각각 월마다, 몇월인지 표시해야 합니다. 그러므로 아래와 같이 '월 표시' 라는 변수를 생성합니다. 그 경우에 IF DATEPART 함수를 통해서, weekday 가 4일때(수요일일떄) -2를 출력하는 함수를 정의합니다. 

이러한 함수를 통해서, 노랗게 칠한 위치에, 마크가 찍히게 됩니다. 

![png](/assets/images/Tab_Vis/10_32.png)

이제 월 표시 변수를 Row 에 올려놓습니다. 

![png](/assets/images/Tab_Vis/10_33.png)

그 이후에 월 표시를 AVG 로 변환합니다. 그 이후에 마크를 모두 제거해서 깨끗히 만듭니다. (여기에는 몇월 이라는 텍스트가 들어갈 것입니다.) 그리고 마크를 원으로 바꾸고 사이즈를 최하로 맞춥니다. (잘 보면 아주 작게 원이 있음을 알 수 있습니다.)

![png](/assets/images/Tab_Vis/10_34.png)

그리고 MONTH 변수를 텍스트로 올려놓습니다. 

![png](/assets/images/Tab_Vis/10_35.png)

그 이후에 Syncronize 를 통헤서 두 열을 합칩니다. 

![png](/assets/images/Tab_Vis/10_36.png)

그리고 텍스트의 Alighment 를 조절합니다. 

![png](/assets/images/Tab_Vis/10_37.png)

이제 다음과 같이 완성됩니다. 

![png](/assets/images/Tab_Vis/10_38.png)

<br>

# 평일 휴일 구분

아래와 같이 평일 , 휴일 데이터를 가져옵니다.

![png](/assets/images/Tab_Vis/10_39.png)

그리고 아래와 같이 평 / 휴일 데이터를 옆에다가 붙입니다. 

![png](/assets/images/Tab_Vis/10_40.png)

그리고 평일 날짜라는 변수를 만듭니다. 아래와 같이, 평일일 경우, 그냥 Day(F1) 을 출력하는 함수입니다. 

![png](/assets/images/Tab_Vis/10_41.png)

똑같이 휴일 날짜도 정의합니다. 

![png](/assets/images/Tab_Vis/10_42.png)

이제, DAY(F1) 을 평일날짜와 휴일날짜로 대체합니다. 이 경우에 어떤것이 다를까요? 사실 달라진게  없습니다. 다만 '평일' 과 '휴일' 을 쪼갠것에 불과합니다. 이 경우 Label 에서 빨강색과 검은색으로 조절하게 된다면 

![png](/assets/images/Tab_Vis/10_43.png)

아래와 같이 우리가 원하는 View 를 얻을 수 있습니다. 

![png](/assets/images/Tab_Vis/10_44.png)

