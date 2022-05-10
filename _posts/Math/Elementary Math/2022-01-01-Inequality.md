---
title:  "HM-GM-AM-QM inequalities"
excerpt: "평균 부등식"
categories:
  - Elementary_Math
last_modified_at: 2021-12-23

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
use_math: true
typora-root-url: ../../../../hana-dool.github.io
---

 기초 Inequality
{: .notice--warning}

# [Another Inequality](#link){: .btn .btn--primary}{: .align-center}

> ## Terminology

- 최댓값 (Max): 말 그대로 최댓값 $\left(=\max \left(x_{1}, x_{2}, \cdots, x_{n}\right)\right)$
- 제곱근 멱평균/제곱 평균 제곱근 (RMS: Root-Mean Square) $: \sqrt{\frac{x_{1}^{2}+x_{2}^{2}+\cdots+x_{n}^{2}}{n}}$
- 산술평균 (AM: Arithmetic Mean): $\frac{x_{1}+x_{2}+\cdots+x_{n}}{n}$
- 기하평균 (GM: Geometric Mean): $\sqrt[n]{x_{1} x_{2} \cdots x_{n}}$
- 조화평균 (HM: Harmonic Mean): $\frac{n}{\frac{1}{x_{1}}+\frac{1}{x_{2}}+\cdots+\frac{1}{x_{n}}}$ (역수들의 산술평균의 역수)
- 최솟값 (Min): 말 그대로 최솟값 $$\left.\left.\left(=\min \left(x_{1}, x_{2}, \cdots, x_{n}\right)\right)\right\}\right\}$$

> ## HM-GM-AM-QM inequalities

- $n$ 개의 양수 $x_{1}, x_{2}, \cdots, x_{n}$ 에 대하여 $\mathrm{MAX} \geq \mathrm{RMS} \geq \mathrm{AM} \geq \mathrm{GM} \geq \mathrm{HM} \geq \mathrm{MIN}$, 즉 다음이 성립한다.

$$\begin{aligned} \max \left(x_{1}, x_{2}, \cdots, x_{n}\right) 
&\geq \sqrt{\frac{x_{1}^{2}+x_{2}^{2}+\cdots+x_{n}^{2}}{n}} \\ 
&\geq \frac{x_{1}+x_{2}+\cdots+x_{n}}{n}\\
&\geq \sqrt[n]{x_{1} x_{2} \cdots x_{n}} \\
&\geq \frac{n}{\frac{1}{x_{1}}+\frac{1}{x_{2}}+\cdots+\frac{1}{x_{n}}} \\&\geq \min \left(x_{1}, x_{2}, \cdots, x_{n}\right)\end{aligned}$$

- $x_{1}=x_{2}=\cdots=x_{n}$ 이 아니면 등호가 성립하지 않는다.

> proof MAX $\geq$ RMS

- WLOG $x_{1} \geq x_{2} \geq \cdots \geq x_{n}$ 이라 가정한다. 
- 그러면 $\max \left(x_{1}, x_{2}, \cdots, x_{n}\right)=x_{1}=\sqrt{\frac{n x_{1}^{2}}{n}} \geq \sqrt{\frac{x_{1}^{2}+x_{2}^{2}+\cdots+x_{n}^{2}}{n}}$. 곧, MAX $\geq$ RMS

> proof MAX $\geq$ AM

- 코시-슈바르츠 부등식에 의해, $\left(x_{1}{ }^{2}+x_{2}{ }^{2}+\cdots+x_{n}{ }^{2}\right)(1+1+\cdots+1) \geq\left(x_{1}+x_{2}+\cdots+x_{n}\right)^{2}$ 이다. 
- 양변을 $n^{2}$ 으로 나눠주고 정리하면, $\frac{x_{1}^{2}+x_{2}^{2}+\cdots+x_{n}^{2}}{n} \geq\left(\frac{x_{1}+x_{2}+\cdots+x_{n}}{n}\right)^{2}$. 
- 양변에 제곱근을 씌워주면, $\sqrt{\frac{x_{1}^{2}+x_{2}^{2}+\cdots+x_{n}^{2}}{n}} \geq \frac{x_{1}+x_{2}+\cdots+x_{n}}{n}$. 
- 즉, RMS $\geq \mathrm{AM}$ 이 성립한다.

> proof $AM \ge GM$  

$X=\frac{a_{1}+a_{2}+\cdots+a_{n}}{n}$ 라 하면 다음이 성립한다.
$$
\begin{aligned}
e^{\left(a_{1} / X\right)-1} & \geq \frac{a_{1}}{X} \\
e^{\left(a_{2} / X\right)-1} & \geq \frac{a_{2}}{X} \\
& \vdots \\
e^{\left(a_{n} / X\right)-1} & \geq \frac{a_{n}}{X}
\end{aligned}
$$
에서 이를 모두 곱하면
$$
e^{\left(a_{1}+a_{2}+\cdots+a_{n}\right) / X-n} \geq \frac{a_{1}}{X} \frac{a_{2}}{X} \cdots \frac{a_{n}}{X}
$$
$$
\begin{aligned}
\text { 이때 } \frac{a_{1}+a_{2}+\cdots+a_{n}}{X}-n=n-n &=0, \text { 따라서 } \\
e^{0}=1 & \geq \frac{a_{1} a_{2} \cdots a_{n}}{X^{n}} \\
X^{n} & \geq a_{1} a_{2} \cdots a_{n} \\
\therefore \frac{a_{1}+a_{2}+\cdots+a_{n}}{n} & \geq\left(a_{1} a_{2} \cdots a_{n}\right)^{\frac{1}{n}}
\end{aligned}
$$

> Proof $\mathrm{GM} \geq \mathrm{HM}$ 

- AM-GM을 활용한다. $\frac{\sum_{k=1}^{n} \sqrt[n]{\frac{x_{1} x_{2} \cdots x_{n}}{x_{k} n}}}{n} \geq 1$ 이므로, 
- 이를 잘 정리해주면, $\sqrt[n]{x_{1} x_{2} \cdots x_{n}} \frac{\sum_{k=1}^{n} \frac{1}{x_{k}}}{n} \geq 1$ 이다. 
- 즉, $\sqrt[n]{x_{1} x_{2} \cdots x_{n}} \geq$ $\frac{n}{\frac{1}{x_{1}}+\frac{1}{x_{2}}+\cdots+\frac{1}{x_{n}}}$. 즉, $\mathrm{GM} \geq \mathrm{HM}$ 이 성립한다.

> Proof $HM \geq MIN$

- WLOG $x_{1} \geq x_{2} \geq \cdots \geq x_{n}$ 이라 가정한다. 
- 그러면 $\min \left(x_{1}, x_{2}, \cdots, x_{n}\right)=x_{n}=\frac{n}{\frac{1}{x_{n}}+\frac{1}{x_{n}}+\cdots+\frac{1}{x_{n}}} \leq \frac{n}{\frac{1}{x_{1}}+\frac{1}{x_{2}}+\cdots+\frac{1}{x_{n}}} .$ 
- 즉, $HM \geq MIN$이 성립한다.

> ## p 차 멱평균

- **멱평균**(power mean) 혹은 일반화된 평균(generalized mean)은, 확장된 실수(즉 실수에 +무한대와 -무한대를 첨가한것) p*p*에 대해 다음과 같이 정의될 수 있다.
  - $p$ 차 멱평균: $M_{p}\left(x_{1}, \cdots, x_{n}\right)=\left(\frac{x_{1}^{p}+x_{2}^{p}+\cdots+x_{n}^{p}}{n}\right)^{1 / p}$

> **멱평균 부등식** (power mean inequality) 혹은 일반화된 평균 부등식(generalized mean inequality)

- $n$ 개의 양수 $x_{1}, x_{2}, \cdots, x_{n}$ 에 대하여, $M_{p}\left(x_{1}, x_{2}, \cdots, x_{n}\right)$ 는 $p$ 에 대해 단조증가한다. $x_{1}=x_{2}=\cdots=x_{n}$ 이 아니면 순증가이다.

> Note

- 위의 모든 평균들은 다 이 멱평균의 특수한 예로, 최대값/제곱평균제곱근/산술평균/기하평균/조화평균/최소값은 각각 $p=+\infty, 2,1,0,-1,-\infty$ 에 대응됩니다.
  - 즉 이는 HM-GM-AM-QM Inequality 일반화라 볼 수 있습니다.
- 더욱 일반화하면 이런 류의 것이 다 그렇듯 가중치가 있는 버전, 적분형 버전 등도 당연히 생각할 수 있고, 가장 일반적인 [측도](https://namu.wiki/w/측도)버전은 다음일 것이다.
  - 음이 아닌 확률변수 $X$ 에 대해 $\mathbb{E}\left[X^{p}\right]^{1 / p}$ 는 $-\infty \leq p \leq \infty$ 에서 단조증가이다.

---

**Reference**

- <https://namu.wiki/w/%EB%8D%B8(%EC%97%B0%EC%82%B0%EC%9E%90)#s-3.1>
- https://ko.wikipedia.org/wiki/%EA%B8%B0%EC%9A%B8%EA%B8%B0_(%EB%B2%A1%ED%84%B0)



