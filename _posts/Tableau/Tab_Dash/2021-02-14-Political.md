---
title:  "이념적 성향(집계된 데이터)"
excerpt: "막대그래프 + 성향별 다른 색 + 시계열"
categories:
  - Tab_Dash
tags:
  - 3
last_modified_at: 2021-02-14

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

https://www.youtube.com/watch?v=f8oGxVkgwHU 강의를 참고하였습니다.

# Data

- kosis 의 이념적 성향 데이터 (2013 ~ 2019)

  ![png](/assets/images/Tableau_ex/1_0.PNG)

  ![png](/assets/images/Tableau_ex/1_1.PNG)

- 년도 + 사람의특징 별로 정치 성향의 비율이 제시되어있음 
  - 4차원 데이터(년도,특징,정치성향,비율값) 임을 알 수 있다.
  - 즉 (년도,특징) 을 구분으로 (정치성향,비율값) 을 시각화 하면 될 것이다.
  - 막대그래프의 X_Axis 에 특징,년도 를 표현하고 Y_Axis 에 색깔로 구분되는(정치성향) 비율값을 넣자.

# Preprocessing

​	![png](/assets/images/Tableau_ex/1_2.PNG)

- Issue 1 
  - 년간 데이터가 columns 에 붙어있기 떄문에 시각화 하는데에 어려움이 있다. (필드가 너무 많음)
  - 또한 columns 에 각 성향별 정보도 담겨있다.

- Issue 2
  - '소계' 부분은 필요 없는 부분이다. (합계는 데이터를 요약한 형태이기 때문에 이 작업은 Tableau 에서도 가능하다. 혼란을 피하기 위해 삭제하는것이 더 낫다.) 
- Issue 3
  - 테블루에서 interpreter 를 설정해 읽어왔을때에 구분별(1) 은 큰 분류에 속해서 셀이 병합되어 있는 상태였다. 그런데 이 셀을 Tableau 에서는 나누어서 처리하였다.

- 위 이슈들을 해결해야한다.



## issue 1 처리

- 1.Pivot 을 통해 Melt 시켜서 년간 데이터를 가로에서 세로로 변환시켜주자.

  ![png](/assets/images/Tableau_ex/1_3.PNG)

- 2.뒤의 (%) 를 지워서 깔끔하게 만들어 주자.

  ![png](/assets/images/Tableau_ex/1_4.PNG)

- 3.년도별 정보와 성향별 정보를 떼어내기 위해서, (%) 를 지운 col 에 대해서 seperator 를 space 로 둔 뒤 모두 분리한다.

  ![png](/assets/images/Tableau_ex/1_5.PNG)

- 4.모두 분리해서 성향별 정보도 두조각으로 나뉘어졌는데(노란색) 이를 합치기 위해서 Calculatation 을 만든 뒤에 합쳐준다.

  ![png](/assets/images/Tableau_ex/1_6.PNG)

- 5.합치고 난 뒤 필요없는 데이터를 삭제하고 이름을 새로 지정한다.

  ![png](/assets/images/Tableau_ex/1_7.PNG)



## issue 2 처리

- 1.다음과 같이 DataSource 탭에서 Add filter 하여 소계를 지워낸다.

  ![png](/assets/images/Tableau_ex/1_8.PNG)

- 2.그러면 데이터는 다음과 같아진다.

  ![png](/assets/images/Tableau_ex/1_9.PNG)



## issue 3 처리

- 1.이제 워크시트로 이동한 뒤에 데이터의 유형을 알맞게 바꾸어 준다.

  ![png](/assets/images/Tableau_ex/1_10.PNG)

- 2.그리고 이 상태에서 큰 분류와 작은 분류가 잘 설정되어 있는지 확인하기 위해서, 큰 기준, 작은 기준을 row 탭에 올려 확인해 보자.

  - 큰 기준 Null 이 있는것을 보니, 태블로가 병합된 셀을 인지하지 못한것으로 보인다.

  ![png](/assets/images/Tableau_ex/1_11.PNG)

- 3.작은 기준에서 그룹핑을 통해 아예 새로은 큰 기준을 생성해 내자. 

  - 아래 그림과 같이 작은 기준이 잘 분류가 되게 새로 그룹핑을 일일히 지정한다.

  ![png](/assets/images/Tableau_ex/1_12.PNG)

- 4.그러면 아래 그림과 같이 큰 기준에 대해서 작은기준(group) 이 새로 생성된다. 

  ![png](/assets/images/Tableau_ex/1_13.PNG)

- 5.이 작은그룹(group) 에 대해서 가시성이 높도록 하기 위해서 그룹의 이름을 지정해 주자. 그리고 이 작은그룹(group) 을 새로운 상위 분류 기준으로 사용하고 기존의 '큰 기준' 은 삭제하자.

  ![png](/assets/images/Tableau_ex/1_14.PNG)

- 6.이제 작은기준(group) 과 작은기준 으로 계층을 만든 결과 null 없이 잘 작동하고 있음을 확인했다. 

  ![png](/assets/images/Tableau_ex/1_15.PNG)



# Vis(view)

- 이제 워크시트에서 Visualization 을 실행해 보자.
- Vis1(x축)
  - (큰 기준과 작은 기준 계층, 년도) 2개가 X_Axis 에 오게 하고싶다.
  - 위쪽 X_Axis 는 기준 / 아래쪽 X_Axis 는 년도
- Vis2(y축)
  - 각 비율 데이터이므로 각 범주에 대하여 정치성향의 합은 늘 100%일 것이다. 
  - 각 정치성향의 비율을 누적막대 그래프로 그리고 싶다.
- Vis3(Filter)
  
- 나이, 직업 등을 필터로 지정하면 좋을듯 한다.
  
- 위 사항들을 어느정도 그림판으로 초안을 짜 본 것이 아래 그림이다.

  ![png](/assets/images/Tableau_ex/1_17.PNG)

  

## 초안

- 위 사항들을 모두 적용해서 초안을 짜 보자.

- 1.우선 대충 년도와 비율의 막대그래프를 생성한다.

  - 이때 초안과 맞게 Rows 에 측정값, col 에 기준을 넣었다.

  ![png](/assets/images/Tableau_ex/1_18.PNG)

- 2.위 축에 들어갈 기준들을 columns 에 추가한다.

  - 이제 정치성향(색 으로 구분) 말고는 모든 차원이 들어간 상태

  ![png](/assets/images/Tableau_ex/1_19.PNG)

- 3.아래 col 에 년도가 와야하므로 년도와 적용기준의 순서를 바꾼다.

  ![png](/assets/images/Tableau_ex/1_20.PNG)

- 4.이제 색으로 구분되는 정치성향을 Marks 에 추가한다.

  ![png](/assets/images/Tableau_ex/1_21.PNG)

- 5.이제 적용기준(group) 에 필터를 적용하지.

  ![png](/assets/images/Tableau_ex/1_22.PNG)



## 미세조절

- 정치 성향이 색깔로 잘 구분되게 조절

  ![png](/assets/images/Tableau_ex/1_23.PNG)

- 각 성향의 퍼센티지가 표시되게 조절

  ![png](/assets/images/Tableau_ex/1_24.PNG)

- 경계선 표시

  ![png](/assets/images/Tableau_ex/1_25.PNG)



# Vis(Dashboard)

- 이제 시각화 한 내용을 대시보드를 통해 시각화 해 보자.

- 1.대시보드를 끌어온다.

  ![png](/assets/images/Tableau_ex/1_26.PNG)

- 2.각 view 와 범례들을 배치

  ![png](/assets/images/Tableau_ex/1_27.PNG)

- 3.제목이 작은그룹(group) 별로 바뀌게 조절

  ![png](/assets/images/Tableau_ex/1_28.PNG)

- 4.범례의 스타일 지정 + 필요없는 축 이름 흰색처리

  ![png](/assets/images/Tableau_ex/1_29.PNG)

- 5.축의 표시 자릿수 정리

  ![png](/assets/images/Tableau_ex/1_30.PNG)

- 데이터 표시값 자릿수 정리 

  ![png](/assets/images/Tableau_ex/1_31.PNG)



# Result

<iframe seamless frameborder="0" src="https://public.tableau.com/views/1319_16132987879300/Dashboard1?:embed=yes&:display_count=yes&:showVizHome=no" width = '650' height = '860' scrolling='yes' ></iframe>