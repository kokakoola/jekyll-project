---
layout : blog
title : Zurb Foundation workflow
category : basics
tags : [Foundation, framework, scss, sass]
description : starting with Foundation
comments : true
lang : estonian
excerpt : Zurb Foundation, sest esiteks on Bootsrapi liiga palju ja ta kipub töödest läbi kumama, teiseks on Bootstrapi peal lihtne kavandit teha, aga kustomiseerimine on seal vaevaline, kolmandaks on kiidetuim responsive Foundation. Mis on rikkalik layoutimisvõimaluste osas, aga kujunduselementide osas hästi lage. Nii et frameworkiks peaks olema väga hea. 
---

Bootstrapi, Foundationit ja Skeletoni on võrdlus tabelina on [siin](http://responsive.vermilion.com/compare.php). Skeletoni kasutasin viimases projektis ja võin vaid kiita: lihtsamate asjade jaoks väga mugav ja hästi kerge. Marginid on minu maitse jaoks veidi kitsad - pildirohke lehe korral on tulemus tihe. Skeleton on puhas css, javascript tuleb endal külge panna. Pane tähele, et Skeleton on pisut valesti dokumenteeritud - row elemendist pole seal juttu kus vaja. Bootstrapi juures on üsna kole veel, et divi selektorite klassid on span1 jne (teistel on columnid - vähe etem). Samas on Bootstrapil rohkesti lisamaterjale ja juhendeid, mugavalt laiendatav ja teemadega. Foundationiga oled üsna üksi: peamine lisamaterjal on Zurbi enda dokumentatsioon, asjalikke teemasid pole (peale [Reverie](http://themefortress.com/demo/support/)). Foundation kasutab 12-column gridi, millele saab seada nested columne, `row` on selektor, mis hoiab selle sees olevaid asju ühes rivis.

Algatuseks lae alla viimane [Zurb Foundation](http://foundation.zurb.com/download.php). Minu valik oli Foundation scss. Kuidas sassi gemi installida, on samas ilusasti ära seletatud.

Seejärel tavalised sammud:  
- paigalda git e. `git init` projekti juurkataloogis  
- tee repo githubi (oluline, kui arvuti ise ennast kinni kipub panema nagu minul)  
- kirjelda ruby gemset projekti jaoks (vt Hartli tutoorialist)

Edaspidi projekti avades on sammud projekti juurikas:  
- `rvm use 1.9.3@sinuprojekt`
- `compass watch`

Tutooriale on Foundationi kohta vähe ([dokumentatsioon](http://foundation.zurb.com/docs/navigation.php#) ise on üldiselt hea), sestap loetelu leitute kohta:  
- [Üldine pluss multi-device](http://www.w3resource.com/zurb-foundation3/introduction.php)  
- [rapid prototyping zurbiga](http://www.netmagazine.com/tutorials/quickly-build-prototype-test-any-device)
- [off-canvas tut](https://tutsplus.com/tutorial/going-off-canvas-with-zurb-foundation-3-0/) - off-canvas on üks zurbi eksperimentaallayoute (mida kasutab ka reverie-teema), kus mobiilil sidebar nihutatakse ekraanilt horisontaalselt välja ja nupuga jälle sisse kui vaja. Layoudid ise [siin](http://www.zurb.com/playground/off-canvas-layouts#)

Et Zurbiga tehtud asjadel pole silte küljes just, on ka inspireerivaid ilusaid näiteid vähe. Zurbi enda omad:
- [jobs](http://www.zurb.com/playground/off-canvas-layouts#)  
- [case studies](http://foundation.zurb.com/case-jekyll.php) (siin ka typo retsept cross-browser)


### Icon-fonts
Selleks et projekti ikoonidega kaunistada, pakub Zurbi Playground ilusa komplekti [ikoonifonte](http://www.zurb.com/playground/foundation-icons) välja koos asjaliku lisamisjuhendiga. Kuni soovid kasutada ühte ikoonikomplekti, on okei, kahjuks [ei õnnestu](https://groups.google.com/forum/?fromgroups=#!topic/foundation-framework-/Jj9zfn-IQbs) tööle saada mitut fonti korraga. Lahendus on unustada Zurbi fondid ja kasutada Bootstrapi [Font Awesomi](http://fortawesome.github.com/Font-Awesome/), mis on väga lihtne:  
1. Laed fondi alla ja paned oma töökataloogi nt fontide alla  
2. Lisad `<head>`i css-i lingi  
3. Naudid ikoone süntaksiga `<i class="icon-camera-retro icon-large"></i>`

Pärast hiljem kui projekt live läheb ja on selge, milliseid ikoone just kasutad, tasub terve fondi asemel laadida vaid tarvilikud. Siin tuleb appi [Fontello](http://fontello.com/), mis lubab sul koostada enda ikoonidega piirduva fondikomplekti.

Kokkuvõttev artikkel üldise ikoonifondi kasutamise kohta koos mõninga lisaressursiga asub [siin] http://www.vanseodesign.com/web-design/icon-fonts/

Kui sulle nüüd tuli fondiikoonide isu peale, siis Cris Coiyer on teinud korraliku [kollektsiooni](http://css-tricks.com/flat-icons-icon-fonts/).

### Tips

- Kui tahad täislaia vööti teha, pane selektor külge containerile (width: 100%;). row on kindla laiusega, default maksimumlaius rowle on 980px, määratud foundation.css-is. Enne tuleb alati container, seejärel row, seejärel columnid (mida mähitakse html5 tagidesse nagu header, aside, footer). 

- mobiilidele on eraldi mõeldud. nt class hide-on-phones, hide-on-tablets, show-on-desktops ja teised abiklassid, mis võimaldavad määrata osade ilmumisjärjekorda (või ilmumata jätmist) mobiilis. NB! töötavad ekraaniresolutsiooni, mitte laiuse peal, st et näha ainult päris-seadmel, mitte ekraani vähendades.

- grid süsteemid on tundlikud lisapaddingu suhtes (kõik läheb paigast ära). Sel juhul aitab box-sizing: border-box. Kirjeldatud [Paul Irishi poolt](http://paulirish.com/2012/box-sizing-border-box-ftw/). Süntaks css-is siis selline:

	* {
	    box-sizing: border-box;
	}

> Mind painab html-i temlpliitimise võimalikkus/võimatus. Ei meeldi mulle iga alamlehe algusse headi ja lõppu footerit kirjutada. Ja siis pisut ümber mõelda ning igas failis eraldi parandusi tegema hakata. Üleni-rails tundub liiga suurejooneline, jekyll... või mis?

- [Siin](http://tropism.me/blog/2012/10/13/static-site-development-with-middleman-and-foundation/) on üks lähenemine, huvitav, peaks süüvima (sisaldab lisaks middlemanile ja foundationile ka HAMLi, rsynci)  
- mainitud on ka moustache.js  
- ruby partialide [retsept](http://ryanfunduk.com/simple-partials/) html-lehe jaoks  




