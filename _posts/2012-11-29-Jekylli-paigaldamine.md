---
layout : blog
title : Staatiline blogi Jekylliga
category : how-to
tags : [jekyll, sites, projects]
description : Building a dynamically generated static site
comments : true
lang : estonian
excerpt : Tekstiblogi Wordpressi peal on nagu kopaga peenra rohimine. Tahan staatilist markdownis kirjutatud blogi. Ilma andmebaasi, kasutajaliidese jmt tarbetu kraamita ühe tõesti lihtsa tekstiblogi kohta. Ilma liigsete iluvidinateta nagu etteantud css ja github hosting. Kiiret, ühe näpuliigutusega uuendatavat. Standardse blogistruktuuriga (tagid, kategooriad, arhiiv). 
---

Selleks jäi siis [Jekyll](https://github.com/mojombo/jekyll) - blogiplatform häkkereile. Kellel pole lusti kujunduse ja layoudiga jännata saab võtta Jekylli edasiarenduse [Octopress](http://octopress.org/), veel on samast perekonnast eelkujundatud [jekyll bootstrap](http://jekyllbootstrap.com/) ja [ruhoh](http://ruhoh.com/) on jekylli edasiarendus aga et autor, Jade Dominguez, läks tööle umbes peale seda, pole see vast nii turvaliselt lõpuni ehitatud. 

Kõige lihtsam viis on nimetet bootstrap ja vaba hosting [github pages](http://pages.github.com/). Viimase korral pole muud viga kui et pluginaid ei saa turvakaalutlustel tarvitada. Siinkirjeldatav on juht, kui tarvitusel on puhas jekyll ja hosting on oma serveris. Jekyll on Railsil baseeruv blogividin, seega Rails masinas on eelduseks selle kasutamiseks.

### Kõigepealt lokaalne install:

*  `$ install jekyll` 
	
-  lood [kataloogistruktuuri](http://ostatic.com/blog/build-your-site-with-jekyll) (&#95;config tuleb võtta jekylli githubi lehelt - see on vana postitus ja aeg on edasi läinud, aga aitab alustada. Ametlik [wiki](https://github.com/mojombo/jekyll/wiki/Usage) tundub alguses keerukas. Kui tahad, et :4000 peal otse jookseks, kommenteeri välja baseurl.)
	
*  `$ jekyll --server --auto` 
	`--server` käivitab väikese lokaalse serveri `--auto` võimaldab lehtede automaatset värskendust ja on mugav. Kui sa "autot" ei kasuta, loob käsk `jekyll` staatilise sisuga &#95;site kataloogi, mida su veebileht blogina näitama hakkab. 
	
* ja voila! localhost:4000 peal on su leht.


> [Jekylli pluginad](https://github.com/mojombo/jekyll/wiki/plugins)
> [Jekyll sorteerib kategooriaid](http://dseifried.wordpress.com/2011/11/25/jekyll-yaml-front-matter-and-the-liquid-templating-system/)

### Teine päev
Ma hakkan vaikselt aru saama...

Jekylli kataloogistruktuur on lihtne. Sulle sobivas juurkataloogis peavad asuma:  
	 - index.html  (tavaline index)  
	 - archive.html  (tavaline arhiiv)  
	 - &#95;config.yml  (seaded)  
	 - &#95;layouts dir  (erinevad layoudid eri lehtedele)  
	 - &#95;posts dir  (sinu postitused)  

Kui kataloogistruktuur on paigas (ja &#95;posts dir-i sees on su postitused), siis jooksutades 
terminalis käsku `jekyll` (muidugi pead sa asuma samal ajal oma juurkataloogis), teeb jekyll juurkataloogi uue diri: &#95;site. See on valmis blogi ja kui selle enda serverisse üles riputad, ongi kõik. Kui seda lähemalt uurid, leiad sealt oma postistused korralikult kuupäevakataloogidesse sorteerituna ja puhta html-i kujul [^1]. 

Lokaalis näed seda siis Localhost:4000 peal kui oled jekylli serveri käivitanud käsuga `jekyll --server --auto`. Alakriipsuga nimetused seepärast, et see on välitsus: kõik mitte-alakriipsuga asjad kopeerib jekyll &#95;site kataloogi.

Eriti coole nippe jekylli kustomiseerimiseks (osalt pärit [siit](http://www.kinnetica.com/2011/04/17/jekyll-tips-and-tricks/)):
- YAML Front Matter on see asi, mis iga blogilehe algusse kirjutatakse. YAML kasutab `key : value` süntaksit. Nii saad oma template sisse kirjutada endaloodud muutujaid nagu nt metaandmeid, kategooriaid, tage. Nt käesoleva lehe alguses seisab YAML:

	---
	layout : blog
	title : Jekylli paigaldamine
	categories : how-to  
	tags :
	- jekyll
	- sites
	- projects
	description : Building a dynamically generated static site
	comments : true
	published : true
	sidebar : Tahan staatilist blogi. Ilma liigsete iluvidinateta nagu etteantud css ja github hosting, sest see peab olema loogiline lisa olemasolevale lehele.Ilma sqli, cache jmt tarbetu kraamita ühe tõesti lihtsa tekstiblogi kohta. Kiiret, üle giti hallatavat. Standardse blogistruktuuriga.
	---
	
Ja et ühte `value` neist välja kutsuda, tuleb template sulle vajaliku koha peale kirjutada &#123;&#123; key &#125;&#125;. Nt &#123;&#123; description &#125;&#125; annab teksti "Building a dynamically generated static site" 

Niisamuti saab lisada pilte: lisa YAML front matterisse `image: /img/wing.jpg` ja kutsu templates sobivas kohas välja &#123;&#123;  page.image &#125;&#125;

Postituse nimi peab olema kindla struktuuriga: year-month-day-title.md 

Kui kirjatükk on draft, piisab kui YAMLis panna published : false. Või luua juurkataloogi kataloog drafts ja paigutada postitus sinna.

scripts/ kataloogis käib üleslaadimisskript. &#95;config.yml ignoreerib nii nii draft/ kui script/ kataloogi.

Rohkem pole vaja jutustada: leidsin ammendava juhendi, loe parem [seda](http://erjjones.github.com/blog/How-I-built-my-blog-in-one-day/) (koosneb 2 osast, tagide plugin on teises)

Excerptide tegemise viise on kirjeldatud [siin](http://xconstruct.net/2012/05/01/jekyll-part-1-excerpts/)

[URL rewriting](http://andrewho.co.uk/weblog/clean-urls-on-jekyll-apache)

<div class="last_tweets">
[^1]: Jekyll kasutab vaikimisi markdowni konverterina Marukut, seda saab vahetada. Maruku annab sulle ka jooksvalt teada su markdowni _syntax erroritest_. Nt kui kasutad mõnda markdowni poolt hõivatud tagi tekstis. Siis tuleb see [html-entitiga](http://maruku.rubyforge.org/entity_test.html) asendada
</div>