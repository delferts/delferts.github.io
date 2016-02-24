---
title: "Par programmu R, Excel un SPSS izmantošanu studentu apmācībā"
layout: post
categories: jekyll update
date: 2013-03-25 12:00:00 +0200
---

Šodien man palūdza uzrakstīt viedokli par **R**, **Excel** un **SPSS** izmantošanu apmācībā. Nolēmu šo viedokli uztaisīt publisku, izveidojot ierakstu blogā. Šeit būs tikai īss viedoklis, kura galvenais uzdevums ir paskaidrot kāpēc vajadzētu izvēlēties **R** kā alternatīvu **Excel** un **SPSS**.

Programmām **SPSS** un **Excel** protams ir savas priekšrocības, no kurām kā galvenās no ikdienas lietotāja puses varētu minēt:

* Intuitīva darbošanās – ar izvēlnēm var nonākt pie vēlamā rezultāta;
* Iespēja veidot grafikus izmantojot gatavus šablonus;
* Plaši pieejami materiāli gan latviešu, gan citās valodās;
* Vairumam studentu ir priekšzināšanas darbā ar Excel.

### Tomēr šīm programmām ir arī savi trūkumi:

### Excel

* Nav statistikas programma – attiecīgi statistiskie testi ir pieejami kā Add-in, turklāt šeit ir pieejami tikai daļa no vienkāršākajiem testiem. Nav pieejami pat neparametriskie testi paraugkopu salīdzināšanai, kas ikdienā būtu bieži izmantojami. Lai mācītu kādus papildus testu nākas izmantot arī citas programmas. Tas ir viens no galvenajiem iemesliem, kāpēc Excel vairs netiek izmantots statistikas mācīšanai LU BF.
* Lai arī grafikus ir viegli veidot, no zinātniskā viedokļa standarta grafiki vairumā gadījumu neatbilst labai praksei tam, kā grafikam jāizskātās (trīsdimensiju grafiki, nevajadzīgi virsraksti, apzīmējumi).
* Versijas – datorklasē visos datoros būs vienota Excel versija, bet studentiem katram būs cita versija, kas reizēm apgrūtina apmācību, jo mainās izvēļņu izkārtojums, pieejamās papildus iespējas.

### SPSS

* Programmas iespējas ir atkarīgas no papildus moduļiem, kas tiek iekļauti licenzē – pamata SPSS ļauj darīt tikai niecīgu daļu no iespējamām analīzēm. Pat par nedaudz sarežģītākām analīzēm ir jāņem papildus modulis. Šīs politikas dēļ ir bijusi situāciju, ka vienā gadā nebija iespēja mācīt visas tēmas, jo konkrētā gada licenze neparedzēja šādus analīzes veidus (tāpēc arī meklēta alternatīva R veidā)
* Cena – nav iespējams nodrošināt, ka visiem studentiem ir pieejama programma SPSS, turklāt tādā pašā versijā kā datorklasē. Tādējādi studenti apgūst programmu SPSS, kura ārpus universitātes viņiem varbūt vairs nav pieejama. Universitātei arī nebūtu jāveicina nelegālo programmu izmantošana, jo tas visdrīzāk būs risinājums, kuru meklēs studenti.

Par **R**, iespējams, pilnīgi objektīvu vērtējumu vairs neesmu spējīgs sniegt, jo esmu liels šīs programmas atbalstītājs, bet tomēr mēģināšu:

### Trūkumi:

* Komandu rindas – nenoliedzami lielākais “klupšanas akmenis” gan mācoties, gan mācot programmu R ir tas, ka visas darbības notiek rakstot komandu rindas, kuras ir jāzin, vai arī jāmāk tās atrast. Turklāt, komandu rindu rakstīšana nozīmē, ka nedrīkst būt kļūdas pierakstos, pretējā gadījumā darbība netiek izpildīta. Tomēr mācību procesā ir iespējams vienkāršot šo komandu rindu rakstīšanu līdz minimumam – ir jāiemāca importēt failus (paris komandas), vajadzības gadījumā atlasīt datus, un pēc tam jau pamatstatistisko analīžu veikšanai ir gatavas funkcijas, kas veic visas nepieciešamas analīzes, piemēram, lineāra regresija – lm(), korelācija – cor(), vidējo aritmētisko salīdzināšana – t.test(). Pēc tam jau mācību procesa laikā var likt klāt jau sarezģītākas lietas, ko iespējams izdarīt R.
* R lietotāju skaits – šobrīd starp pasniedzējiem programma R netiek plaši izmantota, kā rezultātā studentiem ir samazināta iespēja konsultēties ar saviem darba vadītājiem par praktiskām lietām datu analīzē/apstrādē. Tāpēc vienlaicīgi ar studentu apmācību, ir jādomā arī par pasniedzēju apmācību šajos jautājumos.
* Mācību materiāli – ir piejemi plaši materiāli angļu valodā (gan grāmatas, gan bezmaksas materiāli internet), bet samērā maz ir materiālu latviešu valodā. Šo jautājumu esmu meģinājis risināt gan izveidojot R pamācības mājaslapu (http://dendro.daba.lv/R/), gan arī sākot veidot bezmaksas R grāmatu biologiem (http://dendro.daba.lv/R/gramata/)

### Priekšrocības

* Bezmaksas – programma brīvi pieejama jebkurai datorsistēmai. Var nodrošināt, ka visiem studentiem ir šī programma, turklāt visi var izmantot vienu un to pašu versiju;
* Papildinājumi – R programma šobrīd ir pieejamas vairāk nekā 4000 oficiālās papildus paketes, plus vairāki tūkstoši citu pakešu, kas nodrošina, ka ar R var veikt lielāko daļu statistisko testu gandrīz jebkurā zinātnes virzienā;
* Savas funkcijas – programmā R var veidots pats savas funkcijas, kuras vajadzības gadījumā var apvienot savās paketēs;
* Grafiku veidošana – viena no labākajām R iespējām ir veidot augstas kvalitātes grafikus, kuros var kontrolēt gandrīz visus parametrus.
* Savietojamība – ar programmu R izmantojot gan bāzes versiju, gan papildus paketes, ir iespējams importēt ļoti plašu klāstu failu (.txt, .csv, Excel, SPSS, SAS, STATA, …), importēt failus no interneta, izmantot API, veidot pieslēgumus datubāzēm (SQL).
* Atkārtojamība – ir iespējams veidot R skripta failus, saglabājot visas darītās darbības un nodrošināt, ka arī citi var atkārtot visu, kas veikts, lai pārliecinātos par aprēķinu pareizību. Šobrīd R ir izveidotas paketes, kas nodrošina arī iespējas veidot automātisku ziņojumu veidošanu, no jauna analizējot datus.

### R papildinājumi:

* Rcmdr (Rcommander) – viena no R paketēm, kas nodrošina GUI iespējas darbā ar R, piedāvājot lietājam iespēju ar izvēlnēm importēt failus, veikt analīzes, veidot grafikus, vienlaikus arī ļaujot rakstīt komandu rindas, ja nepieciešams. Tā varētu būt laba alternatīva sākot darbu ar R un mācot pamatstatistiskos testus.
* RStudio (http://www.rstudio.com) – atsevišķa programma (IDE), kas nodrošina saskarsni ar programmu R. Joprojām visas pamatdarbības jāveic ar komandu rindām, bet ir iespēja vienotā programmā pārvaldīt visus R komandu skriptus, grafikus, veidot projektus, veidot sasaisti ar tādām vietnēm kā github automātiskai sinhronizācijai.
