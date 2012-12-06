---
layout : blog
title : Sea korda Railsi arenduskeskkond
category : how-to
tags : [Rails, Development, Setup]
description : Set up Rails Development Enviroment OSX 10.6.8
comments : true
lang : estonian
excerpt : Enne kui ma PÄRISELT unustan, olgu kirja pandud - järgmise süsteemivahetuse puhuks. Probleem - Leopardilt Snow peale üle minnes enam uut Ruby äppi luua ei saanud. Bundle install andis jsoni gemi juures vea ja kogu muusika. 
---

`$ cat /Users/Mare/.rvm/log/ruby-1.9.3-p327/configure.log` annab inetu tulemuse. 

Lahendus (aitäh, Janika Liiv, Mihkel Sokk, Google ja Stackoverflow):

1. Viska ära oma vana, tarbetuks muutunud Xcode - see ei tööta uue süsteemi peal.Pealegi on sellest Railsi jooksutamiseks vaja ainlt GCC-d, mis on saadaval eraldi ja kordi väiksem kui terve Xcode. Kui sul mingil põhjusel on vahepeal kaotsi läinud uninstall script (nagu mul), siis lae alla toimiv 3.x (vist oli 3.2) Xcode ja kasuta selle unistalli - võtab maha kogu varasema Xcode. Alates Xcode 4-st piisab (väidetavalt) Developer kataloogi ära viskamisest, varasemate versioonide korral on failid üle kogu kõvaketta laiali ja kataloogi äraviskamine ei vabasta sind KOGU Xcodest.  
`$ sudo /Developer/Library/uninstall-devtools –mode=all` 

2. [Viska ära oma rvm](http://www.mkoby.com/2011/06/03/completely-removing-rvm/) koos selle peal jooksva Rubyga

3. Installi GCC Package.  
	`$ wich gcc` -- näitab gcc asukohta  
	`$ gcc` -v -- näitab versiooni  

4. Installi Homebrew (`/usr/bin/ruby -e "$(curl -fsSL https://raw.github.com/gist/323731)` või `ruby -e "$(curl -fsSkL raw.github.com/mxcl/homebrew/go)"`)  
	Brew help:  
	`$ man brew` ja `$ brew home`

5. Jooksuta Terminalis brew doctor ja järgi selle juhtnööre ülejäänud tarbetute, mõttetute ja kahtlaste failide eemaldamiseks, mida homebrew leiab.
Minu korral nt   
	`$ rm -rf /usr/local/lib/libsqlite3.la`  
	`$ rm -rf /usr/local/lib/pkgconfig/sqlite3.pc`  
	`$ rm -rf /usr/local/lib/libsqlite3.a`  
	`$ rm -rf /usr/local/lib/libsqlite3.0.8.6.dylib`  

6. [Installi rvm]( http://ryanbigg.com/2011/06/mac-os-x-ruby-rvm-rails-and-you/ ) ja jälgi ka rvmi antavaid seadistusjuhiseid (siin ka üks [dummy-juhend](http://www.moncefbelyamani.com/how-to-install-xcode-homebrew-git-rvm-ruby-on-mac/) mida ma küll ei kasutanud)

7. Installi rvmi peale Ruby:   
	`$ rvm requirements`  
	`$ rvm install 1.9.3`  

Homebrew on kullatükk, mis aitab Pathi puhtana hoida ja kõike muud tarvilikku installida (nt git kui sa veel ei kasuta)

Edasi võid nautida [Hartli Ruby on Rails tutoriali](http://ruby.railstutorial.org/ruby-on-rails-tutorial-book) ilma liigse peavaluta. 
