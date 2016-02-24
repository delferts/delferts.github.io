---
title: "Kā nodrošināt visu jaunāko R pakešu instalāciju"
layout: post
categories: jekyll update
date: 2012-01-12 12:00:00 +0200
---



Ja Jūsu datorā ir instalētas visas pieejamās R paketes un ir vēlme nodrošināt, ka tiek uzinstalētas arī jaunākās paketes, var izmantot sekojošās komandu rindas.
Pirmkārt, kā vektoru jāsaglabā visu pieejamo pakešu saraksts:


{% highlight r %}
list.of.packages<-as.vector(available.packages()[,1])
{% endhighlight %}

Pēc tam izveido sarakstu ar jaunajām paketēm – salīdzina sarakstu ar instalētajām paketēm ar pieejamo pakešu sarakstu. Atšķirīgās paketes saglabā jaunajā sarakstā.


{% highlight r %}
new.packages <- list.of.packages[!(list.of.packages %in% installed.packages()[,"Package"])]
{% endhighlight %}

Beigās instalē jaunās paketes.


{% highlight r %}
install.packages(new.packages)
{% endhighlight %}
