---

title:  "Tableau with ipynb,md"
excerpt: "테블로를 ipynb, md에 올려봅시다."
categories:

  - Tableau
tags:
  - 1
last_modified_at: 2021-02-08

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true

---

# ipynb

- 테블로의 결과를 ipynb 와 같이 보고싶다면(즉 ipynb) 에 첨부하고 싶을때 아래와 같이 하면 된다.

- ipynb 의 셀 안에 %%HTML 를 입력 후 

  ![png](/assets/images/Tableau/b1.PNG)

- 위의 사진처럼 공유를 누른 상태에서, 내장코드의 값을 집어넣자. 

  ![png](/assets/images/Tableau/b2.PNG)

- 그럼 위와 같이 파이썬 ipynb 파일 위로 interactive 한 뷰가 생성된다.

- (note) : 이떄 주의할 점이 미리 Visualization 을 public 에 업로드 해야한다.



# md

- md 파일은 어떻게 해야할까?

  ![png](/assets/images/Tableau/b1.PNG)

- 이 때에는 위의 공유에서 아래쪽의 link 를 복사한다.

- https://public.tableau.com/views/1_16042552319710/Sheet12?:language=ko&:display_count=y&:origin=viz_share_link

- 그러면 위와 같이 링크가 형성되는데, 이때 중요한것은 ? 전의 https://public.tableau.com/views/1_16042552319710/Sheet12 값이다. 이를

- src 부분의 ? 전 링크에 다 붙여넣는다.

  ![png](/assets/images/Tableau/b3.PNG)

- 위와 같이 링크를 붙여넣고 md 에 넣으면 자동으로 html 로 인식해준다!

<iframe seamless frameborder="0" src="https://public.tableau.com/views/1_16042552319710/Sheet12?:embed=yes&:display_count=yes&:showVizHome=no" width = '750' height = '600' scrolling='yes' ></iframe>

- 완성!