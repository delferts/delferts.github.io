---
title: "Kā izveidot grafiku ar divām y asīm?"
layout: post
categories: jekyll update
date: 2012-01-31 12:00:00 +0200
---



Lai arī daļa speciālistu atzīst, ka grafiki ar divām y asīm nav labi, reizēm ir vēlme tādus izveidot.

Kā pirmais solis, protams, ir nepieciešami dati, kurus šoreiz mākslīgi radīsim:


{% highlight r %}
x<-1:10
y<-seq(15,6,-1)
y2<-seq(102,120,2)
{% endhighlight %}

Tālāk vajag nodefinēt vietu otrajai y asij un tekstam pie tās, jo automātiski labējā mala tiek veidota šaura:


{% highlight r %}
par(mar=c(5,5,2,5))
{% endhighlight %}

Tagad varam uzzīmēt datus, ko vēlamies attēlot uz pirmās y ass:


{% highlight r %}
plot(x,y,type="l",lwd=2,col="green")
{% endhighlight %}

Lai varētu pievienot datus uz otras y ass, ir jāizmanto funkcija `par()` ar argumentu `new=TRUE`, kas ļauj esošam grafikam likt virsū nākamo grafiku:


{% highlight r %}
par(new=TRUE)
{% endhighlight %}

Otro grafiku zīmējam, piemēram, ar funkciju `plot()`. Galvenais ir jāatceras, ka jāatslēdz automātiskā tekstu un asu veidošana šim grafikam, pretējā gadījumā teksti pārklāsies ar iepriekšējo grafiku:


{% highlight r %}
plot(x,y2,type="l",lwd=2,col="red",axes=FALSE,ann=FALSE)
{% endhighlight %}

Tagad varam arī nedefinēt kādu tieši vēlamies redzēt otro y asi, kā arī pielikt pie tās apzīmējumu. Papildus pieliekam arī leģendu:


{% highlight r %}
axis(4,at=seq(100,120,5))
mtext("y2",side=4,line=3)
legend(5,120,c("y","y2"),col=c("green","red"),lwd=2)
{% endhighlight %}

![center](/figs/2012-01-31-divas-asis/divasis-1.png)
