---
title: "Manis sniegto atbilžu lapā https://stackoverflow.com analīze"
layout: post
categories: blog update
date: 2016-11-01 12:00:00 +0200
---



Jau gandrīz četrus gadus esmu reģistrējies jautājumu/atbilžu portālā [https://stackoverflow.com](https://stackoverflow.com) un uz šo brīdi esmu sniedzis 699 atbildes uz jautājumiem par R programmu un uzdevis tikai vienu jautājumu.

Tagad visi jautājumi un atbildes par programmu R no StackOverflow pieejami lapā [https://www.kaggle.com/stackoverflow/rquestions](https://www.kaggle.com/stackoverflow/rquestions) kā csv faili, kas ļauj tos katram analizēt pēc savām vajadzībām. Protams, ka uzzinot par šādu iespēju, radās vēlme papētīt manis sniegtās atbildes.


## Dati

Jautājumu un atbilžu dati ir pieejami trīs failos, attiecīgi par jautājumiem, par atbildēm, par tagiem (birkām) (izņemot R tagu, kas ir kopīgs visiem jautājumiem).

Datus lejupielādējam no [https://www.kaggle.com/stackoverflow/rquestions](https://www.kaggle.com/stackoverflow/rquestions) mājaslapas un tad importējam programmā R.


{% highlight r %}
library(readr)
library(dplyr)
atbildes <- read_csv("rquestions/Answers.csv",progress = FALSE)
tags <- read_csv("rquestions/Tags.csv",progress = FALSE)
{% endhighlight %}

Tagad no atbilžu objekta atlasām tās atbildes, kuras esmu sniedzis es (to nosaka pēc kolonnas `OwnerUserId`). Rezultātā paliek pārī 684 rindiņas, kas ir mazāk nekā manis sniegtais atbilžu daudzums (iespējams, ka kādai atbildei nav pievienots R tags).


{% highlight r %}
atbildes_manas <- atbildes %>% filter(OwnerUserId=="1857266")
{% endhighlight %}

Lai atlasītu manu atbilžu tagus, tiek apvienota kopā daļa no `atbildes_manas` tabulas ar `tags` tabulu, balstoties uz jautājumu Id numuru.


{% highlight r %}
tags_mani <-atbildes_manas %>% select(ParentId,CreationDate) %>%
      left_join(.,tags,by=c("ParentId"="Id"))
{% endhighlight %}


## Atbildes

Savu sniegto atbilžu izmaiņu analīzei datu tabulai pievieno jaunas kolonnas, kas parāda gadu, mēnesi un nedēļas dienu, kurā sniegta atbide

{% highlight r %}
library(lubridate)
atbildes_manas <- atbildes_manas %>%
      mutate(Gads = year(CreationDate),
             Mēnesis = month(CreationDate),
             Nedēļa = wday(CreationDate))
{% endhighlight %}

Tagad varam skatīties, kā mainījies sniegto atbilžu daudzums pa gadiem. Skaidri redzams, ka aktīvākais gads man ir bijis 2013., pēc kā sekojis straujš aktivitātes kritums. 

{% highlight r %}
library(ggplot2)
library(cowplot)
atbildes_manas %>%
      group_by(Gads) %>%
      summarise(Skaits=n()) %>%
      ggplot(.,aes(Gads,Skaits))+geom_bar(stat="identity")
{% endhighlight %}

![center](/figs/2016-11-01-stack-atbildes/unnamed-chunk-5-1.png)

Šo tendeci var arī redzēt skatot kā kumulatīvi ir mainījies manis sniegto atbilžu skaits.


{% highlight r %}
atbildes_manas %>%
      arrange(CreationDate) %>%
      mutate(Skaits=seq_along(CreationDate)) %>%
      ggplot(.,aes(CreationDate,Skaits))+geom_step()
{% endhighlight %}

![center](/figs/2016-11-01-stack-atbildes/unnamed-chunk-6-1.png)



Ja skatāmies uz mēnešu sadalījumu, tad aktīvākie mēneši bijuši marts un aprīlis, bet vismazāk atbildes sniegtas septembrī. Zemā aktivitāte septembrī, laikam, skaidrojama ar to, ka tad parasti universitātē ir daudz darba sākoties jaunajam a.g. un neatliek laika palīdzēt citiem.


{% highlight r %}
atbildes_manas %>%
      group_by(Mēnesis) %>%
      summarise(Skaits=n()) %>%
      ggplot(.,aes(as.factor(Mēnesis),Skaits))+geom_bar(stat="identity")+
      labs(x="Mēnesis")
{% endhighlight %}

![center](/figs/2016-11-01-stack-atbildes/unnamed-chunk-7-1.png)

Vismazāk atbildes sniegtas svētdienās, kad arī jautājumi parasti ir daudz mazāk nekā citās dienās.

{% highlight r %}
atbildes_manas %>%
      group_by(Nedēļa) %>%
      summarise(Skaits=n()) %>%
      ggplot(.,aes(as.factor(Nedēļa),Skaits))+geom_bar(stat="identity")+
      labs(x="Nedēļas diena")
{% endhighlight %}

![center](/figs/2016-11-01-stack-atbildes/unnamed-chunk-8-1.png)

Sniegtās atbildes uz jautājumiem citi lietotāji novērtē balsojot ar pozitīvi vai negatīvu vērtējumu. Šobrīd nav nevien atbilde, kuras kopējais vērtējums būtu negatīvs, bet ir 38 atbildes, kuras vērtējums ir 0 jeb neviens to nav novērtējis. Tikai divām atbildēm (0.3%) vērtējums ir virs 100 punktiem, bet visvairāk atbilžu (69.4%) ir ar vērtējumu no 2 līdz 10.


{% highlight r %}
atbildes_manas %>% 
      mutate(Vertejums = cut(Score,breaks=c(-10,-1,0,1,10,25,50,100,1000))) %>%
      select(Score,Vertejums) %>%
      group_by(Vertejums) %>%
      summarise(Skaits=n()) %>%
      mutate(Procenti=round(Skaits/sum(Skaits)*100,1))
{% endhighlight %}



{% highlight text %}
## # A tibble: 7 × 3
##     Vertejums Skaits Procenti
##        <fctr>  <int>    <dbl>
## 1      (-1,0]     38      5.6
## 2       (0,1]    104     15.2
## 3      (1,10]    475     69.4
## 4     (10,25]     52      7.6
## 5     (25,50]     10      1.5
## 6    (50,100]      3      0.4
## 7 (100,1e+03]      2      0.3
{% endhighlight %}


## Tagi

Kā jau vairāk kārt esmu rakstījis, tad mana mīļākā tēma, par kuru sniegt atbildes, ir ggplot2 attēli. To ļoti labi var redzēt pēc 10 populārākajiem tagiem, kur dominē ggplot2 un ir vēl septiņi tagi, kas saistāmi ar attēliem.


{% highlight r %}
tags_mani %>% group_by(Tag) %>%
      filter(!is.na(Tag)) %>%
      summarise(Skaits=n()) %>%
      arrange(desc(Skaits)) %>%
      top_n(10) %>%
      ggplot(.,aes(reorder(Tag,Skaits),Skaits))+geom_bar(stat="identity")+
      coord_flip()+labs(x="Tagi")
{% endhighlight %}

![center](/figs/2016-11-01-stack-atbildes/unnamed-chunk-10-1.png)


