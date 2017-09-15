---
title: "Regresijas vienādojuma pievienošana ggplot2 attēliem"
layout: post
categories: blog update
date: 2017-09-15 12:00:00 +0200
---



Veidojot attēlos, kuros parādīta saistība starp diviem mainīgajiem un regresijas līkne, reizēm ir nepieciešams attēlam pievienot arī pašu regresijas vienādojumu, vai arī kādus citus parametrus, piemēram, determinācijas koeficientu vai AIC vērtību. 

Tie, kas veidojuši attēlus Excel, atcerēsies cik viegli tas bija - labais peles taustiņš uz regresijas līknes un tad tikai jāieliek atzīme pie tā, vai gribat redzēt arī vienādojumu un determinācijas koeficientu.

Programmā R veidojot attēlus ar `ggplot2` paketi, šādas iespējas kaut ko ieklikšķināt nav. Viens variants pašam manuāli pievienot šīs lietas ar `geom_text()`, pirms tam aprēķinot vajadzīgos koeficientus. Otra iespēja ir izmantot paketi `ggpmisc`, kurā ir ieviestas papildus funkcijas vienādojumu un papildus rādītāju pievienošanai.

Izmantojot funkciju `stat_poly_eq()`, pēc noklusējuma parādās determinācijas koeficients. Obligātie argumenti funkcijai ir formula (izmantojot apzīmējumus x un y), kā arī arguments `parse = TRUE`. Visus koeficientus aprēķina pati funkcija un tad izmantot apzīmējumu veidošanai.


{% highlight r %}
library(ggplot2)
library(ggpmisc)

ggplot(iris,aes(Petal.Width,Petal.Length)) +
  geom_point() +
  geom_smooth(method = "lm") +
  stat_poly_eq(formula = y ~ x, parse = TRUE)
{% endhighlight %}

![center](/figs/2017-09-15-regresija/unnamed-chunk-11-1.png)

Parasto determinācijas koeficientu var aizstāt arī ar pielāgoto determinācijas koeficientu, pievienojot argumentu `label = ..adj.rr.label..`.


{% highlight r %}
ggplot(iris,aes(Petal.Width,Petal.Length)) +
  geom_point() +
  geom_smooth(method = "lm") +
  stat_poly_eq(formula = y ~ x, parse = TRUE, 
               aes(label = ..adj.rr.label..))
{% endhighlight %}

![center](/figs/2017-09-15-regresija/unnamed-chunk-12-1.png)

Tā pat var parādīt arī AIC vērtību vienādojumam.


{% highlight r %}
ggplot(iris,aes(Petal.Width,Petal.Length)) +
  geom_point() +
  geom_smooth(method = "lm") +
  stat_poly_eq(formula = y ~ x, parse = TRUE, 
               aes(label = ..AIC.label..))
{% endhighlight %}

![center](/figs/2017-09-15-regresija/unnamed-chunk-13-1.png)

Pašu regresijas vienādojumu var pievienot ar argumentu `label = ..eq.label..`.


{% highlight r %}
ggplot(iris,aes(Petal.Width,Petal.Length)) +
  geom_point() +
  geom_smooth(method = "lm") +
  stat_poly_eq(formula = y ~ x, parse = TRUE, 
               aes(label = ..eq.label..))
{% endhighlight %}

![center](/figs/2017-09-15-regresija/unnamed-chunk-14-1.png)

Vienā rindā var parādītā gan vienādojumu, gan arī determinācijas koeficientu. Šajā gadījumā pie argumenta `label = ` papildus ir jāizmanto funkcija `paste()`.


{% highlight r %}
ggplot(iris,aes(Petal.Width,Petal.Length)) +
  geom_point() +
  geom_smooth(method = "lm") +
  stat_poly_eq(formula = y ~ x, parse = TRUE,
               aes(label = paste(..eq.label.., ..rr.label..,sep = "*\",\"~~")))
{% endhighlight %}

![center](/figs/2017-09-15-regresija/unnamed-chunk-15-1.png)

Funkcijas `stat_poly_eq()` priekšrocība ir arī tā, ka nosakot krāsu vai aizpildījumu punktiem, līnijā, utt., regresijas vienādojumi automātiski veidojas katram no līmenim ar atbilstošajiem koeficientiem. 


{% highlight r %}
ggplot(iris,aes(Petal.Width,Petal.Length, color = Species)) +
  geom_point() +
  geom_smooth(method = "lm") +
  stat_poly_eq(formula = y ~ x, parse = TRUE,
               aes(label = paste(..eq.label.., ..rr.label..,sep = "*\",\"~~")))
{% endhighlight %}

![center](/figs/2017-09-15-regresija/unnamed-chunk-16-1.png)

Regresijas vienādojumi var būt ne tikai pirmās pakāpes, bet arī otrās, trešās, ..., galvenais jānorāda atbilstošā formula gan līknei, gan arī vienādojuma funkcijai.


{% highlight r %}
ggplot(iris,aes(Petal.Width,Petal.Length)) +
  geom_point() +
  geom_smooth(method = "lm", formula = y ~ x + I(x^2)) +
  stat_poly_eq(formula = y ~ x + I(x^2), parse = TRUE, 
               aes(label = ..eq.label..))
{% endhighlight %}

![center](/figs/2017-09-15-regresija/unnamed-chunk-17-1.png)





