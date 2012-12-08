---
layout : blog
title : Javascript konsoolil
category : basics
tags : [ javascript, erik ]
description : javascript
comments : true
lang : estonian
excerpt : Sa võid proovida näiteks nii, et paned konsooli pealt mõnele DOM elemendile ‘mouseover’ või ‘click’ vms event-handleri külge
---

$(“#slide-1”)  annab sulle <div id=”slide-1”>

$(“#slide-1”).mouseover(function() { alert(“your put the mouse cursor over slide 1”); });

või siis võid $(“#slide-1”) mingisse muutujasse (nt ‘slide1’) salvestada ja toda edaspidi kasutada

või sa võid ka globaalseid muutujaid ‘passiveSlide’ ja ‘activeSlide’ kasutada, sest need on ka konsooli pealt nähtavad

kõik su programmis defineeritud protseduurid ja globaalsed muutujad/konstandid on konsooli pealt ligipääsetavad

toksi näiteks konsooli peal: LEFT

või LAST_SLIDE_NR

või changeSlide (ilma sulgudeta)

siis ta ütleb, et muutuja ‘changeSlide’ sees on protseduur/funktsioon

nüüd proovi changeSlide(RIGHT)

nüüd tee näiteks selline trikk, et muuta “jooksvat” programmi sedasi, et pane ‘changeSlide’ tegema lisaks midagi täiendavat

alustuseks anna changeSlide’ile alias:

changeSlideOld = changeSlide (ilma var’ita, sest see on globaalne nimi)

seejärel defineeri uus protseduur ‘changeSlide’, mis kutsub välja vana, kasutades aliast, mille sa just lõid

ja lisaks vana väljakutsumisele näiteks enne seda tee alert(“changeSlide!”);

ja seejärel proovi Next ja Previous nuppe vajutada

mina tegin nii, et andsin changeSlide’ile aliase ‘changeSlideOld’ nagu ma ülal soovitasin, ning seejärel sisestasin:

function changeSlide(direction) { alert(“changeSlide!”); changeSlideOld(direction); }

(seal protseduuri sees on 2 rida tegelikult, aga nad võib ühele reale kokku kirjutada, kui neil semikoolon ; vahel on (ja tee ikka kõike konsooli pealt, mitte javascripti faili muutes)

changeSlideOld = changeSlide ja function changeSlide(direction) { alert(“changeSlide!”); changeSlideOld(direction); }

sa võid algse olukorra ka sedasi taastada:

changeSlide = changeSlideOld

mingiList.each(mingiEeskiri);

siis sa kutsud välja mingiList.each meetodit andes talle kaasa mingi eeskirja

reaalselt JS listidel seda ‘each’ meetodit pole, on ainult jQuery asjadel

aga sa võid ‘sokid’ listi jQuery’iga ära wrappida ja siis each’i kasutada:

$(sokid).each(…)

ja jQuery each ei anna kaasapandud eeskirjale mitte ainult igat listi elementi, vaid ka iga listi elemendi numbri:

	$(sokid).each(function(number, element) {

	    alert(“Hakkan pesema sokki nr ” + number);

	    peseSokk(element);

	});

   console.debug(“stepNr = “, stepNr);

A great way to check if it is pulling the correct value, try this.

	var z = $(“#element”).css(‘z-index’);

	alert(z);

	foo1(function() {

	    doSmth();

	    doSmth();

	});

	foo2(

	    function() {

	        doSmth();

	    },

	    function() {

	        doSmth();

	    }

	);

	foo1(function() { doSmth(); });

	foo2(function() { doSmth(); }, function() { doSmth(); });

	foo2(function() { doSmth(); },

	     function() { doSmth(); });
