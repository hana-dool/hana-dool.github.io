---
title:  "Github BLog Markdown"
excerpt: "깃허브 블로그 특수기호입력"
categories:
  - Others
tags:
  - 3
last_modified_at: 2021-09-11

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true

use_math : true
---

- 아래와 같은 설정들을 통하여, 깃허브 블로그를 다채롭게 이용할 수 있습니다.

# [버튼 설정](#link){: .btn .btn--primary} 

```
[Default Button Text](#link){: .btn}
[Primary Button Text](#link){: .btn .btn--primary}
[Success Button Text](#link){: .btn .btn--success}
[Warning Button Text](#link){: .btn .btn--warning}
[Danger Button Text](#link){: .btn .btn--danger}
[Info Button Text](#link){: .btn .btn--info}
[Inverse Button](#link){: .btn .btn--inverse}
[Light Outline Button](#link){: .btn .btn--light-outline}
```

[Default Button Text](#link){: .btn}
[Primary Button Text](#link){: .btn .btn--primary}
[Success Button Text](#link){: .btn .btn--success}
[Warning Button Text](#link){: .btn .btn--warning}
[Danger Button Text](#link){: .btn .btn--danger}
[Info Button Text](#link){: .btn .btn--info}
[Inverse Button](#link){: .btn .btn--inverse}
[Light Outline Button](#link){: .btn .btn--light-outline}

| Button Type   | Example                                                      | Class                      | Kramdown                                    |
| :------------ | :----------------------------------------------------------- | :------------------------- | :------------------------------------------ |
| Default       | [Text](https://mmistakes.github.io/minimal-mistakes/docs/utility-classes/#link) | `.btn`                     | `[Text](#link){: .btn}`                     |
| Primary       | [Text](https://mmistakes.github.io/minimal-mistakes/docs/utility-classes/#link) | `.btn .btn--primary`       | `[Text](#link){: .btn .btn--primary}`       |
| Success       | [Text](https://mmistakes.github.io/minimal-mistakes/docs/utility-classes/#link) | `.btn .btn--success`       | `[Text](#link){: .btn .btn--success}`       |
| Warning       | [Text](https://mmistakes.github.io/minimal-mistakes/docs/utility-classes/#link) | `.btn .btn--warning`       | `[Text](#link){: .btn .btn--warning}`       |
| Danger        | [Text](https://mmistakes.github.io/minimal-mistakes/docs/utility-classes/#link) | `.btn .btn--danger`        | `[Text](#link){: .btn .btn--danger}`        |
| Info          | [Text](https://mmistakes.github.io/minimal-mistakes/docs/utility-classes/#link) | `.btn .btn--info`          | `[Text](#link){: .btn .btn--info}`          |
| Inverse       | [Text](https://mmistakes.github.io/minimal-mistakes/docs/utility-classes/#link) | `.btn .btn--inverse`       | `[Text](#link){: .btn .btn--inverse}`       |
| Light Outline | [Text](https://mmistakes.github.io/minimal-mistakes/docs/utility-classes/#link) | `.btn .btn--light-outline` | `[Text](#link){: .btn .btn--light-outline}` |

```
[X-Large Button](#link){: .btn .btn--primary .btn--x-large}
[Large Button](#link){: .btn .btn--primary .btn--large}
[Default Button](#link){: .btn .btn--primary }
[Small Button](#link){: .btn .btn--primary .btn--small}
```

[X-Large Button](#link){: .btn .btn--primary .btn--x-large}
[Large Button](#link){: .btn .btn--primary .btn--large}
[Default Button](#link){: .btn .btn--primary }
[Small Button](#link){: .btn .btn--primary .btn--small}

| Button Size | Example                                                      | Class                              | Kramdown                                            |
| :---------- | :----------------------------------------------------------- | :--------------------------------- | :-------------------------------------------------- |
| X-Large     | [X-Large Button](https://mmistakes.github.io/minimal-mistakes/docs/utility-classes/#) | `.btn .btn--primary .btn--x-large` | `[Text](#link){: .btn .btn--primary .btn--x-large}` |
| Large       | [Large Button](https://mmistakes.github.io/minimal-mistakes/docs/utility-classes/#) | `.btn .btn--primary .btn--large`   | `[Text](#link){: .btn .btn--primary .btn--large}`   |
| Default     | [Default Button](https://mmistakes.github.io/minimal-mistakes/docs/utility-classes/#) | `.btn .btn--primary`               | `[Text](#link){: .btn .btn--primary }`              |
| Small       | [Small Button](https://mmistakes.github.io/minimal-mistakes/docs/utility-classes/#) | `.btn .btn--primary .btn--small`   | `[Text](#link){: .btn .btn--primary .btn--small}`   |

# [문자 박스 설정](#link){: .btn .btn--primary} 

- 텍스트를 입력하고, 그 뒤 shift enter 를 입력후에 (typora 에서 입력시) , {,} 안에 아래의 class 를 넣어주면 된다.

| Notice Type | Class              |
| ----------- | ------------------ |
| Default     | `.notice`          |
| Primary     | `.notice--primary` |
| Info        | `.notice--info`    |
| Warning     | `.notice--warning` |
| Success     | `.notice--success` |
| Danger      | `.notice--danger`  |

**Default 문자 박스입니다.** 문자 박스를 이용하여 원하는 문장을 좀 더 강조하여 보여줄 수 있습니다. <br>흔히 p-value가 0.05 이하면 가설이 틀릴 가능성이 낮다고 보고 논문을 출판했으나, 0.005로 기준을 높여야 한다는 주장이 근래에 많이 나오고 있다. 문제는 이렇게 한다고 해서 마냥 이 논란이 잠잠해지지도 않는다는 것. 이 경우 도리어 방법론 연구자들이 가장 극렬하게 반발한다. 실제로 국내의 한국심리학회 학술대회에서도 p-값을 강화하자는 주장을 소개하면서 문제가 많은 주장이라고 비판하는 논자도 있었다. 실험설계 및 사회연구 자체의 특성상, 출판 기준을 그렇게 높여 버리면 오히려 영가설을 기각해야 하는데 기각하지 못하는 새로운 통계적 오류가 발생한다는 것이며, 사회과학은 그 오류를 줄일 수 있는 연구주제가 아니라는 것이다. 또한 사회과학의 통계는 반드시 실증을 최우선하기보다는 기존 문헌과의 실질적인(substantive) 연관성을 함께 고려해야 하므로 항상 통계적 엄격함을 견지하는 게 힘들다. 그렇기 때문에 이런 논의는 오히려 자연과학 연구자들에게 좀 더 생산적인 효과를 내고 있으며, 사회과학자들은 입맛만 다시고 있는 중이다(…).
{: .notice}

#**Primary 문자 박스입니다.** 문자 박스를 이용하여 원하는 문장을 좀 더 강조하여 보여줄 수 있습니다
{: .notice--primary}

**Info 문자 박스입니다.** 문자 박스를 이용하여 원하는 문장을 좀 더 강조하여 보여줄 수 있습니다
{: .notice--info}

**Warning 문자 박스입니다.** 문자 박스를 이용하여 원하는 문장을 좀 더 강조하여 보여줄 수 있습니다
{: .notice--warning}

**Success 문자 박스입니다.** 문자 박스를 이용하여 원하는 문장을 좀 더 강조하여 보여줄 수 있습니다
{: .notice--success}

**Danger 문자 박스입니다.** 문자 박스를 이용하여 원하는 문장을 좀 더 강조하여 보여줄 수 있습니다
{: .notice--danger}



# [인용 문구](#link){: .btn .btn--primary} 

```
> 내용
>> 내용
>>> 내용
>>>> 내용
```

> 내용
> > 내용
> > > 내용
> > >
> > > > 내용

