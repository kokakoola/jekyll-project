---
layout : blog
title : php failistruktuur
category : basics
tags : [erik, php]
description : php vs other languages
comments : true
lang : estonian
excerpt :  tegelt kõige parem on üldse, kui "äriloogikat" ehk siis koodi, mis määrab rakenduse navigatsiooni ja loogika ja DB jne, mitte segiläbi panna ühte ja samasse .php faili    
  
---

näiteks mida saab teha, on jagada rakendus 2 kihiks—1. kihti nimetatakse kontrolleriks, 2. kiht on view/vaade e. presentatsioonikiht 

kontrolleris suhtled andmebaasiga ja otsustad, *mida* kasutajale näidata; view kiht määrab, *kuidas* näidata 

kontroller näiteks *kogub* andmed DB'st kokku, paneb mingisse (eeltöödeldud) *pakki*, ja kutsub view välja andes talle selle paki kaasa 

view on tegelt lihtsalt template, ja kuna PHP ongi template'imiskeel algselt, siis tavaline .php fail võib ka template olla 

> *mõtlesin selle peale. aga et kontroller kontrolliks ühte view kihti, tundus see ülepingutatud*

jah, seda küll, a no ta ei pea kontroller olema; võib lihtsalt olla lahus hoitud 2 eri loogikat  
see, mil määral need piirid eri kihtide vahel "materialiseeritud" on, on su enda otsustada  
"materialiseerituse" all pean silmas umbes sellist analoogiat, et kas mingid nimetused ja mõisted ja piirid on ainult sinu peas, või on nad koodis ka reaalselt eri tükkidena

näiteks väga lihtne variant:  kogu loogika on ühes samas jadas (fail, funktsioon, klass, misiganes), ja piir läheb ainult loogiliselt... st et alguses on kontrolleriloogika ja pärast view 

raskekaaluvariant oleks midagi sellist, et sina kirjutad kontrolleri ja commit'id kuhugi SVN/git reposse, ja siis keegi teine programmeerib eraldi view kihi 

ja siis on veel hunnik vahepealseid variante 

aga printsiip on sama: mitte segiläbi kirjutada HTML'i väljastamist ja andme/navigatsiooniloogikat 

näiteks mida sa teha võid: 

	$tplData = array(); 

	$jsonData = mysql_query(...); 
	$data = json_decode($json_data, true); 

	for ($data as $key, $value) { 
	    $title = $fieldTitles[$key]; 
	    array_push($tplData, array('title' => $title, 'value' => $value); 
	} 

^

	<h1>Kasulikud Andmed</h1>
	<div id="container">
	    <?php for ($tplData as $item): ?>
	    <div class="useful-item">
	        <h2><?php echo $item['title'] ?></h2>
	        <?php echo $item['value']; ?>
	    </div>
	    <?php endforeach ?>
	</div>


st see võib sama fail olla; aga kui sa "üldloogika" osa loed/kirjutad, ei koorma sa oma aju HTML'i-jamaga; ja vastupidi

ja see array_push seal mu näites:
seal on nii, et $tplData on list, ja $tplData sisse pushitakse üksteise järel dict'e
(ehk siis "välimine" array on list, selle listi sees olevad elemendid on dict'id)

PHP süntaksiga on see muidugi kõik ilgelt kohmakas...

Pythonis saaks kirjutada näiteks:
	tpl_data = [{'title': FIELD_TITLES[key], 'value': value
	                    for key, value in json.loads(json_data)]

> *sellega teed sa uue listi, milles key-d on dict-is määratud terminid ja value-d ei muutu - saan ma õigesti aru?*

jah, uue listi template'i jaoks kus key on juba map'itud title'iks
json_decode tagastab tegelt täpselt sama andmestruktuuri
lihtsalt ma konverteerin selle sedasi, et key'de asemel on title'id

	json_data = [
	    {'key': 'wc', 'value': 'jah'},
	    {'key': 'rodu': 'value': 'jah'},
	]

^

	tpl_data = [
	    {'title': "WC", 'value': 'jah'},
	    {'title': "Rõdu", 'value': 'jah'},
	]

tegelt võib isegi teha lihtsamalt

	tpl_data = [
	    ("WC", "jah"),
	    ("Rõdu", "jah"),
	]

a PHP's see muidugi ei annaks midagi  
Pythoni puhul oleks hiljem HTML genereerimisel kasu sellest, aga PHP ei oska midagi targemat teha sellega  

http://pastie.org/2913784  
$field_titles pane kuhugi eraldi faili defs.inc.php vms, ja tee põhifailist "include('defs.inc.php');"  

> *kas andmebaasipäring läheb ka defs.inc.php-i?* 

ei
defs = definitions

	if ($value !='') { ?>
	    <?php echo $title. (', '); ?>
	<?php }

^

	if ($value != "") {
	    echo $title . ',';
	}

ehk siis see esimene variant on küll üleliigselt keerukas... sellisel puhul pole mõtet PHP blokist välja minna selleks, et seda kohe uuesti alustada, lõpetada ja uuesti alustada  
need looksulud võib ka ära võtta, kui if'ile järgneb aint üks lause  
aint siis tuleb hoolikas olla, et nad tagasi panna, kui if'i sisse jälle üle 1 lause paned  
see on hea tava muidugi neid alati kasutada  

ja endiselt: ära kasuta eestikeelseid nimetusi (v.a. andmeväljade identifikaatorid, mis juba on eestikeelsed sissetulevas voos)

> *kas duubeljutumärkidel on põhjendus-vajadus või sa lihtsalt panid? ($value != "")*

üldiselt minu konventsioon on see, et:  
tehnilised stringid '...'  
inimloetav tekst "..."  
st igasugused teated, pealkirjad, bla topeljutumärkidega  
igasugused identifikaatorid ja HTML tükid ühekordsetega  
muidugi Pythonis on seda konventsiooni väga mugav järgida, sest mõlemad on täpselt ekvivalentsed  
PHP's on nad natuke erinevad... '' sisse ei saa muutujaid panna  

tegelt nimetatakse seda string interpolation'iks  
 Python:  "Tere, minu nimi on %s" % name   
PHP: "Tere, minu nimi on $name"  
üldiselt mulle isiklikult see PHP lahendus ei meeldi ja ma teen alati PHPs:  
"Tere, minu nimi on " . $name

ja endiselt: ära kasuta eestikeelseid nimetusi (v.a. andmeväljade identifikaatorid, mis juba on eestikeelsed sissetulevas voos)

asi on tavas
\+ selles, et programmeerimiskeeled on kõik inglise keele baasil  
\+ eesti keeles on käänamine  
tuba -> toad  
ja tehniliselt võttes on see üldiselt keerukas  
inglise keeles on 99.9% lihtsalt 's' lõpus  
seega sul tekib:  
for ($toad as $tuba)  
vs:  
for ($rooms as $room)  
ingliskeelne variant on matemaatiliselt lihtsam  
ainsus + s  

siis on veel näiteks toa_id  
vs room_id  
ja tuba_id on kole  
ja kui on tuba ja toa_id, on jälle kole  
eriti Pythonis on erinevus selge:  

for tuba in toad:   
for room in rooms:    
viimane on terviklik lause; esimene on mingi Estonglish moodustis  
+ see "lingua franca" asjaolu ka, mis sa välja tõid