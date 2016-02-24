---
title: "Statistisko modeļu rezultātu pārvēršana par datu tabulām ar paketi broom"
layout: post
categories: jekyll update
date: 2016-02-24 12:00:00 +0200
---



## Problēma

Veicot statistiskās analīzes programmā R, piemēram, lineāro regresiju vai T testu, mēs iegūstam ļoti saprotamu rezultātu, kas parāda mūs interesējošās lietas. 

Šeit ir piemērs regresijas analīzei izmantojot `iris` datu objektu starp mainīgajiem `Petal.Width` un `Sepal.Width`. Analīzes rezultātos mēs redzam gan aprēķinātos koeficientus, gan arī to būtiskumu.

{% highlight r %}
data(iris)
mod<-lm(Petal.Width ~ Sepal.Width, data = iris)
summary(mod)
{% endhighlight %}



{% highlight text %}
## 
## Call:
## lm(formula = Petal.Width ~ Sepal.Width, data = iris)
## 
## Residuals:
##      Min       1Q   Median       3Q      Max 
## -1.38424 -0.60889 -0.03208  0.52691  1.64812 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept)   3.1569     0.4131   7.642 2.47e-12 ***
## Sepal.Width  -0.6403     0.1338  -4.786 4.07e-06 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 0.7117 on 148 degrees of freedom
## Multiple R-squared:  0.134,	Adjusted R-squared:  0.1282 
## F-statistic: 22.91 on 1 and 148 DF,  p-value: 4.073e-06
{% endhighlight %}

Problēmas rodas tajā brīdī, kad mums šos rezultātus vajag dabūt kā datu tabulu, lai eksportētu vai arī izmantotu kādās citās analīzes/attēlu veidošanā. Vairumā gadījumu statistisko testu rezultāti ir saglabāti kā saraksti (list) ar ļoti daudz apakšelementiem, kas apgrūtina rezultātu tālāku izmantošanu.

## Risinājums
### broom pakete
Ar šo problēmu veiksmīgi var tikt galā izmantojot paketi `broom`, kuras trīs galvenās funkcijas ir `tidy()`, `augment()` un `glance()`.

### tidy()
Funkcija `tidy()` ir paredzēta, lai kā datu tabulu izveidotu koeficientus un to būtiskumu, ko iegūstam, piemēram, lineārā regresijas rezultātā. Tagad katrs koeficients ir savā rindā (kolonna `term`), kā arī ir kolonnas ar pašiem koeficientiem, standartkļūdām un p vērtībām. Turklāt kolonnu nosaukumi nesatur dīvainus apzīmējumus vai atstarpes.


{% highlight r %}
library(broom)
tidy(lm(Petal.Width ~ Sepal.Width, data = iris))
{% endhighlight %}



{% highlight text %}
##          term   estimate std.error statistic      p.value
## 1 (Intercept)  3.1568723 0.4130820  7.642242 2.474053e-12
## 2 Sepal.Width -0.6402766 0.1337683 -4.786461 4.073229e-06
{% endhighlight %}

Līdzīgi mēs varam darīt arī ar T testa rezultātiem.


{% highlight r %}
tidy(t.test(Sepal.Width~Species,data=subset(iris,Species!="setosa")))
{% endhighlight %}



{% highlight text %}
##   estimate estimate1 estimate2 statistic     p.value parameter   conf.low
## 1   -0.204      2.77     2.974 -3.205761 0.001819483  97.92683 -0.3302836
##     conf.high
## 1 -0.07771636
{% endhighlight %}

### glance()

Ja ir nepieciešams kā datu tabulu saglabāt dažādus modeļa kopējos novērtējuma radītājus, piemēram, $R^2$, p vērtību, AIC, tad ir jāizmanto funkcija `glance()`.


{% highlight r %}
glance(lm(Petal.Width ~ Sepal.Width, data = iris))
{% endhighlight %}



{% highlight text %}
##   r.squared adj.r.squared     sigma statistic      p.value df    logLik
## 1 0.1340482     0.1281972 0.7117042  22.91021 4.073229e-06  2 -160.8201
##        AIC      BIC deviance df.residual
## 1 327.6402 336.6722 74.96539         148
{% endhighlight %}

### augment()

Ar funkcijas `augment()` palīdzību ir iespējams no modeļiem izvilkt katram novērojumam aprēķināmos lielumus un tos pievienot modeļa veidošanai izmantotajiem datiem. Tas ietver prognozētās vērtības, atlikuma vērtības, kā arī diagnosticējošos rādītājus.


{% highlight r %}
head(augment(lm(Petal.Width ~ Sepal.Width, data = iris)))
{% endhighlight %}



{% highlight text %}
##   Petal.Width Sepal.Width   .fitted    .se.fit     .resid        .hat
## 1         0.2         3.5 0.9159042 0.08296509 -0.7159042 0.013589132
## 2         0.2         3.0 1.2360425 0.05861432 -1.0360425 0.006782791
## 3         0.2         3.2 1.1079872 0.06116395 -0.9079872 0.007385705
## 4         0.2         3.1 1.1720149 0.05839002 -0.9720149 0.006730978
## 5         0.2         3.6 0.8518766 0.09298579 -0.6518766 0.017070023
## 6         0.4         3.9 0.6597936 0.12681910 -0.2597936 0.031751938
##      .sigma     .cooksd .std.resid
## 1 0.7116418 0.007065726 -1.0128065
## 2 0.7089548 0.007285276 -1.4606828
## 3 0.7101538 0.006100442 -1.2805305
## 4 0.7095758 0.006362988 -1.3703765
## 5 0.7120588 0.007411235 -0.9238565
## 6 0.7137888 0.002256445 -0.3709673
{% endhighlight %}

### Saites

Lai iegūtu papildus informāciju par šo paketi un tās darbību, var apmeklēt:

* [broom paketes lapa CRAN serverī](https://cran.r-project.org/web/packages/broom/index.html)
* [Paketes autora David Robinson bloga raksts](http://varianceexplained.org/r/broom-intro/)
* [Ievadpamācība darbā ar paketi broom](https://cran.r-project.org/web/packages/broom/vignettes/broom.html)
