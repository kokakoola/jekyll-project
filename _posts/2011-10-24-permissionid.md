---
layout : blog
title : Permissionid
category : basics
tags : [permission, bash, erik]
description : permissions
comments : true
lang : estonian
excerpt : 
---

erik@erik:/home/mare/www/seldon.era.ee/htdocs/wordpress/wp-content$ ls -la

	total 14
	drwxr-xr-x  6 mare  mare   512 18 mai   16:05 .
	drwxr-xr-x  6 mare  mare  1024 19 mai   16:12 ..
	-rw-r—r—  1 mare  mare    30 14 mai   18:15 index.php
	drwxr-xr-x  2 mare  mare   512 14 mai   18:15 languages
	drwxr-xr-x  9 mare  mare   512 24 mai   14:25 plugins
	drwxr-xr-x  5 mare  mare   512 16 mai   16:20 themes
	drwxrwsr-x  3 mare  www    512 18 mai   16:16 uploads
	
näed, wp-content kaust (see kõige esimene punktiga rida) kuulub sulle, ja kirjutusõigus w on olemas  

permissioni muutmine:  
chmod 766 fail  
tavaliselt on mingi 755 või 644 või 775 ja 664  

nii, ja kuidas ma kontrollin, et kas sai õige permissioni külge (644 siis)
ls -l fail
või noh, ls -l

XAMPP permissionid wordpressile  
sest ta jookseb apache’i alt  
ja apache’i ei jookse samades õigustes mis sina  

sa võid teha uue grupi ‘webdev’ (igale projektile eraldi pole vaja, sest nagunii kõikidel on samad õigused—aint sina)  
panna kõik failid sellesse gruppi ja lisada apache’ ka sellesse gruppi
ja anda grupile kirjutusõigus kõikidel failidel  

a sa võid kaval ka olla ja ära kasutada asjaolu, et Apache’ grupp on www-data (peaks olema vähemalt) (kui pole, siis on www) a võid failid lihtsalt sellesse gruppi lisada. või noh, piisab, kui sa upload kausta sellesse gruppi lisad ja paned grupile seal kirjutusõiguse. ülejäänud failidele pole mõtet. ja gruppi saad määrata chgrp’iga  
või chown’iga ka  
chown user fail  