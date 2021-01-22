---
title:  "연산 함수"
excerpt: "R의 기초적인 연산,통계 등의 함수를 알아봅시다."
categories:
  - R_Basic
tags:
  - 기초
last_modified_at: 2021-01-23

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
---
# 수학 함수

{% highlight r %}
abs(-10) # 절대값
{% endhighlight %}



{% highlight text %}
## [1] 10
{% endhighlight %}



{% highlight r %}
sqrt(9) # 제곱근
{% endhighlight %}



{% highlight text %}
## [1] 3
{% endhighlight %}



{% highlight r %}
ceiling(9.4) # 올림
{% endhighlight %}



{% highlight text %}
## [1] 10
{% endhighlight %}



{% highlight r %}
floor(9.4) # 내림
{% endhighlight %}



{% highlight text %}
## [1] 9
{% endhighlight %}



{% highlight r %}
round(9.45,1) # 소수점 n자리까지 반올림
{% endhighlight %}



{% highlight text %}
## [1] 9.4
{% endhighlight %}



{% highlight r %}
log(100,base=10) # 밑이 10 인 log
{% endhighlight %}



{% highlight text %}
## [1] 2
{% endhighlight %}



{% highlight r %}
log(2.718) # 자연로그
{% endhighlight %}



{% highlight text %}
## [1] 0.9998963
{% endhighlight %}



{% highlight r %}
exp(2) # exponential 함수
{% endhighlight %}



{% highlight text %}
## [1] 7.389056
{% endhighlight %}



{% highlight r %}
factorial(3) 
{% endhighlight %}



{% highlight text %}
## [1] 6
{% endhighlight %}



{% highlight r %}
diff(c(1,3,4,5),lag=1) # 차분
{% endhighlight %}



{% highlight text %}
## [1] 2 1 1
{% endhighlight %}



{% highlight r %}
length(c(1,4,3,5)) #관측값 갯수
{% endhighlight %}



{% highlight text %}
## [1] 4
{% endhighlight %}
# 기술통계 함수

{% highlight r %}
x<-c(1,5,2,8,4) 
mean(x)   #평균
{% endhighlight %}



{% highlight text %}
## [1] 4
{% endhighlight %}



{% highlight r %}
median(x) #중앙값값
{% endhighlight %}



{% highlight text %}
## [1] 4
{% endhighlight %}



{% highlight r %}
var(x)    #분산
{% endhighlight %}



{% highlight text %}
## [1] 7.5
{% endhighlight %}



{% highlight r %}
sd(x)     #표준편차
{% endhighlight %}



{% highlight text %}
## [1] 2.738613
{% endhighlight %}



{% highlight r %}
min(x)    #최소
{% endhighlight %}



{% highlight text %}
## [1] 1
{% endhighlight %}



{% highlight r %}
max(x)    #최대
{% endhighlight %}



{% highlight text %}
## [1] 8
{% endhighlight %}



{% highlight r %}
range(x)  #범위
{% endhighlight %}



{% highlight text %}
## [1] 1 8
{% endhighlight %}



{% highlight r %}
length(x) #갯수 
{% endhighlight %}



{% highlight text %}
## [1] 5
{% endhighlight %}



{% highlight r %}
cumsum(x) #벡터누적합
{% endhighlight %}



{% highlight text %}
## [1]  1  6  8 16 20
{% endhighlight %}



{% highlight r %}
cumprod(x)#벡터누적곱
{% endhighlight %}



{% highlight text %}
## [1]   1   5  10  80 320
{% endhighlight %}



{% highlight r %}
rank(x)   #순서
{% endhighlight %}



{% highlight text %}
## [1] 1 4 2 5 3
{% endhighlight %}
# 통계 분포 함수 
beta        : beta  (shape1 shape2) <br>
binomial    : binom (size prob) <br>
chi-square  : chisq (df) <br>
unif        : unif  (min max) <br>
exp         : exp   (rate) # $pdf=re^{(-rx)}$ <br> 
F           : f     (df1 df2) <br>
gamma       : gamma (shape rate(scale)) <br>
note: scale 에 대해 shape * scale 이 mean, shape * scale^2 이 var <br>
geometric   : geom  (prob) <br> 
normal      : norm  (mean sd) <br>
poisson     : pois  (lambda) <br>
T           : t     (df) <br>
<br>
d--- : pdf/pmf <br>
p--- : cdf <br>
q--- : quantile <br>
r--- : random sample <br>


{% highlight r %}
rnorm(100) # 100개의 N(0,1) sample
{% endhighlight %}



{% highlight text %}
##   [1] -0.51486107  1.62454419 -1.11406000 -1.81887346 -0.45115911 -0.29220011
##   [7] -0.18932286 -0.99320736  0.60421787  0.34769643  0.91889825  0.71172373
##  [13] -1.56812551 -0.82013261  0.77452540  0.89990205  0.03982180 -1.69313369
##  [19]  1.26096718  1.18886016 -0.04805326  1.04827623 -0.09922206 -0.60699097
##  [25]  0.44216918 -0.02194928 -1.40591641  1.74609772  1.12598239 -0.22820512
##  [31]  0.01094715 -2.16279305  1.71268852  0.70921260 -0.92422666 -0.70319326
##  [37] -2.14617690 -0.34398487  0.21924757  0.55181557 -1.53840496  0.24206886
##  [43]  0.89694790  0.65616990  0.71413355  1.26109552 -1.30944480  0.50977556
##  [49]  0.70434740 -0.62387244 -0.42016074  1.09980610  0.01730196  0.98928846
##  [55] -0.11779552  1.31425434 -0.22039086  0.15603564 -0.29455189 -0.01943872
##  [61]  0.94572961 -0.51347868  1.52107017 -1.23258978 -0.50555493 -0.89629132
##  [67] -0.75750721  1.54966777  0.03214905  0.57236850  0.85810737  0.29717812
##  [73] -3.01868975  0.11390557 -1.78338275 -0.53197799  0.92693723  1.66420708
##  [79] -0.09362997  1.72840924 -1.31478204  1.49724465  2.79536597  0.45608787
##  [85] -0.77114132 -1.50553521  1.55402407 -1.14624430 -0.72501921 -1.08168341
##  [91]  1.02130976  1.25300900 -0.15140751  2.69330357  0.09970793 -0.04549826
##  [97] -0.77644721 -0.20146885  0.22035607 -0.18866954
{% endhighlight %}



{% highlight r %}
rexp(100,rate=1) 
{% endhighlight %}



{% highlight text %}
##   [1] 1.60384018 0.72855133 0.58697600 3.84523263 0.50500888 3.69654610 0.02534901
##   [8] 2.41876383 0.14417165 0.13159788 1.05091115 0.01300418 0.01297914 1.86359557
##  [15] 2.34727713 1.26986963 0.98523695 0.53589314 0.55770860 0.36313139 0.31244804
##  [22] 0.60641579 1.22406460 0.40372185 0.27428800 1.77448934 1.59705520 0.42755264
##  [29] 0.03667174 0.76313566 2.15347073 1.50137733 1.30699144 0.15644988 1.16070186
##  [36] 0.80148936 2.44139443 2.87488566 0.62060132 0.92541639 1.62451963 0.71579582
##  [43] 1.11174981 2.79130584 0.11030943 0.86152000 0.68596131 1.75951260 1.12221886
##  [50] 0.28365990 0.28225082 2.31703708 1.20780414 0.56683230 0.39104527 0.07307613
##  [57] 1.52552707 0.54059893 0.78922011 1.09568176 0.30374692 0.05024920 0.57537197
##  [64] 3.51944368 1.14904214 2.20597858 0.37312628 1.76783390 1.15106590 1.16821459
##  [71] 0.63793091 1.83681097 0.34543591 0.12274404 1.90044791 0.30775157 0.44586343
##  [78] 0.31107831 1.15516487 1.17574621 0.24223302 0.61478580 1.05075222 2.88363329
##  [85] 0.05824786 0.70687735 0.13669437 2.18925338 2.07864816 0.17099445 3.53343578
##  [92] 1.73279132 0.60777510 0.35704820 1.99236088 0.17401845 0.34610136 0.78221226
##  [99] 0.14126663 0.04088275
{% endhighlight %}



{% highlight r %}
dbinom(3,size=10,prob=0.25) # X ~ B(10,0.25) 에서 P(X=3)
{% endhighlight %}



{% highlight text %}
## [1] 0.2502823
{% endhighlight %}



{% highlight r %}
dpois(0:2,lambda = 4) # X ~ pois(4) 에서 P(X=0,1,2)
{% endhighlight %}



{% highlight text %}
## [1] 0.01831564 0.07326256 0.14652511
{% endhighlight %}



{% highlight r %}
pnorm(12,mean=10,sd=2) # X~N(10,4) 에서 P(X <= 12)
{% endhighlight %}



{% highlight text %}
## [1] 0.8413447
{% endhighlight %}



{% highlight r %}
qt(0.95,df=20) # 95th percentile of t(20) 즉 왼쪽꼬리의 값이 0.95 
{% endhighlight %}



{% highlight text %}
## [1] 1.724718
{% endhighlight %}



{% highlight r %}
qt(0.05,df=20,lower.tail = F) # 즉 오른쪽 꼬리의 확률이 0.05
{% endhighlight %}



{% highlight text %}
## [1] 1.724718
{% endhighlight %}

# 논리 연산

{% highlight r %}
x<-c(1:5) 
y<-c(5:1)

# elementwise 하게 수행이 된다.
x*y
{% endhighlight %}



{% highlight text %}
## [1] 5 8 9 8 5
{% endhighlight %}



{% highlight r %}
x+y
{% endhighlight %}



{% highlight text %}
## [1] 6 6 6 6 6
{% endhighlight %}



{% highlight r %}
#비교
x>=y
{% endhighlight %}



{% highlight text %}
## [1] FALSE FALSE  TRUE  TRUE  TRUE
{% endhighlight %}



{% highlight r %}
x<=y
{% endhighlight %}



{% highlight text %}
## [1]  TRUE  TRUE  TRUE FALSE FALSE
{% endhighlight %}



{% highlight r %}
x>y 
{% endhighlight %}



{% highlight text %}
## [1] FALSE FALSE FALSE  TRUE  TRUE
{% endhighlight %}



{% highlight r %}
x!=y #서로 같지 않다.
{% endhighlight %}



{% highlight text %}
## [1]  TRUE  TRUE FALSE  TRUE  TRUE
{% endhighlight %}



{% highlight r %}
#논리
(3 <= x) & (x <= 4) # and
{% endhighlight %}



{% highlight text %}
## [1] FALSE FALSE  TRUE  TRUE FALSE
{% endhighlight %}



{% highlight r %}
(3 <= x) | (x <= 4) # or
{% endhighlight %}



{% highlight text %}
## [1] TRUE TRUE TRUE TRUE TRUE
{% endhighlight %}



{% highlight r %}
any(3<=x) # 하나여도 맞으면 true
{% endhighlight %}



{% highlight text %}
## [1] TRUE
{% endhighlight %}



{% highlight r %}
all(3<=x) # 모두 맞아야 true
{% endhighlight %}



{% highlight text %}
## [1] FALSE
{% endhighlight %}

# 특수 연산

{% highlight r %}
x
{% endhighlight %}



{% highlight text %}
## [1] 1 2 3 4 5
{% endhighlight %}



{% highlight r %}
y
{% endhighlight %}



{% highlight text %}
## [1] 5 4 3 2 1
{% endhighlight %}



{% highlight r %}
x%%3 #나머지
{% endhighlight %}



{% highlight text %}
## [1] 1 2 0 1 2
{% endhighlight %}



{% highlight r %}
x%/%3 #몫
{% endhighlight %}



{% highlight text %}
## [1] 0 0 1 1 1
{% endhighlight %}



{% highlight r %}
x%*%y #행렬곱
{% endhighlight %}



{% highlight text %}
##      [,1]
## [1,]   35
{% endhighlight %}



{% highlight r %}
x%in%2 #벡터내 특정값 포함여부
{% endhighlight %}



{% highlight text %}
## [1] FALSE  TRUE FALSE FALSE FALSE
{% endhighlight %}

#행렬 연산 함수

{% highlight r %}
A <- matrix(c(1,6,3,
              4,2,5,
              8,7,9), byrow=TRUE,nrow=3)
B <- matrix(c(1,1,1,
              -1,-1,-1,
              0,0,0),byrow=TRUE,nrow=3)
t(A) #transpose
{% endhighlight %}



{% highlight text %}
##      [,1] [,2] [,3]
## [1,]    1    4    8
## [2,]    6    2    7
## [3,]    3    5    9
{% endhighlight %}



{% highlight r %}
diag(c(1,2,3,4)) #대각행렬
{% endhighlight %}



{% highlight text %}
##      [,1] [,2] [,3] [,4]
## [1,]    1    0    0    0
## [2,]    0    2    0    0
## [3,]    0    0    3    0
## [4,]    0    0    0    4
{% endhighlight %}



{% highlight r %}
diag(4) #항등행렬
{% endhighlight %}



{% highlight text %}
##      [,1] [,2] [,3] [,4]
## [1,]    1    0    0    0
## [2,]    0    1    0    0
## [3,]    0    0    1    0
## [4,]    0    0    0    1
{% endhighlight %}



{% highlight r %}
solve(A) #역행렬
{% endhighlight %}



{% highlight text %}
##             [,1]       [,2]       [,3]
## [1,] -0.39534884 -0.7674419  0.5581395
## [2,]  0.09302326 -0.3488372  0.1627907
## [3,]  0.27906977  0.9534884 -0.5116279
{% endhighlight %}



{% highlight r %}
det(A) #det
{% endhighlight %}



{% highlight text %}
## [1] 43
{% endhighlight %}



{% highlight r %}
A*B # elementwise 연산
{% endhighlight %}



{% highlight text %}
##      [,1] [,2] [,3]
## [1,]    1    6    3
## [2,]   -4   -2   -5
## [3,]    0    0    0
{% endhighlight %}



{% highlight r %}
A%*%B # 행렬연산
{% endhighlight %}



{% highlight text %}
##      [,1] [,2] [,3]
## [1,]   -5   -5   -5
## [2,]    2    2    2
## [3,]    1    1    1
{% endhighlight %}



{% highlight r %}
# 1~10 의 vector 만들기
{% endhighlight %}

# 인덱싱

{% highlight r %}
x<-c(1:5) 
y<-c(5:1)
#x[i] : 벡터의 i번째 값을 보여준다.
x[2]
{% endhighlight %}



{% highlight text %}
## [1] 2
{% endhighlight %}



{% highlight r %}
#x[i] <- 3 : 벡터의 i번째 값을 3 으로 치환한다.
x[2] = 99

#x[-i] : 벡터의 i번쨰 값을 없애고 보여준다.
x[-2]
{% endhighlight %}



{% highlight text %}
## [1] 1 3 4 5
{% endhighlight %}



{% highlight r %}
#x[n:m] : 벡터의 n~m 값을 보여준다.
x[2:4]
{% endhighlight %}



{% highlight text %}
## [1] 99  3  4
{% endhighlight %}



{% highlight r %}
#apppend(x,y) : x와y 를 연결한다.
append(x,y)
{% endhighlight %}



{% highlight text %}
##  [1]  1 99  3  4  5  5  4  3  2  1
{% endhighlight %}


{% highlight r %}
x = c(1,2,3,4)
names(x) = c('a','b','c','d') # 이렇게 인덱싱을 달게되면
x[c(2,4)] # 위치로 인덱싱
{% endhighlight %}



{% highlight text %}
## b d 
## 2 4
{% endhighlight %}



{% highlight r %}
x[c(-1,-3)] # - 값은 제외하여 인덱싱
{% endhighlight %}



{% highlight text %}
## b d 
## 2 4
{% endhighlight %}



{% highlight r %}
x[c(TRUE,TRUE,FALSE,TRUE)] # T,F 로 인덱싱
{% endhighlight %}



{% highlight text %}
## a b d 
## 1 2 4
{% endhighlight %}



{% highlight r %}
x[c('a','c')] # names 했던 문자로 인덱싱
{% endhighlight %}



{% highlight text %}
## a c 
## 1 3
{% endhighlight %}

# 벡터의 집합연산

{% highlight r %}
x
{% endhighlight %}



{% highlight text %}
## a b c d 
## 1 2 3 4
{% endhighlight %}



{% highlight r %}
y
{% endhighlight %}



{% highlight text %}
## [1] 5 4 3 2 1
{% endhighlight %}



{% highlight r %}
union(x,y) #x,y 의 합집합
{% endhighlight %}



{% highlight text %}
## [1] 1 2 3 4 5
{% endhighlight %}



{% highlight r %}
intersect(x,y) #x,y 의 교집합
{% endhighlight %}



{% highlight text %}
## [1] 1 2 3 4
{% endhighlight %}



{% highlight r %}
setdiff(x,y) #x,y 의 차집합
{% endhighlight %}



{% highlight text %}
## numeric(0)
{% endhighlight %}
