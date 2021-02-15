---
title:  "Map(google spread)"
excerpt: "테블로 맵 시각화를 위해 구글 스프레드를 통한 전처리를 알아보자"
categories:
  - Tableau
tags:
  - 3
last_modified_at: 2021-02-11

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

# 구글맵 API

- 구글 API 를 이용해서, Python 에서 아래와 같은 변환이 가능하다.
  - 위/경도 -> 주소 (역 지오코딩)
  - 주소 -> 위/경도 (지오코딩)

- google maps 를 이용하려면 결재카드 등록을 해야했다.  프로젝트를 생성한 뒤에 결제 카드를 등록하자. 정해진 금액을 넘지 않는다면 체험판으로 준 달러로 충분하고 또한 정해진 금액을 초과하더라도 사용자가 추가 결제를 하지 않으면 금액은 자동으로 빠져나가지 않는다고 한다.
- 하지만 여전히 우려되는것은 사실이다.
  - 카드 정보를 입력할 때 자동 결제라고 되어있어서 부담됨
  - 내 API 키가 유출될 걱정도 든다.
- 그래서 우선 구글 맵 API 를 이용한 변환은 나중으로 미루어 두고 구글 스프래드를 이용하도록 하였다.



# 구글 스프레드

- 구글 스프레드는 아래와 같이 구글 계정에서 사용 가능하다.

![png](/assets/images/Tableau/4_1.PNG)

- csv 파일 (또는 원하는 파일) 을 스프레드에 올린 후 스프레드에서 geocoding by awsome 을 다운

![png](/assets/images/Tableau/4_3.PNG)

- 그 이후 부가기능에 새로운 Geocode by Awesome Table 이 추가된것을 볼 수 있다.

![png](/assets/images/Tableau/4_2.PNG)

- 이때 위 부가기능에서 start geocode 를 들어간다.

![png](/assets/images/Tableau/4_4.PNG)

- 자 이제 위와 같이 geocode 를 적용하고픈 시트와 column 을 선택하고 변환을 누른다
- 그러면 차례로 주어진 도로명 주소에서 위/경도를 추출해준다.



# 스프레드 오류

- 때떄로, 주소를 제대로 읽지 못해 빨간색 칸이 나오는 경우가 있다.

![png](/assets/images/Tableau/4_5.PNG)

- 위와 같이 에러가 나오는 경우 google map 페이지에서 직접 보정해 주자.

![png](/assets/images/Tableau/4_6.PNG)

- 위와 같이 구글맵에서는 주소를 입력했을때에 위도 경도를 주소창에 표시해준다.
- 이를 이용해서 보정하자.



# 스프레드의 단점

- 물론 별다른 결재 정보를 묻지 않고 바로 변환을 해 주어서 좋기는 하지만
- 1.주소 -> 위/경도 의 변환밖에 없고
- 2.도로명주소가 안좋으면 변환 자체가 잘 안되는점
- 3.그리고 하루 1000개정도의 제한이 걸려있는점
- 위의 단점때문에 대용량 데이터나 더러운 데이터에서는 사용할 수 없다.
- 하지만 어느정도는 쓸모가 있기때문에 적은 데이터(1000~3000 rows) 에서는 강력! 추천드립니다.