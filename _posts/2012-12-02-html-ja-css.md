---
layout : blog
title : HTML ja CSS dummy
tags : [basics, html, css]
description : basics of html and css
comments : true
lang : estonian
excerpt : Brauser loeb ainult htmli, javascripti ja cssi. Ainult ja ainult - kõik programmeerimiskeelte poolt kirjutatav kola tõlgitakse ekraanil esitamiseks htmli ning javascript on ainus scriptimiskeel mis on brausereisse sisse ehitatud ja seda pole vaja tõlkida. Seepärast on hea ka programmeerijana sellest poolest veidi aimu omada.
---

#### HTML: Hypertext Markup Language

Pmst on see lihtsalt tekst, millele on lisatud tagid e. selektorid. Tagid on need nurksulgudega eraldatatud kokuleppelised lühendid, mille abil saab tekstiosadele anda eri funktsioone või tuua tekstiosasid välja kujundamise tarbeks css-is. Tag algab `< foo >` ja lõpeb `</ foo >`. Tagile saab panna külge selektoreid klassi või id kujul. id on kiirem, sest nagu nimigi ütleb, on see unikaalne: id-d saab ühe lehekülje ulatuses kasutada ühe korra. Class on selektor, mida saab mitmele tagile külge panna, brauser loeb seda aeglasemalt, sest peab kogu dokumendi läbi otsima. Süntaks on vastavalt `id="foo"` ja `class="foo"`. Hea tava ütleb, et funktsionaalselt erinevad lehe osad tuleb lahus hoida: nii ei segata omavahel javascripti, htmli cssi vaid lingitakse javascript ja css välise dokumendina htmli külge. Htmlis on vaid tekst, vormid, lingid ja selektorid väliste dokumentide jaoks.

HTML koosneb päisest `head` ja põhiosast `body`.   
Päist ei kuvata ekraanile, see sisaldab brauserile tarvilikku informatsiooni: 
	- encoding e. millise valemiga tähti kirjutatakse  
	- DOCTYPE e. millisele standardile antud html vastab  
	- lingid dokumendis kasutatavatele lisadele nagu css ja javascript  
	- metaandmed e. kuidas otsimootorid enda jaoks teksti loevad  
	- mõnikord ka kustom javascript, aga see on soovitatav panna dokumendi   lõppu, et laadimisaeg oleks kiirem  

Põhiosa oli ennevanasti tabel, mille ruute sai erineva sisuga täita. Nagu Ecxeli tabel. Siis leiti, et tabel on puine ja ka aeglane brausereile lugeda ja mõeldi välja selline selektor nagu `div`. Et ta on pärit tabelist, on ka div olemuselt kast. Vbl on see segadust tekitav, sest kui vaadata raw htmli, ei koosne see üldse kastidest, vaid näeb välja nagu formaatimata Wordi dokument. Põhjus selles, et raw htmli div on kast küll, aga et kastile pole antud mõõte, on kastide suurused null, samuti ka nende omavaheline paigutus. Selleks, et leht kuju saaks on css. Inline css-st ma ei räägi, sest see on halb toon.  
Tavalisematest html tagidest annab ülevaate [W3school](http://www.w3schools.com/)  
Htmli kontrollitakse [W3C Markup Validation Service](http://validator.w3.org/) abil. Vigane html tekitab brauseriaknas ootamatuid tagajärgi ja mõjub halvasti otsimootorite rankingule.

HTML5 on eraldi teema, aga asja lühike mõte on et puhas kastisüsteem, mis pärineb tabelist, tundub aja jooksul mõttetu olevat, html5 lähtub loogilisest lehe reaalsest ülesehitusest ja on sisse toonud lehe osadele vastavad tagid nagu aside jmt. See, et html5 võimaldab animatsioone teha, on teine teema.

#### CSS

CSS on õige lihtne stiilide loetelu, kujul   
	`selektor: { stiili definitsioon: stiil; }`  
selektor võib olla tag ise, nt `<p>, <span>` või selektorile antud nimetus - klass või id. Klassi märgitakse `.foo`, id-d `#foo`
Tavalisemast css süntakstist annab ülevaate samuti [W3school](http://www.w3schools.com/). Oma selektoritevalikut saab laeindada, õppides tundma [XPathi](http://www.w3.org/TR/xpath/) 
CSS3 laiendab kujunduse piire määratult, siin on probleemiks et vanemad brauserid ei toeta seda, samuti on probleeme Internet Exploreriga (see on üks väga paha brauser üldse. Kasuta Chrome või Firefoxi)  





