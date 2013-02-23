---
layout : blog
title : programmeerimine per se
tags : [programmeerimine, abstaktsioon, nimetamine, erik]
description : basics of programming
comments : true
lang : estonian
excerpt : ja samuti "siiami kass" ja "pärsia kass" on mõlemad hunnik molekule, aga me mitte ainult ei nimeta mõlemaid kassiks, vaid me veel lausa klassifitseerime. see on jällegi abstraktsioon... see toimub ainult meie peas, sest looduse jaoks pole sellist asja nagu "kass" või "pärsia kass" või "siiami kassi" 
---
"tmp = passiveSlide"  tähendab  "pane muutuja 'passiveSlide' sees olev väärtus/objekt muutuja "tmp" sisse"  
muutujad on nagu panged... neil on midagi sees
kas number või slaid või tekstistring või array või funktsioon/protseduur jne
või tühjus  
blabla = 3;   // panges nimega 'blabla' on number 3  
haha = "abc";  // panges nimega 'haha' on teksti-string "abc"  
asd = "123";  // panges nimega 'asd' on teksti-string "123" (mitte number) 

iga asi on väärtus  
3 on väärtus, "abc" on väärtus, "123" on väärtus, [1, 2, 3] on väärtus (ja isegi protseduurid on väärtused)  
[1, 2, 3] on list, mille sees on OMAKORDA väärtused  

väärtuseid on eri tüüpi: arv (täisarv, murdarv), teksti-string, tõeväärtus (true/false), list, tühjus (null (mitte 0)), ja mõned veel

    var kassideArv = 1 + 2 + 3;  
    var saabasteArv = 1 + 2 + 3;  
    
mõlemal juhul on 1 + 2 + 3, aga esimesel juhul on ilmselgelt mõeldud kasside arvu, teisel juhul saabaste arvu   

aga arvuti jaoks on kõik ükstaspuha...  

selle pärast on ka oluline, et muutuja nimi selgelt ütleks, millega on tegu, et sa ise aru saaksid, mis seal sees oleva arvu tegelik tähendus on  

asjadele nime andmine ongi tegelikult inimmõtlemise alus.. selle nimi on abstraktsioon  

näiteks kass on hunnik molekule... aga meie ajus on tema nimi kass, et me ei peaks teda vaatlema kui hunnikut molekule  

ja samuti "siiami kass" ja "pärsia kass" on mõlemad hunnik molekule, aga me mitte ainult ei nimeta mõlemaid kassiks, vaid me veel lausa klassifitseerime  
see on jällegi abstraktsioon... see toimub ainult meie peas, sest looduse jaoks pole sellist asja nagu "kass" või "pärsia kass" või "siiami kassi"  

ja samamoodi arvuti jaoks on nagu looduse jaoks... tema jaoks on kõik lihtsalt mingi arv... meie ise anname sellele arvule tõlgenduse  

arvutiga on samad lood nagu looduses... arvuti ise ei tea abstraktsioonidest midagi  

igatahes arvuti sees on lõppudelõpuks on kõik asjad üldsegi nullid ja ühed...  

> tänase päevani?

see ei ole muutunud ega hakka ka kunagi muutuma  
ja kui sa imestad, miks sina nendega veel kokku pole puutunud (ega ka mina), siis asi on selles, et meil on abstraktsioon nimega Javascript  
tegelikult meil on 0 ja 1 ja Javascripti vahel veel päris pikk seeria abstraktsioone.

> kahendsüsteemist popimat pole leitud?

kahendsüsteem ongi kõige popim, alguses üritati kümnendsüsteemis ja 64ndsüsteemis. ja sa ei pea seda ka ebapopiks pidama, sest see ei ole vähearenenud vaid just kõige parem võimalik lahendus, sest ta on väga lihtne  

> kas abstrakne mõtlemine tähendab klassifitseerivat mõtlemist?  

mitte tingimata  
klassifitseerimine on konkreetne abstraktsioonitüüp  
abstraktsioon kui selline on lihtsalt mingile (üldiselt keerulisele) hulgale lihtsa nime andmist  
näiteks sa oskad korrutada, kuig korrutamine on tegelikult mitu korda liitmine
[ja sellele mitu korda liitmisele on antud nimi korrutamine... vastasel juhul oleks ilgelt raske rääkida korrutamisest  
või kui sa peaksid oma autot iga hommik kirjeldama loetledes üles kõik tema komponendid selle asemel, et öelda "auto"; oleks ka paras pain-in-the-ass  
ja kui sa tahad öelda "autopark" siis sa ei ütle "auto auto auto auto ... " vaid "autopark"  

programmeerimises muutub selline abstraktsioon aga silmaganähtavamaks  
iga kord, kui sa mingile protseduurile nime annad, tegeled sa abstraksiooniga  
sest sa ei pea enam mõtlema, mis seal protseduuri sees on, vaid sa vaatad tema nime ja saad aru, mida ta teeb  
täpsemalt: sa võid unustada detailid ja vaadata suurt pilti  
ja suurtest piltidest saab moodustada veel suurema pildi  

ja veel suuremat pilti teiste veel suuremate piltidega kombineerides saad hiigelsuure pildi  
ehk siis abstraktsioone saab üksteise peale panna  
see on ainuke võimalus, kuidas keerulisi programme lihtsateks teha

> nii tulebki välja programm?

no sa võid seda ka mitte teha, ainult et su aju lehdab õhku

> siis ei tohi ära unustada esimest nime. või - ei tohi viga teha esimeses nimes

nimesid saab alati muuta, ja seda ka PEAB tegema  
sest alguses võid sa asjale vale nime anda  
näiteks laps võib arvata, et hüään on koerlane, sest ta tundub siuke  
aga hiljem saab teada, et ups.. vale, kaslane hoopis on

> ja siis teed terve keti algusest peale uuesti  

ei pea tegema
ainult nime muudad ära kõikjal, kus teda kasutatud on  
programmi see ei muuda  
küll aga muudab seda, kuidas sa ise edaspidi programmist aru saad  
see on nagu lastele mingi keerulise asja seletamine  
alguses seletad ühtmoodi -- ei saa aru  
siis teistmoodi -- ei saa aru  
proovid hästi palju kordi eri moodi sõnastades, ja vahel isegi eri järjekorras jne  
lõpuks saavad aru  
kuigi sa rääkisid koguaeg samast asjast, lihtsalt eri sõnadega (nimedega)  

ja samamoodi kui nad kogemata jäävad uskuma valet sõnastus, võib hiljem segadus tekkida uute asjadega  
seega kui sa oma asjade nimesid korras ei hoia, võib sellest suur segadus tekkida  
ja see on programmeerijate igapäevaelu, sest enamik programmeerijaid on lohakad, laisad ja lollid ja ei anna asjadele õigeid nimesid :)  
või sama hull variant: ei anna asjadele üldse nimesid!  

ehk siis selle asemel, et protseduur kuhugi nimega ära salvestada, nad copy-paste'ivad seda igale poole ilma talle nime andmata. 

asi pole masinas vaid inimeses. nimede andmine on kasulik inimese jaoks ja see on peamine. masinal pole sooja ega külma nimedest. 

kui aus olla, siis tihti tehakse programmid seeläbi kiiremaks, et kaotatakse nimed sootuks ära  (nähtamatult ma mõtlen, kui programm jookseb.. kood jääb samaks inimese jaoks). 

> ...aga siis tuleb kõik molekulid välja kirjutada

masin kirjutabki  

see ongi programmerimise mõte :P  
panna masin enda eest molekulidega tegelema  
täpselt nagu kalkulaator teeb ühe pika arvutuse sinu eest ühe sekundiga ja sina ei pea mõtlema, KUIDAS ta seda teeb  

> "kaotatakse nimed sootuks ära"...

seda teeb arvuti nähtamatult. sina ei näe seda. see on täpselt sama,et looduses ei ole asjadel nimesid. ainult inimese jaoks on. 

programmides on alati nimed asjadel, lihtsalt sel hetkel, kui arvuti programmi sööma hakkab, võivad nimed otstarbekuse tõttu ära kaduda  
sest arvuti jaoks pole nimesid enam vaja ja nimed teevad ARVUTI jaoks asja keerulisemaks  
samas kõige KUNNIMAD programmid vastupidi kasutavad nii häid ja selgeid nimesid, et nad on tihti jutuna loetavad nagu inimkeel  

> miks on nii palju programmeerimiskeeli kui kahendsüsteeme on 1? kas õiget keelt pole leitud? kuidas tõlgitakse inimkeel tagasi nullideks ja ühtedeks?

no programmeerimiskeel on palju samal põhjusel, miks eri inimesed annavad asjadele eri nimesid ja räägivad asjdest teistmoodi  
ja miks maialmas on eri inimkeeled  
sama asja saab eri moodi öelda  
ja see, kuidas sinu inimkeele-sarnane programm muutub nullideks ja ühtedeks -- palun ära küsi seda :P ... sellest arusaamine on täiesti üleliigne ja ebavajalik  

> kas poleks lihtsam kui oleks üks keel - siis liiguksid kõik samas suunas ja kokku kiiremini?

99.9% programmeerijatest ei puutu kahendsüsteemiga kas üldse kokku või teeb seda ainult vahel harva, ja seda ainult siis, kui programm tegeleb numbrilise arvutusega.

no ideaalkeelt pole olemas.. ühe asja jaoks sobib üks, ühe jaoks teine
ja kuidas sa kaotad keeled ära? ütled, et enam ei tohi?  
ma võin kätte võtta ja omale näiteks uue programmeerimiskeele programmeerida  

