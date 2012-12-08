---
layout : blog
title : Javascript
category : basics
tags : [ javascript, erik ]
description : javascript
comments : true
lang : estonian
excerpt : javascripti loeb veebibrauserisse installitud javascripti interpretaator e. mootor
---

	function sayGoodMorningToMare() { alert("Good morning, Mare!"); }
	function sayGoodMorningToErik() { alert("Good morning, Erik!"); }

	function sayGoodMorningTo(who) { alert("Good morning, " + who + "!"); }
	sayGoodMorningTo("Erik");
	sayGoodMorningTo("Mare");

EESKIRI e. PROTSEDUUR e. FUNKTSIOON ja TÄITMINE e. VÄLJAKUTSUMINE e. KÄIVITAMINE
sa defineerid koodis mingi sektsiooni e. protseduuri, mida sa saad suvalisel hetkel käima panna e. välja kutsuda. see, et protseduuridele saab mingeid väärtusi ette anda, on selleks, et sa saaks kasutada üht sama protseduuri natuke erinevalt iga kord

ehk siis silt/eeskiri ei pea olema teadlik sellest, MILLISES situatsioonis ja milliste konkreetse objektidega teda täitma hakatakse. küllaga peab eeskirja TÄITJA seda teadma, sest muidu ta ei saaks seda täita, mistõttu tuleb eeskirja täitmiseks käsku andes (protseduuri välja kutsudes) reaalne objekt ette anda, millega eeskirja täita tuleb .
 
näiteks preparePassiveSlide eeskiri räägib passiivse slaidi ettevalmistamisest üldiselt mingi küsimuse jaoks, aga sel hetkel (rida 72), kui seda eeskirja täitma hakatakse, räägitakse juba konkreetsest küsimusest

üks asi on koodi lugemine (seda tehakse ainult üks kord muidugi), aga teine asi on koodi käivitamine. preparePassiveSlide kood loetakse sisse ühe korra ja jäetakse meelde, aga see kood pannakse KÄIMA alles siis, kui sa kutsud preparePassiveSlide(nextQuestionNr) real 72 ja käima võib panna mitu korda
 
ja sind huvitab käimine, mitte lugemine (lugemine huvitab sind ainult siis, kui sa teed mingi näpuka ja tuleb syntax error). pärast seda on aga programm sisse loetud, rohkem süntaks erroreid enam tulla ei saa, ja siis läheb edasi juba käivitamine ja käivitamine on see, mis võib hüpata eri kohtadesse kas üles või alla. lugemine on alati ülalt alla, aga nagu ma ütlesin, lugemine ei huvita sind muul hetkel kui ainult süntaks errorite puhul

	function nextSlide() {
	   var nextQuestionNr = currentQuestionNr + 1;
	  preparePassiveSlide(nextQuestionNr);
	   moveRight();
	   currentQuestionNr = nextQuestionNr;
	}

see definitsioon tähendab järgmist inimkeeles:

	moving to the next slide means doing the following:
	   computing the next question number
	       by taking the current question number and adding 1 to it,

	   then preparing the currently hidden/passive slide
	       for displaying the next slide by using the next slide nr we just computed,

	   then moving the slides to the right

	   and finally remembering that we are now at the next question,
	       so next time we repeat the same procedure, we can treat what is currently the next question, as the current question.
^
	// definitsioon
	function NIMI() { eeskiri }
	// täitmine/kutse
	NIMI();
^
	// definitsioon
	function NIMI(parameeter) { eeskiri mis kasutab parameetrit }
	// täitmine/kutse
	NIMI(konkreetne_parameetri_väärtus);
 
// who on siin parameeter... ta on vajalik eeskirja täitmiseks, kui eeskirja täitma hakatakse

	function sayHelloTo(who) { alert("Hello, " + who); }

// siin on "Peeter" väärtus, mis antakse sayHello nimelisele eeskirjale edasi selleks, et ta saaks sellega midagi edasi teha
sayHello("Peeter");
3:50 PM
 
	function sayHelloTo(who) {

tähendab inimkeeli:

meil on mingi eeskiri "sayHelloTo", mida välja kutsudes tuleb ette anda mingi inimese nimi, ja selle inimese nimi on selle eeskirja sees muutujas "who"

eeskiri sokkide puhastamiseks:

	nimi: puhasta
	   eeldus MINGI SOKK

	   pane SEE SOKK vette
	   lisa seepi
	   hõõru SOKKI seebiga
	   pressi SOKK veest tühjaks
^
	puhasta minu sokk
	puhasta sinu sokk
	puhasta ema sokk
	puhasta villae sokk
^
	function puhasta(sokk) {
	   paneVette(sokk);
	   lisaSeep();
	   hõõruSeebiga(sokk);
	   pressiVeestTyhjaks(sokk);
	}
^
	puhasta(minuSokk);
	puhasta(sinuSokk);
	puhasta(emaSokk);
	puhasta(villaneSokk)
^

// nimetud, lennult loodud eeskirjad:

	$('#button-next').click(function() { changeSlide(RIGHT); });
	$('#button-prev').click(function() { changeSlide(LEFT); });


// nimelised, eelnevalt salvestatud eeskirjad

	function nextSlide() { changeSlide(RIGHT); }
	function prevSlide() { changeSlide(LEFT); }

	$('#button-next').click(nextSlide);
	$('#button-prev').click(prevSlide);

 
ja mainin veel.. järgnevad on samad:

	function nextSlide() { changeSlide(RIGHT); }
	var nextSlide = function() { changeSlide(RIGHT); };
 
eeskirjadele saab lihtsalt nime anda kaht moodi:
 1) nagu tavalistele väärtustele
 2) spetsiaalse süntaksiga

ja samuti saab neile ka nimi andmata jätta ja neid kohe kasutada, nagu ka muid väärtusi


() 
need sulud tähendavad "tee seda" ainult siis, kui sa kutsud protseduuri välja 
function move(direction)  on funktsiooni definitsioon... siin pole väljakutsumisega mingit pistmist. see definitsioon ise ei käivitu enne, kui sa teda hiljem välja kutsud. see ongi abstraktsioon... annad asjale nime ja ta omandab uue mõtte
[ ... ] 
on listi loomiseks, ja samuti olemasolevast listist elementide väljavõtmiseks

	var list = ["tere", "head aega", "tere hommikust", "head ööd"];
	list[0];   => "tere"
	list[3];   => "head ööd"

list[0];  ei kirjutada kunagi tegelt, sest see ei tee midagi. ist[0]   eraldi võtab lihtsalt listist väärtuse, aga see haihtub lihtsalt õhku, sest temaga ei tehta midagi

	teeMidagi(list[0]);  meigib rohkem senssi
	var asi = list[0];

ja listi võib hiljem asju ka juurde panna:

	list.push(uusAsi);

ja vanu asju saab muuta:

	var list = ["tere", "head aega", "tere hommikust", "head ööd"];
^
	alert(list[2]);   // ekraanile ilmub tekst "tere hommikust"
	list[2] = "tere õhtust";
	alert(list[2]);   // ekraanile ilmub tekst "tere õhtust"


veel üks asi; järgnevad lõigud teevad sama asja:

	var newLetter = {letter: "λ", options: ["koer", "siga", "lambda"], answer: 2};
	QUESTIONS.push(newLetter);

	QUESTIONS.push({letter: "λ", options: ["koer", "siga", "lambda"], answer: 2});

sa võid asju ka segiläbi kasutada, aint et üldjuhul on sellele raske vajadust leida.

	segapuder = [10, 99, "tere", 0, {"Erik": 25}, ["veel", "üks", "list"], 10, 5];
	segapuder[0] => 10
	segapuder[2] => "tere"

	segapuder[4] => {"Erik": 25}
	segapuder[4]["Erik"] => 25

	segapuder[5] => ["veel", "üks", "list"]
	segapuder[5][0] => "veel"
^
	var
	var a = 25;
	var lasteVanused = {"Erik": a};
	nüüd on 'lasteVanused' sama, mis `{"Erik": 25}`

ja kui ma peale seda kirjutan:
a = 30;
siis sellest muutuja 'lasteVanused' sisu enam ei muutu, sest sinna sisse läheb muutuja 'a' väärtus, mitte muutuja 'a' ise

	a = 25;
	vanused["Erik"] = a;   // Erik on 25
	a = 30;
	vanused["Joosep"] = a;  // Joosep on 30, aga Erik on endiselt 25

VÕRDLUS VS OMISTAMINE  
üks asi küsib, KAS on võrdne   
teine ütleb, VOT NÜÜD ON võrdne 
direction = LEFT   tähendab, et   direction NÜÜD ON left!  
direction == LEFT   tähendab   kas direction on left?  

ja JSil on ainult piiratud hulk samme, mingi 10 tk maksimum
- väärtuse tekitamine  
- väärtuse muutujatesse panemine
- väärtuse kasutamine

- eeskirja e. protseduuri e. funktsiooni tekitamine
- eeskirja e. protseduuri e. funktsiooni väljakutsumine ja soovi korral talle parameetrite etteandmine
 
attr ei ole sisseehitatud, attr on jQuery teema  
ja length ei ole meetod vaid atribuut   
tegelikult on meetodid ka atribuudid, lihtsalt nad on atribuudid, mille sees on protseduur, ehk siis neid saab kutsuda  

ma olen varem kasutanud mõistet "tekstistring", aga tegelt öeldakse lihtsalt "string"  
	•	täisarvu kohta öeldakse "integer" ehk lühidalt "int"  
	•	kümnendmurru kohta "float" (floating point number)  
	•	ja tõeväärtuse (true või false) kohta "bool" või "boolean" sest Bool  on selle teadlase nimi, kes tõeväärtusalgebra ehk Booli algebra (ingl k. "Boolean algebra") lõi ehk siis iga võrdlus, mida sa teeb, tekitatab/tagastab tõeväärtuse ehk bool'i  

	var kolmOnSuuremKuiNeli = (3 > 4);
	kolmOnSuuremKuiNeli
	kolmOnSuuremKuiNeli === false

ehk siis võrdlused on ka avaldised, millel on väärtus ja mida saab muutujasse salvestada

	slide = $("#slide-1")
	> slide.find("img")

sedasi peaksid saama kõik #slide-1all olevad img tagid 
või kompaktsetl:

	> $("#slide-1 img")

"var nextQuestionNr = currentQuestionNr + 1;"  tähendab järgmist:
võta väärtus, mis HETKEL on currQuestionNr sees, liida sinna 1, ja pane tulemus muutujasse nextQstNr

	function nextSlide() {
	   var nextQuestionNr = currentQuestionNr + 1;
	   preparePassiveSlide(nextQuestionNr);
	   moveRight();
	   currentQuestionNr = nextQuestionNr;
	}

see definitsioon tähendab järgmist inimkeeles:

	moving to the next slide means doing the following:
	   computing the next question number
	       by taking the current question number and adding 1 to it,

	   then preparing the currently hidden/passive slide
	       using the next slide nr we just computed,

	   then moving the slides to the right

	   and finally remembering that we are now at the next question,
	       so next time we repeat the same procedure, we can treat what is currently the next question, as the current question.

LIST
game/a/sound.mp3
game/a/letter.jpg
game/a/option1.jpg
game/a/option2.jpg
game/a/option3.jpg 
ja siis sa käid GAME listist saad võtta neid kirjeid. iga kirje külles on .letter atribuut, ja selle atribuudi järgi saad moodustada teekonna 'game/' + kirje.letter + '/sound.mp3' näiteks

	GAME = [
	   {letter: 'a', right_answer: 2},
	   {letter: 'b', right_answer: 3},
	   ...
	];
see on sul otse Javascrpti koodis defineeritud.. see ongi Javascripti list ehk array
var current_letter_number = 0;   # esimene; array nummerdamine algab 0-st mitte 1-st

// võta õige kirje GAME nimekirjast:
current_letter = GAME[current_letter_number];
// current_letter kirje järgi määra HTMLis õiged teekonnad failideni
// jää ootama, kuni kasutaja tahab minna kas eelmise või järgmise tähe peale ja korda sama protseduuri uue current_letter'iga


	var list = [5, 9, 28, 1, 5, 23, 17, 12];
	list.sort()
	list => [1, 12, 17, 23, 28, 5, 5, 9] 

http://hungred.com/how-to/tutorial-sort-array-javascript/
	sort ascending
	function ascending(a, b)
	{
		return (a - b); 
	}
	var list = [5, 9, 28, 1, 5, 23, 17, 12];
	list.sort(ascending);

	ascending seletatult
	function ascending(a, b)
	{
	    if (a < b)
	        return -1;
	    if (a > b)
	        return 1;
	    return 0;
	}
	var list = [5, 9, 28, 1, 5, 23, 17, 12];
	list.sort(ascending);

	sort random
	function random(a, b)
	{
	return 0.5 - Math.random(); 
	}
	var list = [5, 9, 28, 1, 5, 23, 17, 12];
	list.sort(random);


Math.random()
 tagastab väärtuse vahemikus 0.0-1.0  
täpsemalt väärtuse n, kus n > 0 ja n <= 1.0 vist  
(0.0, 1.0]  
if (randomValue < 0.3)  
else if (randomValue >= 0.3 && randomValue < 0.9)  
else ...  
ei pea olema võrdsed osad, võib olla ka 10%, 50% ja 40%  

erinevad asjad on ju
	var question = QUESTIONS[questionNr];
	var questionEl = slide.find(".question");
	questionEl.text(question.letter);
