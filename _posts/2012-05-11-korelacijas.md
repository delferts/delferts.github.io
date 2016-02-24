---
title: "Korelācijas koeficientu matrice ar p-vērtībām"
layout: post
categories: jekyll update
date: 2012-05-11 12:00:00 +0200
---



Analizējot datus ļoti bieži ir situācija, kad nepieciešams aprēķināt korelācijas koeficientus starp vairākām datu kolonnām savos datos. Visvieglāk to programmā R ir izdarīt ar funkciju `cor()`, kurā liek visas vajadzīgās kolonnas vai datu masīvu.


{% highlight r %}
data(iris)
cor(iris[,1:4])
{% endhighlight %}



{% highlight text %}
##              Sepal.Length Sepal.Width Petal.Length Petal.Width
## Sepal.Length    1.0000000  -0.1175698    0.8717538   0.8179411
## Sepal.Width    -0.1175698   1.0000000   -0.4284401  -0.3661259
## Petal.Length    0.8717538  -0.4284401    1.0000000   0.9628654
## Petal.Width     0.8179411  -0.3661259    0.9628654   1.0000000
{% endhighlight %}

Problēma ar funkciju `cor()` ir tāda, ka tā aprēķina tikai korelācijas koeficientus, bet nenorāda būtiskumu. Ja ir vēlme noskaidrot būtiskumu, tad jāskatās speciālajās tabulās, vai arī jāizmanto funkcija `cor.test()`, kurā vienlaicīgi var salīdzināt tikai divus mainīgos.

Risinājums šai problēmai ir meklējams paketē `ltm`, kas satur funkciju `rcor.test()`. Šī funkcija ne tikai aprēķina korelācijas koeficientus starp vairākām kolonnām datu masīvā (matricas augšējā daļa), bet vienlaicīgi arī parāda atbilstošās p-vērtības (matricas apakšējā daļa), kas uzreiz ļauj novērtēt korelācijas koeficientu būtiskumu.


{% highlight r %}
library(ltm)
rcor.test(iris[,1:4])
{% endhighlight %}



{% highlight text %}
## 
##              Sepal.Length Sepal.Width Petal.Length Petal.Width
## Sepal.Length  *****       -0.118       0.872        0.818     
## Sepal.Width   0.152        *****      -0.428       -0.366     
## Petal.Length <0.001       <0.001       *****        0.963     
## Petal.Width  <0.001       <0.001      <0.001        *****     
## 
## upper diagonal part contains correlation coefficient estimates 
## lower diagonal part contains corresponding p-values
{% endhighlight %}
