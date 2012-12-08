---
layout : blog
title : Mis on Python
category : basics
tags : [python, erik]
description : what is python
comments : true
lang : estonian
excerpt : kui sa tahad teha ainult brauseris jooksvaid rakendusi e. JS rakendusi, mille üks omadustest on see, et nende olek/andmed pole püsivad ja peale igat refreshi on jälle algolek, siis piisab Javascriptist..
---

tiimides töötades on tihti ka nii, et keegi teeb serveri poolt, mille olek on püsiv ja mis kasutab andmebaasi, ja keegi teeb JSi
 
aga kui sa tahad paralleelselt ka tasapisi hakata mõtlema serveripoole peale, mis avab uksed andmete hoidmise, sisuhalduse jms maailma, siis võid vaadata ka Pythonit, Rubyt, PHP'd, vms
 
aga sellega on mõtekas paralleelselt tegeleda, sest JSiga sa saad praktilise tulemuseni kiiremini, sest seal on vähem asju, mida teada
 
serveripoolega tegeledes on vaja hoomata andmebaasi (piisavalt, et sa saaksid aru, mis see on, ja mingid põhiprintsiibid ja konkreetsed toimingud), ja lihtsamaid HTTP põhimõtteid, ehk siis kuidas päringud ja vastused toimuvad
 
see pole mitte midagi suurt ega keerulist, lihtsalt JSis sa oled praktilisele väljundile lähemal, seega JSiga jätkamine on ju iseenesestmõistetav
 
sinu valik on, kas sa tahad kahel rindel korraga areneda (mis pole 2x raskem vaid 1.3x raskem)
 
aga samas huvitavam ja lõppkokkuvõttes on tulemus 2.5x parem
 
st sinu teadmised ja mõtlemisoskus paraneb teadmiste kombineerimisega rohkem kui üksikute teadmiste summa  
ja Pythonis saad sa teha ka kliendipoolseid e. desktop-rakendusi, millel on graafiline kasutajaliides... aga brauseris tõesti enamjaolt Pythonit ei jooksutata, kuigi tehniliselt on see võimalik ja seda on tehtud... ja samamoodi on olemas vahendeid, mis võimaldavad sul kirjutada oma JS rakendust Pythonis ja Pythoni kood transparentselt tõlgitakse JS'iks
 
Google tegi selle trikiga algust, kui nad kirjutasid GWT (Google Web Toolkit vms), kus arendajad kirjutavad 100% Java koodi, mis kompileeritakse Javascripti koodiks jam is jookseb suvalises brauseris
 
ehk siis on võimalik kasutada "päris" keelt kõigi korralike vahenditega, ja samas asja jooksutada maailma kõige levinuma keele Javascripti keskkonnas
 
(jah, Javascrit on maailma kõige levinum keel, sest absoluutselt iga arvuti maailmas toetab seda, kuna igas brauseris on javascript)
 
(ainult C ja C++ pakuvad Javascriptile konkurentsi, sest kõik opsüsteemid on kirjutatud C's ja C++'is)

> mida tähendab execute permissionides?

käivitusõigus
seda on vaja programmiel ja skriptidel, mida soovitakse käivitada programmina
näiteks kui on Pythoni skript, siis saab käivitada kaht moodi:

	$ python skript.py
	$ ./skript.py

see viimane eeldab, et skript.py'l on exec õigus

	chmod +x skript.py

[esimese puhul on suva, sest esimese puhul on käivitatavaks programmiks python
ja pythonile antakse lihtsalt parameetriks skriptinimi, mida interpreteerida
teisel juhul käivitatavaks programmiks ongi skript ise
skripti esimesel real on muidugi 

	#!/usr/bin/python

mis tähendab, et tegelikkuses käivitatakse ikkagi python ja kõik käib samamoodi nagu esimesel puhul
aga tehniliselt on tegemist programmi execute'imisega
näiteks sa võid .py laiendi üldse eemaldada ja siis ei ole vahet, kas skript on päris-programm (masinkood) või skript (PHP või Python või Ruby või Perl jne)

	mv skript.py skript
	chmod +x skript
	./skript

näiteks kui sul on Deskop’i peal foo.py, siis kui Terminali lahti teed, sisestad käsud:

	cd Desktop
	python foo.py
	ja pythoni konsooli pealt saab ka nii: execfile(‘failinimi’)	
