---
layout : blog
title : Wordpressi lokaalne install XAMPPi peal 
category : basics
tags : [php, wordpress, install]
description : wordpress install
comments : true
lang : estonian
excerpt : Lokaalne install on lihtne, eelduseks MAMP või XAMPP
---

1. lae alla, paki lahti, pista htdocsi (tühikuid ära katalooginime sisse jäta)
2. phpmyadminis loo uus andmebaas prefiksiga wp_
3. wp-config-samples muuda andmed (baasi nimi, password - pärit php-myadminist)
4. jooksuta installscript (localost/su wordpressikataloogi nimi/wp-admin/install.php või midagi sellist)
installitud.

nüüd permissionid. tavaliselt on kohe õiged. aga kui Wordpessi install annab veidraid veateateid on see esimene veakoht: ilma ei lase wordpress permalinke muuta ja üldse on jama.
vaikimis peale installi on grupp sama, mis owner. pane grupiks nobody (et värk käib läbi apache, ei ole enam kasutaja sinu arvuti vaid apache. ja kui apache pole just konfigureeritud teisiti, on apache nimi nobody)

`$ ls -la wordpress4` (näitab permissione)

omaniku muutmine:  
`sudo chown -R nobody wordpress4` (R on rekursiivne ehk muudab kogu kataloogi sisu. sudo nõuab root passwordi)

grupi muutmine:   
`sudo chgrp -R nobody wordpress4` (see on siis see õige, mida teha vaja)

nüüd permissionid. õige on 755, järgmine pehmem on 775. 777 ei ole aktsepteeritav.
`sudo chmod -R 755 wp-content`

veel on vaja .htaccess faili. nähtamatu desktopil. lahendus: ava tekst editoriga (seal saab märkida et näita invisible faile) vana htaccess ja salvesta uude wordpressi installi. muuda ühtlasi juurkataloogi nimi õigeks. permissionid htaccessile:  
`sudo chmod 755 .htaccess`  
(kontrolliks proovi wordpressi kasutajaliideses permalinke muuta. kui .htacessi teade on kadunud, on korras)

* kui kasutad timthumbi, peab selle cache chmod olema 777. või timthumb ei tööta.

* “BTW the three numbers in chmod describe rights for “user”, “group” and “others”. read==4, write==2, execute==1. Sum of rights make up the number. Hence 777 means read, write and execute for user, group and others. 660 means read and write for user and group, no rights for others.
NEVER do a chmod 777 on any file or directory. NEVER recommend anyone to do it either!”

### Lehe kolimine lokaalis:
enne ikka backupid. duplitseerisin andmebaasi (vt vale), tegin kogu wordpressi folderist duplikaadi JA SIIS:
- deaktiveeri kõik pluginad
- lae alla uus wordpress
- asenda vana wordpressi sisu uuega. ÄRA PUUTU kataloogi wp-content. alles peavad jääma ka wp-config, .htaccess, uploads (jääb vaikimisi, sest seda pole installis)
- mine korra dashboardi. teeb andmebaasi-update.
KÕIK.