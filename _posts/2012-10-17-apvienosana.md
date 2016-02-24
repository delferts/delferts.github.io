---
title: "Divu tabulu apvienošana"
layout: post
categories: jekyll update
date: 2012-10-17 12:00:00 +0200
---




Reizēm ir nepieciešams apvienot divas tabulas balstoties uz kolonnu, kas ir kopējā visām tabulām. 
Piemēram izveidosim divas tabulas tab1 un tab2, kur abās tabulās ir kolonna gints, bet atšķiras otrā kolonna. Turklāt tikai viena no ģints vērtībām atkārtojas abās tabulās.


{% highlight r %}
tab1 <- data.frame(gints = c("Pinus", "Picea", "Alnus"), 
                   skaits = c(5, 8, 3))
tab2 <- data.frame(gints = c("Picea", "Ulmus", "Quercus"), 
                   diametrs = c(25, 34, 67))
tab1
{% endhighlight %}



{% highlight text %}
##   gints skaits
## 1 Pinus      5
## 2 Picea      8
## 3 Alnus      3
{% endhighlight %}



{% highlight r %}
tab2
{% endhighlight %}



{% highlight text %}
##     gints diametrs
## 1   Picea       25
## 2   Ulmus       34
## 3 Quercus       67
{% endhighlight %}

Viena no funkcijām, kuru var izmantot tabulu apvienošanai, ir funkcija `merge()`, kurai kā argumenti obligāti jānorāda tabulas, kuras vēlas apvienot. Ja kolonna pēc kuras vēlas veikt apvienošanu ir ar vienādu nosaukumu abās tabulas, tad to var nenorādīt (šajā gadījumā tā ir kolonna gints). Ja kolonnu nosaukumi ir atšķirīgi, tad jālieto argumenti `by.x=` un `by.x=` ar norādītiem pirmās un otrās tabulas kolonnu nosaukumiem.

Nenorādot papildus argumentus, funkcija `merge()` izveidos jaunu tabulu, kurā būs kolonnas no abām tabulām, bet kā rindiņas parādīsies tikai tie ieraksti, kuriem būs vērtības abās tabulās.


{% highlight r %}
tab3 <- merge(tab1, tab2)
tab3
{% endhighlight %}



{% highlight text %}
##   gints skaits diametrs
## 1 Picea      8       25
{% endhighlight %}

Kā papildus argumentu norādot `all=TRUE`, jaunajā tabulā parādīsies visas vērtības (rindiņas) no abām tabulām, tikai neesošo vērtību vietās parādīsies NA.


{% highlight r %}
tab4 <- merge(tab1, tab2, all = TRUE)
tab4
{% endhighlight %}



{% highlight text %}
##     gints skaits diametrs
## 1   Alnus      3       NA
## 2   Picea      8       25
## 3   Pinus      5       NA
## 4 Quercus     NA       67
## 5   Ulmus     NA       34
{% endhighlight %}

Papildus arguments `all.x=TRUE` nodrošinās to, ka jaunājā tabulā būs tikai tās vērtības (rindiņas), kas bija pirmajā tabulā, bet no otrās tabulas tiks pievienotas atbilstošo kolonnu vērtības pirmās tabulas rindiņām.


{% highlight r %}
tab5 <- merge(tab1, tab2, all.x = TRUE)
tab5
{% endhighlight %}



{% highlight text %}
##   gints skaits diametrs
## 1 Alnus      3       NA
## 2 Picea      8       25
## 3 Pinus      5       NA
{% endhighlight %}

Ar argumentu `all.y=TRUE` panāk pretēju efektu iepriekšējam piemēram.


{% highlight r %}
tab6 <- merge(tab1, tab2, all.y = TRUE)
tab6
{% endhighlight %}



{% highlight text %}
##     gints skaits diametrs
## 1   Picea      8       25
## 2 Quercus     NA       67
## 3   Ulmus     NA       34
{% endhighlight %}
