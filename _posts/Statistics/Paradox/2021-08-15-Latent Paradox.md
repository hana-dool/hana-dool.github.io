---
title:  "Latent Variable Paradox"
excerpt: "잠재변수를 고려한 해석을 해야한다."
categories:
  - Stat_Paradox
tags:
  - 1
last_modified_at: 2021-08-15

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true
---

<br>

# Latent Variable

- 잠재변수를 고려하지 않으면, 두 변수간의 해석을 잘못할 수 있으므로 조심해야 합니다.

- 예를 들어 화재를 진압하기 위해 배치된 소방관의 수와 화재로 인한 부상자 수 사이의 관계를생각해봅시다.
- 상식적으로는 소방관이 많을수록 부상자가 줄어들기를 기대하지만 집계 데이터에서는 오히려 양의 상관 관계가 나오는 이상한 현상이 발생할 수 있습니다.
- 이 경우 소방관이 많이 배치될수록 부상자 수도 많다는 이상한 결론을 내리게 될 것입니다. 

![png](/assets/images/Stat/39_2.png)

- 이건 “화재 심각도”라는 잠재변수를 간과했기 때문입니다.
  -  심각한 화재일수록 더 많은 부상을 초래하는 경향이 있으며, 자연히 더 많은 소방관을 투입해야 합니다

![png](/assets/images/Stat/39_1.png)

- 위 그림에서 오른쪽은 이러한 '화재 심각도' 변수를 고정시킨 상태에서 실험을 한 경우입니다.
- 이렇게 잠재변수를 잘 통제해야 정확한 결과를 얻을 수 있습니다.

<br>

