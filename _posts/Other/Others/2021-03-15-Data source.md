---
title:  "Data Source"
excerpt: "데이터 수집가능한곳"
categories:
  - Others
tags:
  - 3
last_modified_at: 2021-03-15

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---



# Intro

데이터는 Obatainable thing 이다. 데이터를 맞딱뜨렸을때, 제일 먼저 고민해야되는건 '아 여기서 더 붙일 수 있는건 없나?' 라고 생각한다. 그러므로 데이터 수집이 어디어디서 가능할지 알아두는것이 좋다고 생각한다!





# Map

- 국가공간정보포털 <http://www.nsdi.go.kr/lxportal/?menuno=2679>
  - 행정구역 읍면동 < http://data.nsdi.go.kr/dataset?q=%EC%9D%8D%EB%A9%B4%EB%8F%99&sort=score+desc%2C+views_total+desc>
  - 읍면동으로 구분되어있는 지리데이터를 얻을 수 있다. 각 지역(서울, 대전....) 등에 해당하는 지리데이터를 얻을수도 있으며, 또는 전국적으로 읍면동이 구분된 지리데이터를 얻을 수 있다.



- 행정표준코드관리시스템
  - 법정동 코드분류 <https://www.code.go.kr/stdcode/regCodeL.do> 
  - 동 / 구/ 읍/ 면/ 동/ 리.... 등으로 나누어져 있을때, 그것에 대한 분류 코드(법정동!) 을 제공한다. 



- shp 다운로드(맵 정보파일) <http://www.gisdeveloper.co.kr/?p=2332>

  - 시도 , 시군구 , 읍면동, 리 까지의 순차적인 지리 데이터를 계속 업데이트해주는 천사같으신 분이 운영하는 사이트.



# 인구

- 행정안정부 주민등록 인구통계 <https://jumin.mois.go.kr/>

  - 비교적 업데이트가 빠르게 되어 한달 전 상황도 살펴볼 수 있는것이 장점
  - 남/여, 세대수 등을 붙일 수 있으며 또한 읍/면/동 수준까지 세세하게 인구의 이동을 살펴볼 수 있는 좋은 사이트

  





# 상권분석

- 소상공인마당 <https://sg.sbiz.or.kr/godo/index.sg>

  - csv나, 시군구별 분석을 지원하지 않아 약간 아쉽다.

  - 하지만 읍/면/동 별로의 상권분석이 매우 자세하게 나와서 은근히 좋은 insight 를 얻기 좋다.




# index(world)

- <http://hdr.undp.org/en/data>
  - 세계의 주요 지표들에 대한 데이터를 얻을 수 있다. 상당히 다양함.

# Tip

- 데이터가 끊겨있다면(특히 공공데이터포털!) 담당자한테 전화하는것도 좋다.

  - 공무원이라 그런지 일처리가 빠르다. 바로 완벽한 데이터를 얻을 수 있음



