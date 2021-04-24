---
title:  "Order of operation"
excerpt: "작동의 순서에 대해 알아보자"
categories:
  - Tab_Function
tags:
  - 3
last_modified_at: 2021-04-22

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

# intro

태블로는 각각의 operation 에 따른, 작동 순서가 정해져있습니다. 이를 잘 앍있어야 다양한 filter, action 등을 추가할때에 정확하게 추가할 수 있습니다. 아래 그림과 같이 여러 작동들의 순서가 얽히고 있는것을 볼 수 있습니다. 이러한 순서들을 잘 숙지하고있어야합니다.

![png](/assets/images/Tableau/23_0.png)

각각이 뭔지 알아야 잘 쓸 수 있겠죠? 각각이 뭔지 알아봅시다.

<br>

# 1.Extract Filter

Extract filter 란, 아래 그림과 같이 데이터를 불러올때 옆에 있는 Filter 를 말합니다. 즉 데이터를 불러옴과 동시에 바로 필터를 적용하는것이라, 순위가 최상단 일수밖에 없습니다!  아래 그림과 같이 Filter 를 추가할 수 있습니다.

![png](/assets/images/Tableau/24_1.png)

![png](/assets/images/Tableau/24_2.png)

새로 필터가 생긴것을 볼 수 있습니다. 아래 그림과 같이 서울 특별시의 데이터만 남아있는것을 확인할 수 있습니다.

![png](/assets/images/Tableau/24_3.png)

<br>

# 2.Row level calculation

Row level calculation 이란 데이터셋 row 각각에 대해 계산되는것을 말합니다. 아래 그림을 보면 각각 손냄에 대해 가격과, 그 수량이 매겨져 있습니다. 이를 Quantity * Price 의 연산으로 곱한 연산을 해줍니다. 그러면 

![png](/assets/images/Tableau/24_4.png)

아래와 같이 '각각의 row' 에 대해서 계산이 되는것을 볼 수 있습니다. 이런 연산을 row level caculation 이라고 합니다. 우리는 아래와 같이 태블로에게 새로운 계산열을 만들라고 명령을 하고 있는것입니다.

![png](/assets/images/Tableau/24_5.png)

<br>

# 3. Context Filter

컨텍스트 필터란 무엇일까? 태블로에서 모든 필터들은 독립적으로 적용된다. 즉 필터는 다른 필터들과 상관 없이, 데이터 원본 전체를 대상으로 각각 필터링한다. 하지만 A 를 컨텍스트 필터를 지정했다고 하자. 그러면 그 A 필터가 먼저! 적용된 이후 필터링된 데이터를 나머지 필터들이 필터하게 된다. 즉 필터의 왕이라고 생각하면 된다.

이를 사용하는 이유는 필터가 너무 많거나, 데이터 원본이 큰 경우에 performance 향상을 위해 컨텍스트 필터를 사용한다고 한다. 

아래와 같이 필터를 추가한 뒤에, 오른쪽 키를 누르고 Add to Context 를 선택하자. 그러면 이 필터는 필터중의 황제인 'Context Filter' 로 변신한다. 

![png](/assets/images/Tableau/24_6.png)

![png](/assets/images/Tableau/24_7.png)

<Br>

#  4. { Fixed }

FIxed 란 뷰에 있는 차원과 상관없이, 계산된 필드에서 고정한(Fixed) 차원의 집계식을 계산한다. 

아래와 같은 경우를 생각해보자. 뷰가 어떻게되있건 상관없이 우선 제품 대분류로 묶고난 이후에, 매출을 계산하라는 의미이다. 

![png](/assets/images/Tableau/24_8.png)

그 이후에 표를 형성하게 되면 아래 그림과 같이 이미 Fixed 를 하고나서 형성하였기 때문에, 대분류별로는 값이 모두 같은것을 확인할 수 있다! 

![png](/assets/images/Tableau/24_9.png)

<Br>

#  5. Set, Top N, Condition Filter

1.Set filter

아래 그림들과 같이, 차원형에 대해서 Create -> set 을 통해서 set 을 만들 수 있다. 여기서 list 에서 선택하는법, Condition 을 생성하는법, Top N 을 선정하는법 3가지가 있다. 

![png](/assets/images/Tableau/24_10.png)

![png](/assets/images/Tableau/24_11.png)

![png](/assets/images/Tableau/24_12.png)

위 방법으로 Set 을 생성할 수 있다. 이를 아래 그림과 같이 Filters 에 올려놓으면 Set filter 가 된다. 

![png](/assets/images/Tableau/24_13.png)

2.TopN, Condition filter

이는 Set 과 거의 동일한 역할을 한다. 아래처럼 뷰에서 직접 Filter 를 클릭한다. 이 경우에도 Set 을 만들때와 마찬가지로 Condition , Top 이 있음을 알 수 있다. 이것이 바로 Top N, Conition filter 이다. 하지만 Set 으로 만들어서 넣던, 이렇게 넣던 같은 역할을 하게되서, 굳이 구분할 필요는 없어보인다.

![png](/assets/images/Tableau/24_14.png)

![png](/assets/images/Tableau/24_15.png)

<br>

# 6. Dimension Filter

이때에 dimension filter 란 뭘까? 아래와 같이 데이터 선반에 있는 차원을 옮겨오자. 그럴때에 생성하는 Filter를 dimension filter 라 한다. 

![png](/assets/images/Tableau/24_16.png)

<br>



# 7. Include , Exclude 

1.include

include 세부 수준식은 먼저 Include LOD 에 명시된 차원을 포함하여 집계가 이루어집니다.아래 경우를 보면서 예시를 봅시다. 다음과 같이 제품 대분류별 매출을 계산해봅시다. 

![png](/assets/images/Tableau/24_17.png)

그 이후에 include lod 를 써봅시다. 아래의 의미는 '제품 중분류로 묶어서 Ave(매출) 계산' 의 의미를 가지고 있습니다. (즉 include lod 는 자체적으로 FIlter를 가지고 있는것입니다.)

![png](/assets/images/Tableau/24_18.png)

이를 View 에 올려놓으면 아래와 같이 값의 차이가 일어나는것을 볼 수 있습니다. 둘다 같은 매출의 평균을 계산하는것 같은데 어디에서 차이가 벌어진것일까요?

![png](/assets/images/Tableau/24_19.png)

이를 알아보기 위해 아래 그림과 같이 제품 중분류로 나눈 뒤에 평균 매출을 계산해 보았습니다.

![png](/assets/images/Tableau/24_20.png)

그 이후 같은 뷰에서 비교해 보았습니다. 이를 보면 차이가 명확해집니다. 가구의 경우로 예시를 들어보겠습니다. sheet6(2) 에서 

- 왼쪽은 대분류 가구에 해당하는 사람들의 매출 / 총 사람 수 
- 오른쪽은 대분류 가구에서 먼저 중분류별로 나눈뒤 AVG(매출 계산) 이후에 이 값을 다시 평균

위의 차이가 있었던 것입니다. 위와 같은 이유로 차이가 나게 되는것입니다. 

![png](/assets/images/Tableau/24_21.png)

결국 Include LOD 는 그 자체가 차원을 포함하고 있으므로 먼저 계산이 이루어져야 한다. 

1. Include LOD 에 명시된 차원을 포함하여 집계가 이루어짐 
2. VLOD 에 맞추어 표현하기 위해서 첫번쨰 계산 결과를 재집계함 

<br>

2.exclude

exclude 세부 수준식은 먼저 exclude LOD 에 명시된 차원을 제외하여 집계가 이루어집니다. 아래와 같이 각 제품 중분류별로 매출이 형성되어있습니다. 

![png](/assets/images/Tableau/24_22.png)

이제 다음과 같이 Exclude 변수를 만듭니다 아래의 의미는 '제품 중분류' 라고 명시되어있는 차원을 제외한 후에 집계를 하란 것입니다. 

![png](/assets/images/Tableau/24_23.png)

이제 생성된 exclude 변수를 view 에 올려놓으면 아래와 같이 됩니다. 

![png](/assets/images/Tableau/24_24.png)

note) Exclude lod 가 잘 자동하려면, Exclude lod 에서 선언한 차원이 반드시 VLOD (View 에 있는 세부수준, 여기서는 제품 중분류) 안에 포함되어 있어야 한다. 그렇지 않으면 굳이 VLOD 를 쓸 필요가 없는것이다. 

결국 Exclude lod 에서 만들어진 계산 결과는 VLOD 의 수준보다 항상 먼저일 수밖에 없다. (무언가를 제외했기 때문에) 즉 다음과 같이 계산이 이루어진다. 

1. Exclude lod 에 명시된 차원을 제외한 후에 집계가 이루어진다.
2. VLOD 에 맞추어서 표현하기 위해 첫번째 단계의 결과를 복제한다. 



# 8. Aggregate Calculation 

집계함수입니다. AVG, SUM, COUNT, MAX, MEDIAN, VAR 등등의 함수가 포함됩니다. 

아래와 같이, row 별로 존재하고 있는 값들을 Aggregate 해서 계산해준다. 아래 식을 보면 Revenue 는 Row level calculation 이였던것을 기억하자. 즉 row level 보다는 늦을수밖에 없다는것을 알 수 있다.

![png](/assets/images/Tab_Fun/3_1.png)



# 9. Aggregate Calculation Filter

집계된 값에 대한 Filter 이다. 아래와 같이 매출(sum) 을 카테고리별로 나타낸 테이블을 생각해보자. 

![png](/assets/images/Tab_Fun/3_2.png)

이 때에 아래와 같이 측정값을 필터로 옮길 수 있다. (측정값 알약을 선택한 뒤에 오른쪽 클릭으로 filter 를 고를 수도 있다.)  그러면 우리가 집계할 수 있는 min, median 등등이 나오게 된다. 여기서 집계할 형식을 선택하자. 

![png](/assets/images/Tab_Fun/3_3.png)

그러면 그림과 같이 측정값에 대한 filter 를 만들 수 있다. 

![png](/assets/images/Tab_Fun/3_4.png)

다 만들고 나면 아래와 같이 집계된 값에 대해 필터가 걸리게 되어서, 값이 조금만 나타나게 된다. 

![png](/assets/images/Tab_Fun/3_5.png)



# 10. Densiflication

사이사이 값을 채우는 calculation 입니다. 이는 집계된 값을 사용하거나, 해아하므로 당연히 집계 연산보다는 낮은 우선순위를 가지고 있으며, 여기 10번 부터는 data source 에서 이루어지는 연산이 아니라 Tableau 에서 일어나는 연산이 되겠습니다. 

이 연산은 여기서 다루지는 않겠습니다. 나중에 좀 더 배우고 나서 하는게 더 좋을것같네요.





# 11. Blended Aggregate Filter

태블로에서 데이터를 블랜딩할떄 사용하는 필터 

# 12. Data Blending

Tableau 의 Data 항목에서 블랜딩을 확인해보세요! 서로 다른 데이터를 혼합할때에 나타나는 계산입니다. 

# 13. Table Calculation

테이블 Calculation 은 매우 낮은 수준에 있습니다. 이는 값들이 '집계된 이후' 에 일어나게 됩니다. 마치 이동평균같은 경우를 말합니다. 아래와 같이 집계된 값에 대하여, 뷰(테이블) 에서 Calculate 하는것이 Table Calculation 입니다. 

![png](/assets/images/Tab_Fun/3_8.png)

다음과 같은 예시로 알아보겠습니다. 제품 분류별 매출 테이블을 만들어보았습니다. 그 기준은 sum(매출) 로 집계된 데이터입니다.

![png](/assets/images/Tab_Fun/3_9.png)

SUM(매출)에 대해서 Table calculation 을 더해줍니다. 이때의 테이블 계산은 집계된값에 대해서 이루어지기 때문에, 당연히 순위가 후순위입니다. 

![png](/assets/images/Tab_Fun/3_10.png)

이제 다음과 같이 Calculation 타입을 정해주고, Table 에서 어떻게 적용할것인지(이런점떄문에 Table Calculation 이라고 불립니다.) 을 선택하면, SUM(매출) 옆에 삼각형 나타나는것을 볼 수 있습니다. 이는 집계된 값이 테이블 Calculation 으로 변모했다는 이야기입니다. 

![png](/assets/images/Tab_Fun/3_11.png)

# 14. Table Calculation Filter

테이블 계산 필터입니다. 즉 테이블 계산으로 이루어진 값을 Filter 로 적용하는것을 Table Calculation Filter 라고 합니다. 필터가 테이블에 나타난 값을 기준으로 일어나므로 당연히 순위는 Table Calcultion 보다 뒤입니다.

![png](/assets/images/Tab_Fun/3_12.png)

아래와 같이 Table Calulation(last) 을 필터로 올립니다. 

![png](/assets/images/Tab_Fun/3_13.png)

그 이후에 적용된것을 보면 필터링이 된것을 볼 수 있습니다.

![png](/assets/images/Tab_Fun/3_14.png)

# 15. Others...

그 이후는 중요하지 않으므로 넘어가겠습니다. 위에서 중요하게 봐야할것을 다시 정리해보겠습니다.

1. Row level 계산
2. Context 필터
3. Fixed 계산
4. 차원 필터
5. Include / Exclude 계산
6. 집계 계산 
7. 집계 필터
8. 테이블 계산
9. 테이블 계산 필터

위와 같은 순서가 중요합니다. 이를 기억하고 각각 상황에 맞추어 수준을 바꾸시면 원하는 계산 결과를 얻을 수 있습니다.

<br>

<Br>

**Referennce**

- https://community.tableau.com/s/question/0D54T00000C62Iz/using-a-table-calculation-as-filter
- https://www.tableau.com/about/blog/2019/9/understanding-how-tableau-calculation-types-work-together
- https://help.tableau.com/current/pro/desktop/ko-kr/order_of_operations.htm
- https://www.thedataschool.co.uk/harry-cooney/tableaus-order-of-operations

