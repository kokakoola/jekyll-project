---
layout : blog
title : php vs teised keeled
category : basics
tags : [erik, php, python, sql, security]
description : php vs other languages
comments : true
lang : estonian
excerpt :  Mis teeb php räpakaks keeleks? mäletan, et sa ei pea sellest suuremat lugu just.    
  
---
no näiteks see, et sa pead kirjutama array('tere' => 'tore')... Pythonis {'tere': 'tore'}  
ja et [] ja {} vahel pole erinevust  
ja näiteks selleks, et array'sse midagi juurde lisada, tuleb kirjutada:  
`array_push($myArr, item);`  
Pythonis: 
`my_arr.append(item)`  

a no see on aint kosmeetika.. fundamentaalsed erinevused on  
   `echo $olematuMuutuja;`  
siis heal juhul PHP aint hoiatab sind, et sellist muutujat pole, aga prindib ikka rahumeeli tühjust  
    `print olematu_muutuja`  
selline asi Pythonis annab suure ja koleda errori (mis on hea antud juhul)

\+ siis tavaks saanud probleemid.. näiteks see, et kasutatakse mysql_query funktsiooni, mis on ülimalt low-level
low-level selle koha pealt, et ta ei tee mitte midagi sinu eest ära, mistõttu tekivad turvaaugud näiteks
no oletame, et URL on selline /apartments/?id=123
siis sina PHP's naiivselt teed nii:
$aptId = $_GET['id'];
nüüd sul on seal $aptID muutujas '123'
seejärel:
$apartment = mysql_query('SELECT * FROM apartment WHERE id = ' . $aptId');
sellest tuleb päring  SELECT * FROM apartment WHERE id = 123
kõik OK
kõik toimib
nüüd tuleb kasutaja, kes kirjutab URL'iks:

/apartments/?id=123; DELETE FROM apartment
$aptId on seejärel "123; DELETE FROM apartment"
seejärel see SELECT, mis enne oli kena ja ilus, on nüüd:

SELECT * FROM apartment; DELETE FROM apartment
edasi aimad isegi, mis juhtub

*heh! nii lihtsalt?* 

no kui sa kasutad mysql_query funktsiooni ja ei escape'i kasutaja sisendit ära
a no, seda ei pea tegema, kui sa ei kasuta mysql_ algavaid funktsioone
vaid mingeid abstraktsemaid asju, mis teevad seda automaatselt
näiteks PDO, mis on ka PHP'le sisseehitatud
(PDO = PHP Data Objects)

$query = new PDO('SELECT * FROM apartment WHERE id = ?');
$query->addParam($aptId);
$results = $query->execute();

(ma ei mäleta, kuidas see täpselt oli, aga midagi taolist) võis olla ka lihtsalt:

$query = new PDO('SELECT * FROM apartment WHERE id = ?', $aptId);
$results = $query->execute();

igatahes point on see, et sa ütled talle, et ? kohale tuleb mingi sisend, ja ta ise garanteerib, et see sisend oleks korralikult ja turvaliselt escape'itud

ja kui sa näiteks otsustad hiljem sama koodi PostgreSQL'i või SQLIte'i peal kasutada, siis ta automaatselt escape'ib selle andmebaasi jaoks sobivas formaadis

mysql_* töötavad aint MySQL'iga (ilmselgelt)

(aa ja nagu sa näed, siis PHPs on muutujate ees see kole $, ja meetoditele pääseb ligi märgiga ->, mis on ka kole ja tülikas trükkida... PHP: $foo->bar();  Python: foo.bar() —ja semikoolonit ka pole)

(ja seda peamiselt seetõttu, et punkt oli juba enne ära võetud stringide liitmiseks, kui PHP'sse alles objektid ja klassid lisati)

(aa ja + märk stringidega ei tööta :P tore eks)

Pythonis:
    3 + 3
    "Mare " + "Hunt"
PHPs
    3 + 3
    "Mare " . "Hunt"

AGA
+ töötab stringidega, ta lihtsalt teeb midagi muud :D
nii et errorit sa ei saa
"3" + "3" PHP's annab 6
Pythonis annab ootuspärase "33"
samas kui sa teed "asd" + "bsd" PHP's, siis sa vist saad 0 või midagi sellist, mitte errori

	~$ cat test.php
	<?php

	echo "Mare " + "Hunt";

	~$ php test.php
	0
(näed, PHP faile saab ka käsurealt käivitada väga mugavalt)
