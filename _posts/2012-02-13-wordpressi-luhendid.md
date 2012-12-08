---
layout : blog
title : _GET ja Wordpressi teised lühendid 
category : basics
tags : [php, wordpress, shorthand]
description : wordpress basics
comments : true
lang : estonian
excerpt : Kuidas lisada eri kujundusega lehti dünaamiliselt, ilma mitme eri templateta?
---

Alustada tasub ikka error_reporting(E_ALL); peale panemisest. Ja edasi - meetod _GET aitab välja, Wordpressi korral on süntaks jälle eksitavalt erinev, permalingid lisavad vürtsi:
	- 'pagename' annab Page nime;
	- 'page' annab Post nime;
	- $wp_query->post->ID; annab lehe ID

Asi töötab ilusasti mõlema, nii nime kui ID korral. 
ID korral:   

	$id = $wp_query->post->ID;
	if (!empty($id) && ($id === 82)) {
			include('includes/partners.php');
		} 

Lehenime korral:  

	$term = get_query_var('pagename');
	if (!empty($term) && ($term === 'koostoopartnerid')) {
			include('includes/partners.php');
		} 

Kumba kasutada? Pagename oleks muidugi selgem lugeda. Aga arvestades tõlkekeeltega, mis tulemas - ID ja korralikult muutujateks kirjutatud. Defs.inc-i.

> Miks lisada dünaamiliselt ja mitte kirjutada Wordpressi kasutajaliidesesse?

1. Wordpress lisab kangekaelselt break-tagid iga elemendi lõppu ja teeb ul-i algusse eemaldamatuid mummukesi. 
2. Vähem ohtu, et nutikas klient lehe tuksi keerab. 
3. Kaob ära tarvidus järjekordsele pluginale. Enne pidin admini lisama php-plugina, et pilte saaks dünaamiliselt lisada ja lehte kolides ei peaks pilte uuesti linkima. Nimelt tavaline struktuuripõhine linkimine nagu / või ./ Wordpressi korral ei toimi. Dünaamiliselt saab pilte lisada koodijupiga `<?php bloginfo('template_directory'); ?>`
Nt
	<a href="http://www.seb.ee/" title="" target="_blank"&&img src="<?php bloginfo('template_directory'); ?>/images/logos/seb_color.jpg" alt="SEB"/></a> 

4. dünaamiline pildilinkimine viib Validatori veateadeteni. Mingid tagid jäävad validatorile mõistetamatuks.

### Veel märkimistväärivad lühendid:

'bloginfo('url');` - viide avalehele
`bloginfo('description');` - viide lehe nimetusele
`bloginfo('template_directory');` - viide kõigi teemafailide kataloogile

Nt header.php-st logo dünaamiline lisamine:

	<img src="<?php if ($logo) echo $logo; else { bloginfo('template_directory'); ?>/images/logo.png>?php } ?>" alt="<?php bloginfo('name'); ?>" />
