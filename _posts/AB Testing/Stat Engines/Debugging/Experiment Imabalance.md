---
title: "Debugging Experiment"
excerpt: "문제가 생겼을떄 대처하기"
tags :
  - AB_Stat
last_modified_at: 2022-02-26

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math: true

---

CUPED 방법론을 활용해서 Metric 의 Sensitivity 를 높히는 방법
{: .notice--warning}

# Experiment Imbalanced 

- Online Experimentation Diagnosis and Troubleshooting Beyond AA Validation
- https://www.researchgate.net/publication/312211485_Online_Experimentation_Diagnosis_and_Troubleshooting_Beyond_AA_Validation

```
Finding the root cause of experiment imbalance requires knowledge of and investigation into the experimentation plat- form and engineering code base. Observing symptoms and understanding which components may be responsible for any imbalance is critical for remedying the problems. Previous papers have documented important lessons learned from the design and analysis of online experimentation [27], [29], [31]. In related field, practical difficulties and solutions for customer sentiment survey was also discussed [40]. One feature of this paper is providing examples with real data linking experiment quality validation test, symptoms, root causes, and remedies.
```

- experiment imabalance 를 해결하기 위해서는, Experimentation Platform 에 대한 이해와 , Code  Base 부터의 지식이 필요합니다. 
- 실험 불균형에 대한 증상을 살펴보고, 실험플랫폼의 어떠한 Component 가 이러한 불균형을 일으키는지에 대해서 살펴보는것이 중요합니다.
- 이러한 불균형에 대해서는 다양한 Paper 에서 연구되었습니다.
  - R. Kohavi, A. Deng, B. Frasca, R. Longbotham, T. Walker, and Y. Xu. Trustworthy online controlled experiments: Five puzzling outcomes explained. In *Proceedings of the 18th ACM SIGKDD international conference on Knowledge discovery and data mining*, pages 786–794. ACM, 2012.
  - R. Kohavi, A. Deng, R. Longbotham, and Y. Xu. Seven rules of thumb for web site experimenters. In *Proceedings of the 20th ACM SIGKDD international conference on Knowledge discovery and data mining*, pages 1857–1866. ACM, 2014.
  - R. Kohavi and R. Longbotham. Unexpected results in online controlled experiments. *ACM SIGKDD Explorations Newsletter*, 12(2):31–35, 2011.
- 관련된 분야에서, customer sentiment survey 에 대한 위한 실질적인 어려움과 해결책도 논의되었다
  - 이 논문의 한 가지 특징은 실험 품질 검증 테스트, 증상, 근본 원인 및 치료법을 연결하는 실제 데이터의 예를 제공한다는 것입니다.
  - 이러한 Lesson 에서 우리는 