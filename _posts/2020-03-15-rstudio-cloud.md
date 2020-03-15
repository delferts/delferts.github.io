---
title: "RStudio.cloud servisa izmantošana"
layout: post
categories: apmaciba update
date: 2020-03-15 12:00:00 +0200
---

Tā kā ne vienmēr ir iespējams izmantot R un RStudio, kas instalēts uz Jūsu datora, vai arī ir nepieciešams rīks, kas ļautu strādāt ar RStudio no jebkura datora, ir izveidots RStudio mākoņpakalpojums https://rstudio.cloud. Šobrīd šis pakalpojums ir Beta stadijā, pieejams bez maksas.


Lai sākto lietot šo servisu, jādodas uz mājaslapu https://rstudio.cloud, augšējā labajā stūrī jāklikšķina uz "Sign Up".

![RStudio1](/figs/RStudio1.png){:style="float: right;margin-right: 7px;margin-top: 7px;margin-bottom: 10px;"}

Piereģistrēties lapai var trīs veidos: a) piereģistrējoties ar jaunu paroli tikai šim kontam; b) piereģistrējoties ar jau esošu Google kontu; c) piereģistrējoties ar esošu GitHub kontu.

![RStudio2](/figs/RStudio2.png){:style="float: right;margin-right: 7px;margin-top: 7px;margin-bottom: 10px;"}

Pēc veiksmīgas reģistrēšanās un pierakstīšanās lapā (Log in), atvērsies lietotāja lapa.

Uzsākot darbu, jāklikšķina kreisajā pusē uz "Your Workspace" (ja šī sadaļa jau nav aktivizēta). Darba uzsākšanai ar RStudio, jāveido jauns projekts, ar izvēlni labajā pusē "New Project".

![RStudio3](/figs/RStudio3.png){:style="float: right;margin-right: 7px;margin-top: 7px;margin-bottom: 10px;"}

Tā kā ir iespējams veidot arī vairākas projektus, tad klikšķinot loga augšējā daļā uz "Untitled Project", var izvēlēties sev vēlamo nosaukumu.

![RStudio4](/figs/RStudio4.png){:style="float: right;margin-right: 7px;margin-top: 7px;margin-bottom: 10px;"}

Līdzīgi kā lokāli instalētā RStudio programmā, arī RStudio.cloud jaunu R skripta failu var izveidot ar izvēlni File/New File/R Script.

![RStudio5](/figs/RStudio5.png){:style="float: right;margin-right: 7px;margin-top: 7px;margin-bottom: 10px;"}

Failus, piemēram, Excel faili ar datiem, kuras jāizmanto konkrētā darba sesijā, nepieciešams augšupielādēt serverī. Lai to izdarītu, labajā apakšējā RStudio daļā ir jābūt "Files" sadaļā un tad jāklikšķina uz "Upload". Atvērsies logs, kurā varēs no datora izvēlēties augšupielādējamo failu.

![RStudio6](/figs/RStudio6.png){:style="float: right;margin-right: 7px;margin-top: 7px;margin-bottom: 10px;"}

RStudio.cloud katra lietotāja profilā sākotnēji ir instalētas tikai tās R paketes, kuras iekļautas R bāzes versijā. Visas pārējās R paketes jāinstalē pašiem. To var izdarīt ar R komandu `install.packages()` vai labajā apakšējā RStudio daļā izvēloties "Packages".Tad jāklikšķina uz "Install".

![RStudio7](/figs/RStudio7.png){:style="float: right;margin-right: 7px;margin-top: 7px;margin-bottom: 10px;"}

Logā, kas atvērsies, jānorāda R paketes, kuras ir nepieciešams instalēt, to nosaukumus atdalot ar semikolu vai atstarpi.

![RStudio8](/figs/RStudio8.png){:style="float: right;margin-right: 7px;margin-top: 7px;margin-bottom: 10px;"}

R skripta failus var saglabāt ar izvlēni File/Save vai File/Save as....

![RStudio9](/figs/RStudio9.png){:style="float: right;margin-right: 7px;margin-top: 7px;margin-bottom: 10px;"}

Darba gaitā radīto failu (piemēram, R skripta failu) saglabāšanai uz sava datora, labajā apakšējā RStudio daļā ir jābūt "Files" sadaļā, jāieklikšķina pie faila, kuru nepieciešams lejupielādēt, tad jāklikšķina uz More un jāizvēlas Export. Atvērsies logs, kurā jāapstiprina lejupielādējamais fails (Download).

![RStudio10](/figs/RStudio10.png){:style="float: right;margin-right: 7px;margin-top: 7px;margin-bottom: 10px;"}

Beidzot darbu, ieteicams saglabāt visu R skripta failus (File/Save) un augšējā stūrī uzspiežot uz lietotāja vārdu, izvēlēties "Log Out".

Nākamajā reizē pieslēdzoties RStudio.cloud, jāizvēlas projekts, ar kuru vēlaties turpināt darbu.

![RStudio12](/figs/RStudio10.png){:style="float: right;margin-right: 7px;margin-top: 7px;margin-bottom: 10px;"}

Lietas, kuras vērts atcerēties:

* RStudio.cloud vēl atrodas izstrādes stadījā, tāpēc atsevišķos gadījumos mēdz būt aizkavēta darbība;
* Pēc noklusējuma katrā projekta darba direktora ir projekta sākumdirektora, attiecīgi, ja faili atrodas pamatdirektorijā, tad darba direktorija nav jāmaina.