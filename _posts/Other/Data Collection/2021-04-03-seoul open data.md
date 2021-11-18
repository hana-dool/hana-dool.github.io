---
title: "서울 열린데이터광장 API"
excerpt: "서울 열린데이터광장의 API 에서 데이터를 추출하자."
categories:
  - Data_Collection
tags:
  - 3
last_modified_at: 2021-04-03

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---



# 회원가입

우선 우리의 목표는 아래의 공공자전거 대여소의 위치 데이터를 api 에서 가져오는 것이다. 

![png](/assets/images/Data/1_0.PNG)

api 를 받으려면 먼저 인증키를 받아야 한다. 인증키를 받으려면 로그인을 한 뒤에 발급받자. 로그인을 한 뒤에 인증키를 신청하자. 아래의 신청서에를 작성한다. Url 과 사용처를 적고 제출하자. (나는 네이버 블로그를 적었다. 하지만 제출하자마자 발급되므로 너무 공들여서 작성할 필요는 없다.)

![png](/assets/images/Data/1_1.PNG)

작성하고 제출하게 되면 우리의 일반 key 를 받게 된다.

![png](/assets/images/Data/1_2.PNG)

# API 추출

아래 sample url 을 보면 {인증키} 부분에 우리의 인증키를 넣으면 아래의 예제가 나오게 된다. 우선 명세서를 보면서 어떻게 데이터가 구성되어있는지 확인하자.

![png](/assets/images/Data/1_3.PNG)

아래 명세서를 보면 한전에 최대 1000건을 초과할 수 없으니, 몇회 나누어 호출해야 함을 알 수 있다. 그리고 한번에 1000개의 데이터를 가져올 수 있음을 볼 수 있다. 그리고 요ㅈ청인자를 보자. 우리가 받은 인증키, 요청 파일 타입(웬만하면 json 이 제일 편하다.), service 는 bikelist 라고 입력해야 하며 요청시작위치 ~ 끝나는 위치를 정해주어야함을 알 수 있다. 이

![png](/assets/images/Data/1_4.PNG)

위에서 설명한대로 request 를 통해서 데이터를 가져와 보자. sell 별로 설명하자면 우선 key 는 노출되면 안되므로 코딩할때에 txt 파일에 저장한 뒤에 이렇게 불러와서 사용하는것을 추천한다.

그리고 get 으로 url 의 정보를 요청한 뒤에 json 으로 받아온다.(처음 요청 자체가 json 이였으ㄹ므로 json 으로 받아와야 한다.) 그리고 data 를 읽어보면서 우리가 필요한 정보를 가져온다. 내 경우 rentbikestatus 의 row 의 레벨에 우리가 원하는 정보인, 각 지점별 위/경도 데이터가 있었다.

그리고 start , end 가 1000개밖에 호출이 안되므로 아래처럼 3번 나누어서 호출하였다.(3000이상은 없었음)

![png](/assets/images/Data/1_5.PNG)

이제 마지막으로 불러온 데이터들을 concat 하고 저장하자. 이제 우리가 원하는 데이터를 excel 형태로 가지고 있게 되었다.

![png](/assets/images/Data/1_6.PNG)

위 데이터를 이용해 위/경도를 맵 위에 흩뿌려 보았다.(그냥 추가적으로 해본거..)

![png](/assets/images/Data/1_7.PNG)

