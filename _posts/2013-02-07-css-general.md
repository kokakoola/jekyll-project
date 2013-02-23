---
layout : blog
title : CSS oma ilus ja valus
category : resources
tags : [web design, css, IE7]
description : Some practical CSS3
comments : true
lang : estonian
excerpt : On selgunud, et uhkelt pead selga lüüa ja vanu IEsid ignoreerida siin ei saa. Olgu pääle - kogun siia kokku CSS layoudi trikid erinevate brauserite vahel.
---

Display Inline vs Float. Float ei tööta kui on eri kõrgusega kastid. Inline Block on li element, millel säilivad boxi omadused - laius, kõrgus, alignement. Pane tähele, et li inline omandab 4px laiuse margini elementide vahele kui li on htmlis korralikult indenditud. Selle vastu aitab, kui kirjutada markup li-de osas ühte rivvi. Lähem seletus ja IE-hack [siin](http://robertnyman.com/2010/02/24/css-display-inline-block-why-it-rocks-and-why-it-sucks/)

Ebamäärase laiusega elementide tsentreerimisest [siin](http://www.red-team-design.com/center-a-block-element-without-knowing-its-width-part-ii)

[z index](http://philipwalton.com/articles/what-no-one-told-you-about-z-index/)

### Semantiline html
[klassinimedest](http://www.brettjankord.com/2013/02/09/thoughts-on-semantic-html-class-names-and-maintainability/)  
siitsamast üks lahendus korduvate, pisut erinevate klasside jaoks:

    <div class="reviews-albums">
    <h2>Album Reviews</h2>
    ... 
    </div>

    <div class="reviews-books">
    <h2>Book Reviews</h2>
    ... 
    </div>

    [class*="reviews-"] {/* Module Styles */} 

    .reviews-movies {/* Sub-Module Styles */} 
    .reviews-albums {/* Sub-Module Styles */} 
    .reviews-books {/* Sub-Module Styles */} 

ja siin raamat [sellest](http://smacss.com/)

- kuidas vahetada pilte mobiili-tavaekraani korral ja [teisi](http://www.jordanm.co.uk/lab) toredaid eksperimente (nt responsive [horisontaalne leht](http://www.jordanm.co.uk/lab/horizontal-columns) )