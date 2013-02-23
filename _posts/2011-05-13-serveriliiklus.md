---
layout : blog
title : Failide liigutamine serveri vahet
category : basics
tags : [gzip, tar, rsync, erik, bash]
description : git basic
comments : true
lang : estonian
excerpt : Kuidas saab asju serveris lahti pakkida? Kohtan juba teist korda soovitust enne .gz serverisse tõsta ja siis seal lahti pakkida.
---
`gunzip `

kausta saad ka pakkida, kui enne .tar'iks teed 

> mis on .tar?

:/ 

`$ tar cf minuasjad.tar minuasjad`  (minuasjad on kaust, mida tahad pakkida)

`$ gzip minuasjad.tar`  (tulemuseks on minuasjad.tar.gz)  

laed minuasjad.tar.gz serverisse ja serveris siis:  
`$ tar xf minuasjad.tar.gz`  
tar xf teeb ise gunzip ja siis pakub .tar faili ka lahti 

samas kogu see jama on mõtekas, kui sul on tõesti palju faile, või asi on suur   ja pakkimisel muutub väiksemaks vastasel juhul käib `scp -r` kah

ja edaspidi üksikute muutuste sünkimiseks on endiselt parim `rsync` 

kui paremat pakkimisvõimsust tahad, siis `bzip2` ja `bunzip2`  
ja lahjema jaoks `zip` ja `unzip`  
zip on sama, mis parema klikiga faili/kausta peal ja Compress  

> ja faili kustutamiseks?

möh??

> kui ma serverist mõnd faili kustutada soovin terminali kaudu

eee

`ssh mare@erik.server.co.ee`
`rm failinimi`

see ei sobi?

ssh'ga sa saad enamvähem samasugusesse keskkonda, nagu see, kus sa Terminali avades juba oled

rsync kustutab ise serveripoolsest kaustast ära need failid, mida sinu kaustas enam pole

### Mare 09.12.2012

rsync on kullatükk. Saad hetkega ja ühe näpuliigutusega oma failid üles.
Nt selle blogi deploymise rsynci käsk on:

`$ rsync -arvuz  --delete --rsh=ssh  /Users/Mare/rails_projects/marehunt/blog/_site/. mare@erik.server.co.ee:www/seldon.era.ee/htdocs/marehunt/blog/`

ja portfolio deploymiseks:

rsync -arvuz --delete --rsh=ssh /Users/Mare/rails_projects/marehunt/static/. mare@erik.server.co.ee:www/seldon.era.ee/htdocs/marehunt/

. lokaalfailide pathi lõpus tähendab "kogu kataloogi sisu"

et mingeid projekti osasid välja jätta, kirjuta käsu lõppu nt --exclude ".git/" --exclude "deploy/"

rsynci võimalusi vaata [siit](http://ss64.com/bash/rsync.html)
