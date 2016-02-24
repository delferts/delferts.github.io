---
title: "Word cloud attēlu veidošana"
layout: post
categories: jekyll update
date: 2012-06-25 12:00:00 +0200
---




Lai programmā R varētu uzzīmēt word cloud grafiku, pirmkārt, ir nepieciešams pievienot darba sesijai divas paketes: `wordcloud` un `RColorBrewer`. Pirmā ļauj veidot pašu grafiku, bet pārējās ir nepieciešamas, lai nodefinētu atbilstošās krāsas.

{% highlight r %}
library(wordcloud)
library(RColorBrewer)
{% endhighlight %}

Grafika veidošanai ir nepieciešami datu tabula, kur vienā kolonnā ir attēlojamie vārdi, bet otrā kolonnā ir šo vārdu atkārtošanās skaits jeb frekvence. Protams, ka datu tabulas vietā var izmantot arī divus vektorus ar atbilstošajiem datiem. Šim piemēram izmantoti dati par novadu nosaukumiem un putnu sugu skaitu, kas ir novēroti šajā novadā (informācija sagatavota no [Dabasdati.lv](http://www.dabasdati.lv)).


{% highlight r %}
tabula <- structure(list(Novads = structure(c(1L, 2L, 3L, 4L, 5L,
6L, 7L, 8L, 9L, 10L, 11L, 12L, 13L, 14L, 15L, 16L, 17L, 18L, 19L, 20L, 21L,
22L, 23L, 24L, 25L, 27L, 28L, 29L, 30L, 31L, 32L, 33L, 34L, 35L, 36L, 37L,
38L, 39L, 40L, 41L, 42L, 45L, 47L, 48L, 49L, 50L, 51L, 52L, 53L, 54L, 55L,
56L, 57L, 59L, 60L, 61L, 62L, 63L, 64L, 65L, 66L, 67L, 68L, 69L, 70L, 71L,
72L, 73L, 74L, 75L, 76L, 77L, 78L, 79L, 80L, 82L, 83L, 85L, 86L, 87L, 88L,
89L, 90L, 91L, 92L, 93L, 94L, 95L, 96L, 97L, 98L, 99L, 100L, 101L, 102L,
103L, 104L, 105L, 106L, 107L, 109L, 110L, 111L, 112L, 113L, 115L, 116L,
117L, 118L, 58L, 84L, 44L, 46L, 108L, 114L, 81L, 43L, 26L), .Label = c("Adazu",
"Aglonas", "Aizkraukles", "Aizputes", "Aknistes", "Alojas", "Alsungas",
"Aluksnes", "Amatas", "Apes", "Auces", "Babites", "Baldones", "Baltinavas",
"Balvu", "Bauskas", "Beverinas", "Brocenu", "Burtnieku", "Carnikavas", "Cesu",
"Cesvaines", "Ciblas", "Dagdas", "Daugavpils", "Daugavpils_p", "Dobeles",
"Dundagas", "Durbes", "Engures", "Erglu", "Garkalnes", "Grobinas", "Gulbenes",
"Iecavas", "Ikskiles", "Ilukstes", "Incukalna", "Jaunjelgavas", "Jaunpiebalgas",
"Jaunpils", "Jekabpils", "Jekabpils_p", "Jelgava", "Jelgavas", "Jurmala",
"Kandavas", "Karsavas", "Keguma", "Kekavas", "Kocenu", "Kokneses", "Kraslavas",
"Krimuldas", "Krustpils", "Kuldigas", "Lielvardes", "Liepaja", "Ligatnes",
"Limbazu", "Livanu", "Lubanas", "Ludzas", "Madonas", "Malpils", "Marupes",
"Mazsalacas", "Nauksenu", "Neretas", "Nicas", "Ogres", "Olaines", "Ozolnieku",
"Pargaujas", "Pavilostas", "Plavinu", "Preilu", "Priekules", "Priekulu",
"Raunas", "Rezekne", "Rezeknes", "Riebinu", "Riga", "Rojas_Mersraga", "Ropazu",
"Rucavas", "Rugaju", "Rujienas", "Rundales", "Salacgrivas", "Salas", "Salaspils",
"Saldus", "Saulkrastu", "Sejas", "Siguldas", "Skriveru", "Skrundas", "Smiltenes",
"Stopinu", "Strencu", "Talsu", "Tervetes", "Tukuma", "Vainodes", "Valkas",
"Valmiera", "Varaklanu", "Varkavas", "Vecpiebalgas", "Vecumnieku", "Ventspils",
"Ventspils_p", "Viesites", "Vilakas", "Vilanu", "Zilupes"), class = "factor"),
Skaits = c(74L, 4L, 10L, 19L, 3L, 15L, 7L, 78L, 49L, 19L, 35L, 49L, 22L,
0L, 6L, 153L, 38L, 23L, 117L, 40L, 25L, 12L, 0L, 22L, 85L, 61L, 113L,
32L, 188L, 3L, 43L, 104L, 51L, 41L, 66L, 39L, 63L, 7L, 2L, 7L, 43L,
153L, 22L, 3L, 27L, 55L, 46L, 9L, 32L, 52L, 13L, 67L, 52L, 25L, 47L,
7L, 3L, 16L, 135L, 42L, 51L, 14L, 19L, 29L, 72L, 114L, 50L, 37L, 55L,
45L, 30L, 13L, 25L, 77L, 24L, 120L, 4L, 122L, 107L, 96L, 10L, 15L, 46L,
101L, 12L, 110L, 120L, 50L, 12L, 64L, 1L, 32L, 148L, 38L, 94L, 71L,
43L, 141L, 8L, 128L, 7L, 8L, 43L, 68L, 91L, 27L, 94L, 33L, 8L, 185L,
151L, 119L, 99L, 64L, 25L, 20L, 18L, 10L)), .Names = c("Novads", "Skaits"),
class = "data.frame", row.names = c(NA, -118L))

head(tabula)
{% endhighlight %}



{% highlight text %}
##        Novads Skaits
## 1       Adazu     74
## 2     Aglonas      4
## 3 Aizkraukles     10
## 4    Aizputes     19
## 5    Aknistes      3
## 6      Alojas     15
{% endhighlight %}

Nākamais solis ir nodefinēt kādas krāsas vēlaties izmantot vārdu attēlošanai. Viens variants ir uzrakstīt krāsu nosaukumus tādā secībā, kādā vēlaties (sākot ar retāk sastopamiem vārdiem uz biežāk sastopamiem vārdiem). Otrs variants ir izmantot krāsu paletes, kas izdarāms ar funkciju `brewer.pal()`. Šajā gadījumā izmantota palete Dark2 ar astoņām krāsām.


{% highlight r %}
pal <- brewer.pal(8, "Dark2")
{% endhighlight %}

Paša grafika izveidošana notiek ar funkciju `wordcloud()`, kurai kopumā var norādīt deviņus parametrus:

* vektora vai kolonnas nosaukums, kas satur vārdus (norādāms obligāti)
* vektora vai kolonnas nosaukums, kas satur frekvences (norādāms obligāti)
* vektors, kas satur divus skaitļus, lai norādītu vārdu izmēru (pirmais skaitlis ir maksimālais izmērs, otrs skaitlis ir minimālais izmērs). Šie skaitļi norāda izmēru salīdzinot ar standarta burtu izmēru
* minimālā vārdu frekvence, kuru attēlot
* maksimālais vārdu skaits, ko attēlot
* vai attēlot vārdus nejaušā secībā
* vai krāsas izvēlēties nejauši vai arī balstoties uz vārdu frekvencēm
* proporcija vārdiem, kurus jāpagriež par 90 grādiem
* vektors, kas satur krāsu nosaukumus.

Ja kādu no parametriem nevēlas mainīt, tad to var nenorādīt.

Pirmajam grafikam norādīts, ka vārdu izmērs ir no 3 līdz 0.3 vienībām, minimālā frekvence ir 2, vārdiem secība nav jāmaina, par 90 grādiem jāpagriež ne vairāk kā 15% no vārdiem un kā krāsu palete jāizmanto izveidotais vektors pal.


{% highlight r %}
wordcloud(tabula$Novads, tabula$Skaits, scale = c(3, 0.3), min.freq = 2,
          random.order = FALSE, rot.per = 0.15, colors = pal)
{% endhighlight %}

![center](/figs/2012-06-25-wourdcloud/cloud1-1.png)


Otrajā attēlā krāsu palete nomainīta uz zilo toņu paleti ar deviņiem dažādiem toņiem, maksimālais attēlojamais vārdu skaits ir 40, kā arī par 90 grādiem jāpagriež ne vairāk kā 50% no vārdiem.


{% highlight r %}
pal <- brewer.pal(9, "Blues")
wordcloud(tabula$Novads, tabula$Skaits, scale = c(3, 0.3), max.words = 40,
            random.order = FALSE, rot.per = 0.5, colors = pal)
{% endhighlight %}

![center](/figs/2012-06-25-wourdcloud/cloud2-1.png)
