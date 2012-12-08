---
layout : blog
title : Php parser
category : basics
tags : [mysql, parser, php, xpath]
description : php parser
comments : true
lang : estonian
excerpt : 
---

Minult:  

	<?php $prismaFeed = 'https://realexport:le7462realrt@maakler.city24.ee/broker/city24broker/xml';
	$xml = @simplexml_load_file($prismaFeed) or die ("no file loaded");

	echo "<strong>kahetoalised
	";
	foreach ($xml->xpath('//ROW[KIRJELDUS_TOAD="2"]') as $row) {
	    echo $row->MAAKOND, ' hinnaga ' , $row-> HIND, ' maakler ', $row->MAAKLER_TELEFON;
	    echo "
	"; 
	}

	echo "ühetoalised
	";
	foreach ($xml->xpath('//ROW[KIRJELDUS_TOAD="1"]') as $row) {
	    echo $row->MAAKOND, ' hinnaga ' , $row-> HIND, ' maakler ', $row->MAAKLER_TELEFON;
	    echo "
	"; 
	}

	?>

Erikult:

	<html>
	<head>
	    <meta http-equiv="content-type" content="text/html; charset=utf-8"/>    
	  </head>

	  <body>

	    <?php
	    $prismaFeed = 'https://realexport:le7462realrt@maakler.city24.ee/broker/city24broker/xml';
	    $xml = @simplexml_load_file($prismaFeed) or die ("no file loaded");
	    ?>

	    <h1>kahetoalised</h1>

	    <?php foreach ($xml->xpath('//ROW[KIRJELDUS_TOAD="2"]') as $row): ?>
	    <div>
	      <?php echo $row->MAAKOND ?> hinnaga <?php echo $row->HIND ?> maakler <?php echo $row->MAAKLER_TELEFON ?>
	    </div>
	    <?php endforeach ?>

	    <h1>ühetoalised</h1>

	    <?php foreach ($xml->xpath('//ROW[KIRJELDUS_TOAD="1"]') as $row): ?>
	    <div>
	      <?php echo $row->MAAKOND ?> hinnaga <?php echo $row->HIND ?> maakler <?php echo $row->MAAKLER_TELEFON ?>
	    </div>
	    <?php endforeach ?>

	  </body>
	</html>

 peaks töötama

Xpath'iga saad, jah, andmed XML'ist kätte  
edasi teed mis tahad nendega; antud juhul ilmselt on sul vaja nad, jah, andmebaasi pista  
a sa pead enne mõtlema natuke  
kuidas XML struktuur SQL struktuurile vastab  
sest XML on hierarhiline e. puukujuline  
SQL on aga lame  
aga selleks on sul Manga  
see on selline nokitsemine, kus sa kiirustada ei tohi  
pead asja rahulikult uurima, katsetama, ja natuke huvi tekitama endas
perfektsionist tuleb ka olla; st "ah, nüüd näib töötavat küll" suhtumine ei tööta siin eriti hästi  
pead geek'iks/nerd'iks kehastuma hetkel  
krt ma vaatan praegu https://maakler.city24.ee/broker/city24broker/xml ja see on ikka jube, mis sitta nad teevad seal  
a no hea on see, et kuna see pole sisuliselt puukujuline, vaid on 1:1 väljavõte SQL tabelist, siis on sul lihtne see kõik ka SQL'i toppida
sul on vaja luua aint tabelid eri objektitüüpide jaoks, sest Korter ja Äripind on erinevate column'itega  
nii et tabelid 'korter' ja 'aripind' jne oleks sobivad ilmselt  
(+ mingi prefiks, sest sa pead neid Wordpressi tabelitega samas andmebaasis hoidma, ja ilma prefiksita läheb segaseks)  
(mareopibprogema_korter ja mareopibprogema_aripind jne näiteks)  
alati kasuta prefiksit, kui ühes andmebaasis on n>1 rakenduse tabelit  