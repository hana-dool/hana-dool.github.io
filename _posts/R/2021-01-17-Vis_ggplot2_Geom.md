---
title:  "ggplot2 Geom Cheat sheet"
excerpt: "ggplot2 의 기본적 plot 예시를 알아봅시다."
categories:
  - R_Visualization
tags:
  - 시각화
last_modified_at: 2021-01-16

toc: true
toc_label: "Table Of Contents"
toc_icon: "cog"
toc_sticky: true
---

# Tip
아래 그래프는 R-studio 에서 제공하는 cheat sheet 의 내용이다. <br>
geom 은 그래프의 전체적 모양새를 가늠짓는 함수로 제일 중요하다 할 수 있다. <br>

{% highlight r %}
library('ggplot2')
args(geom_col) #이를 통해서 (또는?) 그 함수의 default 설정을 알 수 있다.
{% endhighlight %}



{% highlight text %}
## function (mapping = NULL, data = NULL, position = "stack", ..., 
##     width = NULL, na.rm = FALSE, show.legend = NA, inherit.aes = TRUE) 
## NULL
{% endhighlight %}

# 1연속형

{% highlight r %}
a <- ggplot(mpg, aes(hwy))
{% endhighlight %}

## Area plot

{% highlight r %}
a + geom_area(stat = "bin")
{% endhighlight %}

![plot of chunk unnamed-chunk-51](/assets/images/Vis_ggplot2_Geom/unnamed-chunk-51-1.png)

## density plot

{% highlight r %}
a + geom_density(kernel = "gaussian")
{% endhighlight %}

![plot of chunk unnamed-chunk-52](/assets/images/Vis_ggplot2_Geom/unnamed-chunk-52-1.png)

## 쌓인 점 plot

{% highlight r %}
a + geom_dotplot()
{% endhighlight %}

![plot of chunk unnamed-chunk-53](/assets/images/Vis_ggplot2_Geom/unnamed-chunk-53-1.png)

## 빈도수 plot

{% highlight r %}
a + geom_freqpoly()
{% endhighlight %}

![plot of chunk unnamed-chunk-54](/assets/images/Vis_ggplot2_Geom/unnamed-chunk-54-1.png)

## 히스토그램

{% highlight r %}
a + geom_histogram(binwidth = 5)
{% endhighlight %}

![plot of chunk unnamed-chunk-55](/assets/images/Vis_ggplot2_Geom/unnamed-chunk-55-1.png)

# 1범주형
## g

{% highlight r %}
b <- ggplot(mpg, aes(fl))
b + geom_bar()
{% endhighlight %}

![plot of chunk unnamed-chunk-56](/assets/images/Vis_ggplot2_Geom/unnamed-chunk-56-1.png)


# 2연속+연속
## jitter scatter

{% highlight r %}
e <- ggplot(mpg, aes(cty, hwy))
e + geom_jitter()
{% endhighlight %}

![plot of chunk unnamed-chunk-57](/assets/images/Vis_ggplot2_Geom/unnamed-chunk-57-1.png)

## scatter

{% highlight r %}
e + geom_point()
{% endhighlight %}

![plot of chunk unnamed-chunk-58](/assets/images/Vis_ggplot2_Geom/unnamed-chunk-58-1.png)

## quantile plot
95% 범위를 세개의 선으로 표시

{% highlight r %}
e + geom_quantile()
{% endhighlight %}

![plot of chunk unnamed-chunk-59](/assets/images/Vis_ggplot2_Geom/unnamed-chunk-59-1.png)

## 축에 rug표시

{% highlight r %}
e + geom_rug(sides = "bl")
{% endhighlight %}

![plot of chunk unnamed-chunk-60](/assets/images/Vis_ggplot2_Geom/unnamed-chunk-60-1.png)

## smooth line

{% highlight r %}
e + geom_smooth(method = lm)
{% endhighlight %}

![plot of chunk unnamed-chunk-61](/assets/images/Vis_ggplot2_Geom/unnamed-chunk-61-1.png)

## text plot

{% highlight r %}
e + geom_text(aes(label = cty))
{% endhighlight %}

![plot of chunk unnamed-chunk-62](/assets/images/Vis_ggplot2_Geom/unnamed-chunk-62-1.png)

## 2d histogram

{% highlight r %}
head(diamonds)
{% endhighlight %}



{% highlight text %}
## # A tibble: 6 x 10
##   carat cut       color clarity depth table price     x     y     z
##   <dbl> <ord>     <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>
## 1 0.23  Ideal     E     SI2      61.5    55   326  3.95  3.98  2.43
## 2 0.21  Premium   E     SI1      59.8    61   326  3.89  3.84  2.31
## 3 0.23  Good      E     VS1      56.9    65   327  4.05  4.07  2.31
## 4 0.290 Premium   I     VS2      62.4    58   334  4.2   4.23  2.63
## 5 0.31  Good      J     SI2      63.3    58   335  4.34  4.35  2.75
## 6 0.24  Very Good J     VVS2     62.8    57   336  3.94  3.96  2.48
{% endhighlight %}



{% highlight r %}
h <- ggplot(diamonds, aes(carat, price))
h + geom_bin2d(binwidth = c(0.25, 500))
{% endhighlight %}

![plot of chunk unnamed-chunk-63](/assets/images/Vis_ggplot2_Geom/unnamed-chunk-63-1.png)

## 2d density 

{% highlight r %}
h + geom_density2d()
{% endhighlight %}

![plot of chunk unnamed-chunk-64](/assets/images/Vis_ggplot2_Geom/unnamed-chunk-64-1.png)

## 2d hexagon

{% highlight r %}
h + geom_hex()
{% endhighlight %}

![plot of chunk unnamed-chunk-65](/assets/images/Vis_ggplot2_Geom/unnamed-chunk-65-1.png)

## Area plot

{% highlight r %}
i <- ggplot(economics, aes(date, unemploy))
i + geom_area()
{% endhighlight %}

![plot of chunk unnamed-chunk-66](/assets/images/Vis_ggplot2_Geom/unnamed-chunk-66-1.png)

## Line plot

{% highlight r %}
i + geom_line()
{% endhighlight %}

![plot of chunk unnamed-chunk-67](/assets/images/Vis_ggplot2_Geom/unnamed-chunk-67-1.png)

## Step plot

{% highlight r %}
i + geom_step(direction = "hv")
{% endhighlight %}

![plot of chunk unnamed-chunk-68](/assets/images/Vis_ggplot2_Geom/unnamed-chunk-68-1.png)

# 2범주+연속

## 막대 그래프
아래와 같이 그래프의 default 는 sum 을 출력하고 있는 모습이다. <br>

{% highlight r %}
f <- ggplot(mpg, aes(class, hwy))
f + geom_col()
{% endhighlight %}

![plot of chunk unnamed-chunk-69](/assets/images/Vis_ggplot2_Geom/unnamed-chunk-69-1.png)

{% highlight r %}
tapply(mpg$hwy,mpg$class,sum)
{% endhighlight %}



{% highlight text %}
##    2seater    compact    midsize    minivan     pickup subcompact        suv 
##        124       1330       1119        246        557        985       1124
{% endhighlight %}

## box plot

{% highlight r %}
f + geom_boxplot()
{% endhighlight %}

![plot of chunk unnamed-chunk-70](/assets/images/Vis_ggplot2_Geom/unnamed-chunk-70-1.png)

## scatter

{% highlight r %}
f + geom_dotplot(binaxis = "y", stackdir ="center",dotsize=0.3)
{% endhighlight %}

![plot of chunk unnamed-chunk-71](/assets/images/Vis_ggplot2_Geom/unnamed-chunk-71-1.png)

## violin

{% highlight r %}
f + geom_violin(scale = "area")
{% endhighlight %}

![plot of chunk unnamed-chunk-72](/assets/images/Vis_ggplot2_Geom/unnamed-chunk-72-1.png)

# 2범주+범주
## 격자 plot

{% highlight r %}
g <- ggplot(diamonds, aes(cut, color))
g + geom_count()
{% endhighlight %}

![plot of chunk unnamed-chunk-73](/assets/images/Vis_ggplot2_Geom/unnamed-chunk-73-1.png)

# 3변수

## contour plot

{% highlight r %}
head(seals)
{% endhighlight %}



{% highlight text %}
## # A tibble: 6 x 5
##     lat  long delta_long delta_lat     z
##   <dbl> <dbl>      <dbl>     <dbl> <dbl>
## 1  29.7 -173.     -0.915    0.143  0.926
## 2  30.7 -173.     -0.867    0.128  0.876
## 3  31.7 -173.     -0.819    0.113  0.827
## 4  32.7 -173.     -0.771    0.0980 0.777
## 5  33.7 -173.     -0.723    0.0828 0.727
## 6  34.7 -173.     -0.674    0.0675 0.678
{% endhighlight %}



{% highlight r %}
seals$z <- with(seals, sqrt(delta_long^2 + delta_lat^2))
l <- ggplot(seals, aes(long, lat))
l + geom_contour(aes(z = z))
{% endhighlight %}

![plot of chunk unnamed-chunk-74](/assets/images/Vis_ggplot2_Geom/unnamed-chunk-74-1.png)

## raster plot
z 를 높이로 가지는 tile plot

{% highlight r %}
l + geom_raster(aes(fill = z), hjust=0.5, vjust=0.5,
interpolate=FALSE)
{% endhighlight %}

![plot of chunk unnamed-chunk-75](/assets/images/Vis_ggplot2_Geom/unnamed-chunk-75-1.png)

## tile plot

{% highlight r %}
l + geom_tile(aes(fill = z))
{% endhighlight %}

![plot of chunk unnamed-chunk-76](/assets/images/Vis_ggplot2_Geom/unnamed-chunk-76-1.png)

