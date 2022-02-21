---
title:  "Eulers number"
excerpt: "오일러 수 (자연상수 e)"
categories:
  - Elementary_Math
last_modified_at: 2021-12-23

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
use_math: true
---

 e 에 대해서 알아보자.
{: .notice--warning}

# [Euler numbers](#link){: .btn .btn--primary}{: .align-center}

> ## Definition

- 자연상수 계산 : $$e = \lim _{n \rightarrow \infty}\left(1+\frac{1}{n}\right)^{n}$$
  - $$e=\lim _{x \rightarrow 0}(1+x)^{\frac{1}{x}}$$ 라고도 함

> ## Example

> Example : $$\lim _{x \rightarrow 0} \frac{e^{x}-1}{x}=1$$

- $e^{x}-1=z$ 로 놓으면 $e^{x}=1+z$ 이므로 $x=\ln (1+z)$
- $x \rightarrow 0$ 일 때, $z \rightarrow 0$ 이므로 $\lim _{z \rightarrow 0} \frac{e^{z}-1}{x}=\lim _{z \rightarrow 0} \frac{z}{\ln (1+z)}=\lim _{z \rightarrow 0} \frac{1}{\frac{1}{z} \ln (1+z)}$
- 그런데 $\lim _{z \rightarrow 0} \frac{1}{z} \ln (1+z)=\lim _{z \rightarrow 0} \ln (1+z)^{\frac{1}{z}}=\ln e=1$
- 즉 $\therefore \lim _{x \rightarrow 0} \frac{e^{x}-1}{x}=1$

> Example : $$\lim _{x \rightarrow 0} \frac{\ln (1+x)}{x}=1$$

- 계산시 $$\lim _{x \rightarrow 0} \frac{\ln (1+x)}{x}=\lim _{x \rightarrow 0} \frac{1}{x} \ln (1+x)=\ln \lim _{x \rightarrow 0}(1+x)^{\frac{1}{z}}=\ln e=1$$



---

**Reference**

- https://en.wikipedia.org/wiki/E_(mathematical_constant)
- https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=sbssbi69&logNo=90164861352





