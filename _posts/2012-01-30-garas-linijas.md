---
title: "Līniju novilkšana pāri asīm"
layout: post
categories: jekyll update
date: 2012-01-30 12:00:00 +0200
---




Reizēm rodas nepieciešamība grafikā novilkt līniju, kas iziet ārpus grafika centrālajai daļai un šķērso asis, vai pat pilnībā atrodas ārpus asīm.

Sākumā jānodefinē nedaudz lielāks laukums grafikam:


{% highlight r %}
par(mar=c(5,5,5,5))
{% endhighlight %}

Pēc tam jāizveido pats grafiks, kurā šoreiz neko neattēlosim:


{% highlight r %}
plot(0:1,0:1,type="n",ann=F)
{% endhighlight %}

Lai uzzīmētu līniju, kas šķērso asis vai atrodas ārpus tām, ir jāizmanto argumentu `xpd=TRUE`. Kā piemēru izveidojam slīpu nepārtrauktu līniju starp noteiktām līnijām:


{% highlight r %}
lines(c(-0.15,0.2),c(-0.2,1),lwd=2,xpd=TRUE)
{% endhighlight %}

Līdzīgi varam izveidot punktotu līniju, kas atrodas virs grafika:


{% highlight r %}
lines(c(-0.1,1.1),c(1.1,1.1),lty=3,lwd=2,xpd=TRUE)
{% endhighlight %}

Argumentu `xpd=TRUE` var lietot arī ar funkciju `abline()`, tikai šajā gadījumā līnija šķērsos pilnībā visu grafiku:


{% highlight r %}
abline(-0.1,2,lty=2,lwd=2,xpd=TRUE)
{% endhighlight %}

![center](/figs/2012-01-30-garas-linijas/unnamed-chunk-6-1.png)

