---
layout : blog
title : Update ja Truncate sqlis
category : basics
tags : [mysql, sql, truncate, erik]
description : update and truncate
comments : true
lang : estonian
excerpt : Kuidas saavutada, et toimuks regulaarne update?
---

käivitad import skripti regulaarselt; pead arvestama ka, et andmeid ei tohi andmebaasi topelt kirjutada… seega näiteks kas tühjendad andmebaasi enne ära, või siis kontrollid, kas objekt on juba andmebaasis olemas, ning vajadusel teed UPDATE mitte INSERT

> charseti probleem lahendamata (andmebaas on latin1_swedish_ci, tabel utf8_general_ci)

tabeli encoding on tähtis… a muidugi sa peaks saama ka andmebaasi luua kindla encodinguga… andmebaasi encoding on lihtsalt minuteada default-encoding, mida uute tabelite loomisel kasutatakse, kui tabeli loomisel ei ole teisiti määratud; mingit omaette funktsiooni andmebaasi encoding ei tohiks omada

> kirjutasin oma koodi juurde jupi truncate table - et tabelit regulaarselt värskendada (kustutan kõik ära ja kirjutan uuesti kord päevas). on see õige?

truncate kustutab kogu tabeli, jah;  kui sa saad iga kord feed’ist kõik andmed uuesti, siis see on toimiv lahendus  
kui feed annab sulle vaid uued/uuenenud andmed, siis see ei sobi, sest sellisel juhul pead sa vanad andmed alles jätma ja uue data-set’iga täiendama
aga ma miskipärast arvan, et City24 feed annab sulle lihtsalt kogu data-set’i
ehk siis truncate ja uuestiloomine on OK  
vastasel juhul peaks sa peale uute andmete lisamise ja vanade update’imise ka kustunud andmed ära kustutama, aga ma ei usu, et City24 tüübid on viitsinud sellise asja feed’i lisada  

siinkohal me muidugi jõuamegi küsimuseni, et mis saab, kui sa teed TRUNCATE, ja hakkad uusi andmedi sisestama, ja täpselt samal ajal keegi külastab su lehte—siis ta näeb poolikuid andmeid  
a kui sa teed seda öösel kell 3, on risk suht madal  
+ sa võid kuhugi mingi lipukese püsti panna, nii et index.php lihtsalt teatab kasutajale “Maintenance downtime, please try again in 30 seconds”, ja ei renderda lehte  
 