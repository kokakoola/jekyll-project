---
layout : blog
title : json mysqli, array ja object php-s 
category : basics
tags : [erik, json, dict, array, list, object, php]
description : handle json
comments : true
lang : estonian
excerpt :  teiseks, kui sa tahad asju JSON'iks kodeerida, et neid andmebaasi panna, pole vaja neid enne stringiks teha, nagu sa teed    
  
---

sul on:

	   $query = "$xmlrow->PILT1, 
	       $xmlrow->PILT2, 
	       $xmlrow->PILT3,
	       $xmlrow->PILT4,
	       $xmlrow->PILT5,
	       $xmlrow->PILT6,
	       $xmlrow->PILT7
	       ";
	   $pildid = json_encode($query);

peaks olema:

	   $pildid = array(
	       $xmlrow->PILT1,
	       $xmlrow->PILT2,
	       ...
	   )
	   $pildid_json = json_encode($pildid);

ja siis oleks mingi eraldi dict (kasutan Pythoni mõisteid) kuskil, kus sa saaksid välja-identifikaatori map'ida väljade nimetuseks

	$field_titles = array(
	    'signalisatsioon' => 'Signalisatsioon',
	    ...
	    'keskkute' => 'Keskküte',
	    'wc' => 'WC',
	    'tv' => 'TV'
	);

vot sellist dict'i (PHP's on nii list'id kui dict'id ühe nime all—array) saad kasutada hiljem printimisel  
st võtad andmebaasist oma JSON data, dekodeerid dict'iks, käid kõik key'd ja value'd läbi, ja key'st teed title'i selle field_titles dict'i abil  
 andmete sisemised identifikaatorid üldiselt ei pea vastama väljaprinditud nimetustele  
kuna identifikaatorid peavad olema reeglina täpitähtedeta ja vormingus foo_bar_baz, ja nimetused on "Foo bär bäz šš"  

	$json_data_from_db = ...;
	$data = json_decode($json_data_from_bb);
	for ($data as $key, $value) {
	    $title = $field_titles[$key];
	    ?>
	    <?php echo $title ?>: <?php echo $value ?><br/>
	    <?php
	}

see $field_titles on siis see dict, kus sul on seatud vastavusse sisemised id'd nimetustega, st. on öeldud, millisele sisemisele id'le vastab milline "inimloetav" nimetus/title

täpsustan ka, miks ma ei ütle array kohta array, vaid kasutan mõisteid 'dict' ja 'list'  
kui mäletad, siis nii JS'is kui Pythonis 0li kaks eri andmestruktuuri, mille süntaksid olid JS'is ja Pythonis praktiliselt identsed:  

	sokid = ['punane_sokk', 'must_sokk', 'kollane_sokk', 'tiit_sokk']

	laste_vanused = {
	    'Mare' => 13,
	    'Erik' => 26,
	    'Juhan' => 32,
	    'Pets' => 6
	}

esimesel juhul on kantsulud, teisel juhul looksulud  
PHP's neid looksulge (selles kontekstis) pole, on vaid kantsulud  
ja kantsulgude asemel on array(   )  
ja seda array()'d kasutatakse nii list'i [] kui dict'i {} kirjeldamisel  

	sokid = array('punane_sokk', 'kollane_sokk', 'räpane_sokk', 'tiit_sokk')

	laste_vanused = array(
	    'Mare' => 12,
	    'Erik' => 26,
	    'Pets' => 6
	);

ehk siis kui on =>, siis on dict, kui on lihtsalt i, j, x, y, on list
aga tähendused ja otstarbed on erinevad

muuseas kui sind huvitab, siis PHP puhul list on lihtsalt dict'i erivorm, kus key'd on 0, 1, 2, 3:

	$sokid => array('punane', 'must', 'kollane', 'tiit');
	$sokid => array(
	    0 => 'punane',
	    1 => 'must',
	    2 => 'kollane',
	    3 => 'tiit'
	);
see on suht inetu lahendus muidugi, aga nii on

> json decode puhul kasutasin üldse
$data = json_decode($json_data_from_bb, true);
nii annab ta array mulle 

jah, aga see on irrelevantne
see true lihtsalt tähedab, et tagastatakse dict
(näed, sa ütlesid array praegu, ja see on kahetimõistetav)
kui see oleks false, siis ta annaks põmst sama asja (dict'i), a natuke erineval kujul
JS'is dict'id ja objekt'id on üks ja sama asi, PHPs on erinevad

> std Obj on mingi veider formaat millest ma palju sotti ei saa... 

	$vanused => new stdClass();   // jube nimetus muidugi... tegelt on see lihtsalt sama, mis JS'is `new Object();` ja Pythonis `object()`
	$vanused->mare = 13;
	$vanused->erik = 26;

vs:

	$vanused = array();
	$vanused['mare'] = 13;
	$vanused['erik'] = 26;
	// sama muidugi, mis  $vanused = array('mare' => 13, 'erik' => 26);

ma toon näite JSi põhjal:

 // ekvivalentsed

	var mingiObjekt = new Object();
	var mingiObjekt = {};

// ekvivalentsed

	mingiObjekt.foo = 123;
	mingiObjekt['foo'] = 123;

PHP's on esimene süntaks objekt, teine dict (ehk tehniliselt siis array)

	$mingiObj = new stdClass();
	$mingiObj->foo = 123;

	$mingiDict = array();
	$mingiDict['foo'] = 123;

ja palun lõpeta 'array' kasutamine; antud juhul me räägime dict'idest
array all mõistetakse pealegi üldiselt alati list'i moodi asja
PHP on ainus keel, kus array' nimeliste asjadega saab väljendada ka dict'e
(PHP tegelt nimetab dict'e associative array'deks vms)

(associative seetõttu, et selline array assotseerib e. seostab  key'd value'dega)
