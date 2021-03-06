---
title:  "Data(Source)"
excerpt: "태블로에서 원본 데이터를 다루는법을 알아보자."
categories:
  - Tableau
tags:
  - 3
last_modified_at: 2021-02-12

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

# Data switch

- 태블로에서 데이터를 선택하고 작업할 때에, 새로 데이터를 update 해야될 때가 있다.
- 1.Data -> New data source 에서 새 데이터를 가지고 온다.

  ![png](/assets/images/Tableau/6_1.PNG)
- 2.아래 그림과 같이 새 데이터가 들어온것을 볼 수 있다.

  ![png](/assets/images/Tableau/6_2.PNG)
- 3.이제 Data -> Replace Data source 를 들어간다.

  ![png](/assets/images/Tableau/6_3.PNG)
- 4.아래 그림에서 current 가 옛날 데이터, vis(2) 가 업데이트한 데이터이다. 새로 업데이트한 데이터로 Replacement 를 선택하자.

  ![png](/assets/images/Tableau/6_4.PNG)

- 5.이제 오래된 데이터를 삭제해주면 된다.

  ![png](/assets/images/Tableau/6_5.PNG)

---

# Excel Sheet

- 엑셀 데이터를 다루다 보면 시트가 여러개로 나뉘어져 있는 경우가 있다.

  ![png](/assets/images/Tableau/6_6.PNG)

- 이 데이터를 태블루로 바로 읽게 되면 아래와 같이 Sheets 에 여러개의 시트가 뜨게 된다.

  - Sheets 에서 우리가 원하는 시트를 더블클릭하게 되면 그 시트를 살펴볼 수 있게 된다.

  ![png](/assets/images/Tableau/6_7.PNG)

---

# Data Split

- 테블로에서도 어느정도 전처리가 가능한데, 그 중에서 분할에 대해서 알아보자.

**Split(자동분할)**

- Split은 Tableau가 필드에서 검색한 공통 구분 기호를 사용하여 자동으로 분할해준다.

  ![png](/assets/images/Tableau/6_8.PNG)

- 자동분할 (Split) 을 사용하여 아래와 같이 Salary/Winnings 의 $105 M 형식이 105 M 으로 바뀌었다.

  - 이 때 새로 바뀐 변수 위에 =Abc 기호를 볼 수 있는데 = 기호의 의미는 계산된 필드(원본 데이터가 아니라 내가 새로 만들었다는 의미) 라는 의미이다.

  ![png](/assets/images/Tableau/6_9.PNG)

- 새로 분할된 필드에서 105 M 형식이 아직도 마음에 들지 않는다. 그러면 계산된 Salary/Winnings 에 위 작업을 한번 더 적용하면 된다.

  ![png](/assets/images/Tableau/6_10.PNG)

- 이제 기존의 변수 및 쓸데없는 변수들을 hide 처리하고, 새로 계산된 필드의 이름을 바꾸어주자.

  ![png](/assets/images/Tableau/6_11.PNG)



**자동분할이 그러면 최고인가요?**

- 자동 분할을 사용하지 않는 것이 좋은 경우도 있다. 다음 두 예시들이 대표적인 경우이다.

- 서로 다른 수의 구분 기호가 포함된 값 

  - 값마다 구분 기호의 수가 다른 경우 필드를 자동으로 분할할 수 없습니다. 예를 들어 필드의 값이 다음과 같다고 가정해 보자.

    jsmith-accounting-north

    dnguyen-humanresources

    lscott-recruitin-west

    karnold-recruiting-west

  - 이 경우 사용자 지정 분할을 사용하는 것이 좋다.

  

- 여러 구분 기호가 포함된 값 
  -  구분 기호 유형이 서로 다른 경우 필드를 자동으로 분할할 수 없습다. 예를 들어 필드가 다음과 같은 값을 포함한다고 가정 해 보자.

    smith.accounting

    dnguyen-humanresources

    lscott_recruiting

    karnold_recruiting

- - 이 경우 정규식을 사용하여 새 필드를 만드는 것이 좋습니다.



**Custom split**

- 이번에는 자동으로 말고, 직접 우리가 Split 기준을 명시해준 후 Split 을해보자.

- 먼저 Custom Split 을 선택한다.

  ![png](/assets/images/Tableau/6_12.PNG)

- 그리고 Split 의 기준을 정해준다.

  - Use the seperator : 띄어쓰기, _ ,쉼표 등으로 Split 을 할 기준을 정해준다.
    - 우리의 데이터에서는 $62.3 M 으로 우선 띄어쓰기를 기준으로 Split 하여 $62.3, M 으로 나누자.
  - Split off : seperator 를 어떻게 적용할지
    - 예를 들어서 2007-12-09 를 seperator - 로 나눌시에 2007 12 09 로 3개의 split 이 생성되게 된다.
    - 이때 first + 1columns 로 설정한다면 처음 값의 2007 만 남게되고 2로 한다면 2007 , 12 두개의 데이터가 남게된다.
    - ALL 로 설정하게 된다면 seperator 로 나눈 모든 데이터를 출력해준다. 
    - 우리는 맨 앞의 $62.3 의 데이터만 필요하므로 1로 설정

  ![png](/assets/images/Tableau/6_13.PNG)

  ![png](/assets/images/Tableau/6_14.PNG)

---

# Data Interpreter

- Tableau 에서는 데이터의 해석을 도와주는 인터프리터가 존재한다.

- 먼저 다음과 같은 데이터를 해석하는것을 살펴보자.

  - 병합되 셀이 존재하는 탓에 해석이 어려워보인다.

  ![png](/assets/images/Tableau/6_15.PNG)

- 이를 Tableau 에 올려보자. 그러면 아래와 같다.

  ![png](/assets/images/Tableau/6_16.PNG)

- 올려진 내용의 col 구분이 매우 난잡하다. 이를 데이터 인터프리터를 체크하여 해석해보자. 

  ![png](/assets/images/Tableau/6_17.PNG)

- 데이터 인터프리터를 체크하니 col 이 병합되어 깔끔하게 나타난것을 볼 수 있다. 구체적으로 어떻게 처리되었는지 알기 위해서는 파란색 글씨의 Review the results 를 클릭하면 처리 내용을 알려주는 엑셀이 나오게 된다.

  ![png](/assets/images/Tableau/6_18.PNG) 

---

# Pivot data

- 다음과 같은 데이터의 경우를 생각해보자.

  - 다음과 같이 columns 이 년도로 모두 쪼개져 있기 때문에 이를 그대로 사용하게 되면 field 가 너무 많아져 버려서 처리하기가 너무 힘들다.
  - 즉 데이터를 피벗(가로 형식의 데이터를 세로로 길게 Melt 시키는것) 해야한다.

  ![png](/assets/images/Tableau/6_19.PNG) 

- 우선 CO2 배출량을 시각화 하고 싶다고 하자. 그러면 각 열로 널리 퍼져있는 데이터를 한데 묶어 주어야 한다.

  - 그렇게 하기 위해 1960 ~ 2011 의 데이터를 shift 클릭으로 모두 선택한 뒤에 피벗을 적용한다.

  ![png](/assets/images/Tableau/6_20.PNG) 

- 그러면 우리가 선택한 1960~2011 의 columns 들은 피벗 필드 이름 이라는 column 으로 생성되게 된다. (즉 가로로 퍼져있던 데이터가 세로로 정렬된것)

  - 그리고 피벗 필드 값은 각 피벗필드 이름의 년도에 대한 CO2 배출량이 된다.

  ![png](/assets/images/Tableau/6_21.PNG) 

- 이제 피벗필드 이름 -> 연도 , 피벗필드 값 ->  CO2 으로 이름을 변경해 보자. 

  - 그러면 아래 그림과 같이, 비로소 쉽게 시각화가 가능해 진다.

  ![png](/assets/images/Tableau/6_22.PNG) 

---

# Delete word

- 데이터를 처리하다 보면 뒤나 앞에 쓸데없는 단어가 들어있는 경우가 있다.

  - 응답률 (%)
  - $ 가격

- 위 같은 경우를 처리하기 위해도 Split 을 활용할 수 있다.

  - 아래와 같이 '2019 다소 보수적 (%)' 처럼 (%) 를 지우고 싶은 경우라고 하자. 
  - 그러면 Split 기준을 ( 로 잡는다면 '2019 다소 보수적' 과 '%)' 두개로 쪼개지게 된다.
  - 그런데 Split off 를 First 1 columns 로 잡음으로서 처음의 '2019 다소 보수적' 만 남게된다.

  ![png](/assets/images/Tableau/6_23.PNG) 

- 그 결과 아래와 같이 (%) 를 지운 데이터를 얻을 수 있다.

  ![png](/assets/images/Tableau/6_24.PNG)



# Merge word

- '2019 다소 보수적' 이라는 문장을 맨 앞의 '2019' 년도롸 뒤의 '다소 보수적' 이라는 성향으로 나누고 싶다고 하자.

  - 위를 수행하려면 우선 위의 문장을 seperater 는 띄어쓰기, split off 는 ALL 을 주어서 띄어쓰기별로 모두 분해해 보자.

  ![png](/assets/images/Tableau/6_25.PNG)

- 이제 다소 + 보수적 처럼 2개의 단어를 합쳐서 새로운 Columns 를 만들어야 한다.

- 1.먼저 Calculated Field 를 만든다.

  ![png](/assets/images/Tableau/6_26.PNG)

- 2.그리고 + 연산을 통해서 field 를 더해 새로운 col 을 추가한다.

  - Str 끼리의 연산은 Python과 동일하다.
  - 이때 가운데에 띄어쓰기 ' ' 를 추가로 써 넣었다.

  ![png](/assets/images/Tableau/6_27.PNG)



# Filter (In/Exclude)

- 데이터중에 쓰고싶지 않은 데이터가 있는 경우도 있다.

- 워크시트에서 직접 filter 로 걸러내기에는, 쓸데없는 filter가 생기게 되어서 혼란스러울 수 있으니, Data Source 탭에서 filter 를 써서 걸러내보자.

- 1.먼저 아래의 경우에서 구분별(1) 의 '전체' 를 없애고자 한다.

  - 그러면 노랗게 칠한 Filter Add 를 선택한다.

  ![png](/assets/images/Tableau/6_28.PNG)

- 2.그리고 나서 edit data source filter 창에서 Add..를 클릭한 뒤 Add filter 에서 우리가 지우고자 했던 '전체' 가 들어있는 구분별(1)  을 선택하자.

  ![png](/assets/images/Tableau/6_29.PNG)

- 3.그리고 Filter 에서 '전체' 를 클릭한 뒤 Exclude 를 체크하면 구분별(1) 의 '전체' 데이터가 없는 데이터가 된다.

  ![png](/assets/images/Tableau/6_30.PNG)



