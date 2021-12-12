# A/B Testing

![image-20211209133544472](/Users/gorany/Desktop/Docs/Typora_Screenshot/image-20211209133544472.png)

홈페이지 개선을 하려고 한다고 가정하면 위처럼 2개의 그룹으로 나뉘게 됩니다. 그 이후 주요 지표를 계산하게 되고, 양 그룹간 주요 지표를 비교하게 됨

A/B Testing 가 매우 간단해 보이지만, 양질의 테스트를 하려면 지식과 연습이 필요함

# 라이프사이클 1 : Design

![image-20211209133724601](/Users/gorany/Desktop/Docs/Typora_Screenshot/image-20211209133724601.png)

- 대상선정
- 가설을 세움
- 샘플 사이즈를 계산 (독자적인 프로그램 사용)
- 메트릭을 정의 
- 실험 설계 단계에서부터 검증을 하기때문에 품질을 유지할 수 있음

# 라이프 사이클 2 : Implement

![image-20211209134029453](/Users/gorany/Desktop/Docs/Typora_Screenshot/image-20211209134029453.png)

- 위 단계는 도메인 팀 개발자가 실험에 들어갈 코드를 짜는 단계
  - 사실상 개발자의 단계라 자세한 설명은 생략

# 라이프 사이클 3 : Monitor

- 발생할 수 있는 이슈를 선제적으로 감지하고 이슈에게 알람을 보냄

![image-20211209134638984](/Users/gorany/Desktop/Docs/Typora_Screenshot/image-20211209134638984.png)

> 1.Circuir Breaker

- 실험이 시작되고 6시간동안 퍼널 내의 주요 두 단계에서 유니크한 방문자를 체크함
- 퍼널 내의 주요 두 단계에서 유니크 방문자들을 체크
  - 즉 장바구니에서 결제페이지 , 결제페이지에서 결제 완료로 가는 단계
- 해당 지표는 2분에 한번씩 체크 
- 만약 유의미한 악영향이 있어 고객이 구매퍼널 후반으로 이동하지 못하면, 고객 경험을 보호하기 위해 자동으로 실험을 중지시킴

> 2.Guardrail 지표

- 가드레일 지표는 탑라인 비즈니스 지표로 매우 중요한 지표 (모든 실험에서 중요)
- 어느 실험이든 가드레일 지표에 악영향을 주면 테스트 오너에게 알람을 보내 조사하게 함

> Imbalance (SRM)

- 실제 관찰된 트래픽 분배가 사전에 정의한 비율과 맞는지 검정
- 이러한 비율이 틀리면 imbalance 가 발생했다는 의미 (구현이 틀렸을것)
- 모든 지표결과가 유의하지 않았다면  구현에 문제가 있었을 확률이 큼 ! 

# 라이프 사이클 4,5 Analyze & Decide

![image-20211209134918237](/Users/gorany/Desktop/Docs/Typora_Screenshot/image-20211209134918237.png)



- 분석에서 중심이 되는것은 지표 계산
- 지표를 정확하고 면밀하게 분석하기 위해 다양한 분석이 사용됨

> Outlier Handling

- Removing
  - 알고리즘을 통해 비정상적인 행위 패턴을 보이는 고객을 매일 감시
  - 부정행위 감지팀이 정한 아웃라이어를 활용하기도함
  - 지표 계산시 해당 outlier 사용자 전체를 제외하게 됨
- Capping 
  - 지표의 근간이 되는 데이터가 크게 왜곡된 경우 지표 결과 자체도 왜곡되기 때문에 다소 복잡한 알고리즘을 사용해 데이터 분포를 데이터 분포를 체크하고, 필요한 경우 캐핑을 사용

> p value

- p-value 를 사용할때에는 특정 영향이 기능탓인지, 노이즈로 일어났는지를 체크하게 됨
- MDE 는 최소 탐지
- 미래 시점의 예측 MDE 를 예측하기 위한 알고리즘을 보유
  - 만일 미래 어느 시점에 대한 예측 MDE 가 위험관례 한계치보다 훨씬 크고 해당 실험을 계속 할 이유가 없다면 테스트를 빨리 종료하는것이 좋을 수 있음 

> Review

- 실험이 끝나면 실험을 리뷰하며, 여기서 승인되어야 런칭될 수 있음 

# Summary

![image-20211209135532354](/Users/gorany/Desktop/Docs/Typora_Screenshot/image-20211209135532354.png)

- 쿠팡의 비즈니스가 확대됨에 따라 많은 실험을 하고 있음! 
- 다양한 팀이 폭넓게 사용하고 있으며 하루에 1000개 이상의 지표를 실험중

# 실제 실험 화면

![image-20211209140448676](/Users/gorany/Desktop/Docs/Typora_Screenshot/image-20211209140448676.png)

- 테스트가 얼마나 진행되고 있는지, 상태가 어떤지 등을 살펴볼 수 있음 
  - 하나의 테스트를 먼저 들어가봅시다,

![image-20211209131118125](/Users/gorany/Desktop/Docs/Typora_Screenshot/image-20211209131118125.png)

- 위와 같이 다양한 것들을 볼 수 있습니다.
  - 아래에는 Guardrail 을 모니터링 하는 부분을 볼 수 있습니다. 

![image-20211209131137239](/Users/gorany/Desktop/Docs/Typora_Screenshot/image-20211209131137239.png)

- 자세히 보면 어떤것을 보고 있는지를 많이 알 수 있는데요
  - 첫번째로, Multiple Testing 을 하더라도, Control 과의 비교만 하고 있다는 점 
  - 양측검정을 무조건 Default 로 쓰고 있다는 점 
  - p-value 의 트랜드를 봄으로써 우연으로 일어나난 결과인지? 를 Monitoring 하는것으로 보임

![image-20211209131209389](/Users/gorany/Desktop/Docs/Typora_Screenshot/image-20211209131209389.png)

- 하나의 메트릭을 보고싶으면 위처럼 Daily 하세 볼수도 있음! 

