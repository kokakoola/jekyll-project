---
layout : blog
title : XML ja Xpath mysqli jaoks
category : basics
tags : [xml, mysql, xpath, erik]
description : xml mysql
comments : true
lang : estonian
excerpt : Wordpressile pead oma custom PHP koodi juurde pookima. City24 feed on XML; see tuleb parsida ja seejärel parsimistulemused ehk andmed andmebaasi salvestada ning seejärel kuvada 
---

1) küsid üle HTTP feedi andmed ühe suure stringina  
2) söödad stringi ette PHP või Pythoni built-in XML parserile   
3) parser annab sulle vastu mingid geneerilised (st ilma tüübita) objektid    
4) need objektid käid läbi, võtad andmed välja ja salvestad eelnevalt loodud SQL tabelisse  
ja siis kui pead andmeid kuvama, siis küsid sellest SQL tabelist andmeid ja kuvad (koos pagingu jms-ga)  

XML on universaalkeel  
XML'i peale ehitatakse mingeid spetsiifilisi keeli, näiteks RSS ja XHTML ja Atom ja kõik need City24 feedid ja asjad, kuigi sellise sita kohta on inetu öelda "keel". sa võid võtta seda nii, et kui HTML'is oleks võimalik kasutada mistahes nimedega tag'e ja attribuute, siis ongi XML  
et näiteks mitte aint \<table> ja \<font> ja \<body> ja \<strong>\</strong> jne, vaid ka näiteks \<person> ja \<name> ja \<apartment> ja \<broker> jne ja mitte aint id="" ja name="" ja style="", vaid misiganes atribuudid  \>
see on schema lihtsalt  
sama spetsifikatsiooniga saab eri schema teha, vastavalt soovile/maitsele/arukusastmele  
ja eri spekkidega on ka eri schemad  
või siis võid teha universaalsema schema, mis töötab erinevate spekkidega
sama nagu SQL tabeli schema  
aint et XML schema'd on hierarhilised mitte flat nagu SQL  

> ja html-is kutsun ma xmli andmed välja? 
ja siis selle toore XML' i sa annad XML parserile ette ja tema tagastab sulle mingi hunniku objekte, kust sa saad andmed välja võtta  

et XML feed on sul olemas, Apache, PHP ja MySQL ka olemas enda arvutis
miski ei keela sul võtta ning hakata katsetama seda feed'i sisselugeda ja parsida PHP'ga  
ilma üldse Wordpressi pärast alguses muretsemata  
seejärel ei takista sind miski nuputamast välja sobivad MySQL tabelid, kuhu andmed panna  
jällegi, ilma Wordpress'ita  
lõpuks kui asi ilma Wordpressita töötab, uurid, kuidas custom PHP koodi Wordpressi lehe sisse panna.  

tulemus on see, et sul on City24 andmed mälus (mingis muutujas)   struktureeritud kujul, mida on edasi võimalik andmebaasi INSERT'ida  
mingit HTML väljundit ei ole vahepeal  
PHPl on erinevaid XML parsereid; see, mida see tutorial (event-based) näitab, on mõttetu sinu probleemi lahendamiseks  
sellele tuleb anda ette mingid callback funktsioonid, mida parser teatud hetkedel ise välja kutsub  
a-la kui tuleb uus tag, kutsub startTag, kui tag lõppeb, kutsub endTag<br />
sedasi ei saa suurt midagi teha  
normaalne oleks xpath'il põhinev parser, kus sa saad kasutada selector'eid nagu CSS'is ja "tirida" XML puust välja endale sobivad elemendid, ning nende alamelemendid, jne  
ja siis väljatiritud elemendid (mis antakse sulle list'ina), käid läbi ning koostad vastava INSERT SQL lause ning "saadad" lause andmebaasi.  

http://www.w3schools.com/php/php_xml_dom.asp  
DOM-tüüpi parserit on sul vaja  
sorri et ma enne ei öeld  
ei taibanud  
DOM-tüüpi parseriga laetakse kogu XML dokument sisse (DOM=Document Object Model)  
ja siis on ta juba esmaselt parsitud kujul  
edasi saad sa hakata seda element-haaval läbi käima.  

> tänan. ma olen praegu siin http://tuxradar.com/practicalphp/12/3/3 

SimpleXML  
mm, okei, SimpleXML ongi just see jah  
xpath'ist sa loodetavasti saad enamvähem aru  
kui ei, siis guugelda xpath  

http://ejohn.org/blog/xpath-css-selectors/  

võrdlus  
mõlema eesmärk on enamvähem sama  
xpath on võimsam  

ja ürita enne parsimise osast aru saada; ära ürita kohe andmebaasi insert'ima hakata andmeid  

täpitähtede tulemus hetkel M√º√ºk jne  

	 <head>
	    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
	    ...  
 