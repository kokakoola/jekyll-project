---
layout : blog
title : kood kui selline 
category : basics
tags : [code, erik]
description : handle json
comments : true
lang : estonian
excerpt : Ja su põhiprobleem on endiselt see, et sa ei saa aru koodist. See eilne probleem näitas seda selgelt. Seega kui sa üldisesse koodimisoskusesse rohkem aega ei investeeri, on ülejäänu sinu jaoks raske. Ja lõppkokkuvõttes mõttetu...
---

st kui sa näed mingit N rida koodi ja sa ei saa aru, kuidas see kood põhimõtteliselt käitub, on halvasti
st kui sa näed:

	for (...) {
	    do_smth1();
	    do_smth2();
	}

	do_smth3();

või:

	for (...) {
	    do_smth1();
	}
	do_smth2();
	do_smth3();

ja ei tee neil kahel vahet
siis on jama
st sa pead aru saama, et esimesel juhul on muster selline:

	do_smth1();
	do_smth2();
	do_smth1();
	do_smth2();
	do_smth1();
	do_smth2();
	do_smth1();
	do_smth2();
	...


	do_smth3();

ja teisel juhul:

	do_smth1();
	do_smth1();
	do_smth1();
	do_smth1();
	do_smth1();
	do_smth1();
	...


	do_smth2();
	do_smth3();

...näed mustreid?
kui näed, siis on hästi;  koodimisoskus seisneb selles, et sa vaatad koodile peale ja kujutad oma peas ette mustrit, mida sellise koodi käivitumine tekitab
ja ideaalis ka, et kui näed mustrit päriselus või ekraanil, siis oskad selle mustri kompaktifitseerida koodiks
st kui näed

	a b   
	a b  
	a b   
	a b   
	a b       
	c

siis näed.. ahaa, for loop, for loop'i sees on a ja b
ja siis peale for-loop'i tuleb lihtsalt ükskord  c
ja samas kui näed

	a b c    
	a b   
	a b    
	a b    
	a b c    
	a b c    
	a b    
	a b

siis vaatad, et PEAAEGU on nagu for-loop, aga mingi asi natuke vaheldub
ahaa... järelt on peale a'd ja b'd mingi if, mille sees on c, ja see if ei käivitu iga kord

	for (...) {
	    a();
	    b();
	    if (...) {
	        c();
	    }
	}

> mhmh. siin läheb keerukaks kui on asjad üksteise sees.

	a b c    
	a b    
	a b    
	a b    
	a b c    
	a b c    
	a b    
	a b

kas see on keerukas siis?

iga kord on "a b" olemas, aga "c" on olemas aint mõnikord  
järelt "c" on mingi if-i sees  
ja muidugi need mustrid hakkavad mingi hetk muutuma jadadest kahemõõtmelisteks tabeliteks  
näiteks kui sul on for for'i sees

	for dataset in datasets:
	    for item in dataset:
	        ...

(Python)
siis tekib selline muster:

	1 2 3 4 5 6 7 8 9
	* * * * * * * * *
	* * *   * * *   *
	* * *   * * *   * 
	* * *       *   * 
	*   *           * 
	    *           *

1 2 3 4  ... on välimine (esimene) or-loop  
iga numbri all olevad tärnikesed on sisemine (teine) for-loop  
seal mustris on datasette 9 tk  
ja igas dataset'is on erinev arv item'eid  
mistõttu tärnitulpade kõrgus erineb  
ja protsess ise käib ülalt alla, seejärel paremale järgmine tulp, jälle ülalt alla, jne  
(sa ei pea seda nii pidi visualiseerima, võid ka vastupidi)  
ja samuti kui sul on 3kordne nested for, siis muutub see muster juba 3mõõtmeliseks  
sellisel juhul iga tärnike kasvab ekraanist välja omakorda mingiks jadaks
(sel põhjusel, muide, on programmeerijatel (ja matemaatikutel) võrdlemisi lihtne ette kujutada 4mõõtmelist ruumi, sest 3 mõõtmele saab lisada kergesti järgmise mõõtme sedasi mõõtmeid lisades)  
(aint et sellisel juhul ei saa 4 mõõde enam kasvada ei paremale, alla ega ekraanist välja, vaid peab kuidagi punktikeste sisse edasi arenema, aga ka seda pole raske visualiseerida)  
ja see pole mitte haruldane, et programmeerimises tuleb ette 4mõõtmelisi struktuure  

a-la:

	on N riiki
	igal riigil on M maakonda
	igas maakonnas on L inimest
	igal inimesel on K telefoninumbrit

	for country in countries:
	    for state in country:
	        for person in state:
	            for nr in person.phone_nrs:
	                ....

4mõõtmeline  
kuigi sa ei pea sellele mõtlema kui mõõtmelisele asjale üldse   
lihtsalt see on illustratsiooniks sellele, et mis ekraanil tundub "lame", võib sinu peas olla vägagi mittelame  
(lame=flat siinkohal, mitte labane vms)  
ja see on ka põhjus, mis programmeerimine treenib IQ'd näiteks... lastel eriti
sest ta õpetab peas kujundeid tekitama näiliselt mitte-kujundlikest asjadest
ja kujundlik mõtlemine on teatavasti intellekti alus  
ahv vaatab for-loop'i ja näeb valge ja musta kribukrabu  
laps vaatab, näeb tähti  
täiskasvanu vaatab ja näeb sõnu  
programmeerija vaatab, ja tal tekib peas kujund   

> nii pole see tglt keeruline. eile olin ma pimestatud (ja alati olen) võimalike muude vigade hulgast, sh puuduv konks siin-seal.

see on sinu suhtumise viga juba, et sa endiselt suhtud kõigesse nagu "konksudesse"  
sinu kihlasõrmus võib ka ahvi jaoks lihtsalt konks olla  
a probleem on siiski ahvi mõistmisvõimes, mitte sinu kihlasõrmuse tähenduses
seega kui mingi asi tundub sinu jaoks konks, mida sa ei oska kuhugi panna, siis oleks õige hetk näha konksu taga sõrmust  
ja see eeldab muidugi õppimist ja süüvimist  
seega kui sa ei tea, mis tähendab { ja }, siis kaks järgnevat lõiku on sinu jaoks enamvähem samad:  

	for (...) {
	    a();
	}
	b()

^

	for (...) {
	    a();
	    b();
	}

ja TÄPSELT seesama näide rakendas ennast eile, kui sa ei saanud aru, miks ainult viimane INSERT toimet omab  
sest sa ei teadnud, et } tähendab midagi reaalset  
(kuigi tänu indentimisele on pealt vägagi selgelt näha, et asi on väga erinev, aga küllap sa siis kas ei indentinud või ignoreerisid seda puust-ja-punast infot, mida indent sulle näitas)  

> ma ei teadnud et insertimist saab loopima panna. see on hoopis teine teadmatus.

sa saad ikka aru, et ei PHP'd ega ühtki teist programmeerimiskeelt ei koti, kas mingi lause, mida sa käivitada soovid, on SQL INSERT või echo vms?
mysql_query("INSERT ...");  
echo "tere";  
need on mõlemad PHP jaoks lihtsalt laused  
see, et neist esimene tähendab sinu jaoks SQL INSERTi, on puhas juhus PHP jaoks  
mistõttu kõikidele lausetele kehtivad täpselt samad reeglid, ja täpselt samad võimalused  
kõiki lauseid saab panna for-loop'i sisse ja mitte  
PHP'd ei koti  
kui sa kirjutad:  

	while (true) {
	    mysql_query("INSERT ... INTO my_table");
	}

siis varsti saab tabel täis, ja sellega ka sinu kõvaketas  
ja PHP'd absull ei huvita; tema lihtsalt käivitab seda lauset lõpmatuseni, kuni sa programmi ära katkestad  
...demonstreerimaks, et lause "ma ei teadnud et insertimist saab loopima panna" on absurd  
sest KÕIKE saab looop'ima panna  
ka loop'imist  

	for (...) {
	    for (...) {
	        ...
	    }
	}  

ongi olukord, kus loop'imine on loop'ima pandud  
(vahet pole kas PHP või Python või JS)  
näiteks kui sul on mingi list e. array, ja iga element sellest listist on OMAKORDA array e. list, siis sul ongi vaja loop'i loop'ida  
sest sa tahad käia iga listi selles listis, ja omakorda iga elemendi igas listis  

	lists = [
	    [1, 2, 3],
	    ['whatever', 'blabla'],
	    ['mare', 'opib', 'progema'],
	    ['erik', 'tahab', 'koju'],
	]
	for list in lists:
	    for item in list:
	        print item
	    print "==============="

	1
	2
	3
	======================
	whatever
	blabla
	======================
	mare
	opib
	progema
	======================
	erik
	tahab
	koju
	======================

sellise asja saad ekraanile
ja see on seesama 

	1 2 3 4 5 6 7 8 9
	* * * * * * * * *
	* * *   * * *   *
	* * *   * * *   * 
	* * *       *   * 
	*   *           * 
	    *           *
(juhuslikult lihtsalt kõik tulbad on 3-pikkused, aga ei pea olema)