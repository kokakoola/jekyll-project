---
layout : blog
title : Hartl Rails Tutorial
category : how-to
tags : [tools, sublime, editor]
description : sublime text usage
comments : true
lang : estonian
excerpt : Hartli Railsi tutorial on konkreetse projekti läbiviimine lihtsamast keerukamaks. 
---

### 1. Algus

Tekstieditoriks Sublime Text 2 - neo-TextMate.
Terminaliks vaikimisi Terminal
Brauser Chrome või Firefox

kontrolli, milline Ruby Sul masinas on:

    $ ruby -v

Ilmselt on sul tarvis paigaldada uus Ruby 1.9.3. Selleks on hea tööriist rvm: Ruby Version Manager, mis võimaldab mitut Ruby versiooni masinas jooksutada ja erinevaid gemide bundleid vastavalt projektile. Kui rvm on olemas, paigalda ruby: 

    $ rvm get head && rvm reload
    $ rvm install 1.9.3

Kui rvm ja ruby olemas, saad projektipõhise seti Rubyst-gemidest teha:

    $ rvm use 1.9.3@projektinimi --create --default

`--create` teeb gemseti nimega projektinimi 
`--default` seab versiooni ja gemseti vaikimisi versioonideks

rvm abi on  

    $ rvm --help
    $ rvm gemset --help

#### Installi Gemid

Tegelikult on need sul rvm-iga automaatselt juba kaasas. Vt `$ which gem`

5.3 osa: scss nesting ja muutujad. cool! kuidas ma seni ilma sain? scss-i võlu on, et pmst võid ka tavalist css-i kirjutada. 

aga võid ka värvi defineerida faili alguses $white ja sisse kirjutada #fff asemele $white.

või ühe tagi css-i ära nestida nt h2 ja h2:hover lähevad ühte skoopi, : asemel on &.

Millist preprotsessorit kasutada, saab Rails ise aru failinime järgi (.scss, .coffee, .erb), pmst seda ei märkagi et ta vahepeal midagi kompileerib.
 CoffeScripti kohta vaata [siit](http://railscasts.com/episodes/267-coffeescript-basics)

ja bootstrap-sassi gem võimaldab ilma mingi lisatsirkuseta [lessi muutujaid](http://bootstrapdocs.com/v2.0.4/docs/less.html) kasutada. lisaks Sprockets gem pakib cssi/javascripti serveri jaoks üheks failiks automaatselt (selleks juhendi annab manifest file assets/stylesheets cssi jaoks)


guard on käsk rspeci käivitamiseks.

> Peale kuud railsita on mu mälu hämar. Luban, et konpekteerin edaspidi  

Hämarusest välja tippisin sisse `spork`. See käivitas testivalvuri. Teine tab ja seal peal `guard` jooksutab rspeci mil iganes salvestad.

Nüüd roogime me välja kõik hard-coded pathid ja asendame need pathidega. Algatuseks testis (spec/requests/static_pages_spec.rb):

    visit '/static_pages/help'

saab olema 

    visit help_path

test feilib nagu oodatud. Nüüd parandame teekonnad failis config/routes.rb:

    get 'static_pages/help'

saab olema

    match '/help', to: 'static_pages#help'

index, mis on publicus tuleb ära visata, et rails ei renderdaks default lehte. Et kasutusel on git, tuleb kasutada käsku `git rm public/index.html`.  
Ja tulemus on muidugi, et test feilib endiselt - kuigi peaks toimima nüüd. 

### 15.01 
Ha-ha-haa, vaat kus nali! Muidugi töötab test täna ilusti, kuigi vahepeal pole midagi muudetud. 
Muide, piisab guardi sissetippimisest, et automaattestid käima läheks. MA ei tea enam, mis see spork oli. Küll selgub.

Täna kirjutasin abifaili spec/support/utilities.rb, mis koondab endasse korduvad testiosad:

    def full_title(page_title)
      base_title = "Ruby on Rails Tutorial Sample App"
      if page_title.empty?
        base_title
      else
        "#{base_title} | #{page_title}"
      end
    end

Testi saab nüüd poole lihtsamaks, nt Home page test:

    subject { page }

      describe "Home page" do
        before { visit root_path } 

        it { should have_selector('h1',    text: 'Sample App') }
        it { should have_selector('title', text: full_title('')) }
    end


### User signup

1. Teeme kontrolleri (nagu omal ajal staatilistele lehtedele):

    $ rails generate controller Users new --no-test-framework

mis teeb meile automaatselt valmis mitu tarvilikku faili - nt on nüüd olemas töötav leht aadressil users/new. Me tahame aadressiks /signup.

Kõigepealt aga kirjutame testi - nagu Harltlil kombeks on:

    $ rails generate integration_test user_pages

ja parandame dummy-sisu enda vajadustele vastavaks. Failis spec/requests/user_pages_spec.rb:  

    require 'spec_helper'

    describe "User pages" do

      subject { page }

      describe "signup page" do
        before { visit signup_path }

        it { should have_selector('h1',    text: 'Sign up') }
        it { should have_selector('title', text: full_title('Sign up')) }
      end
    end

Guard vajab restarti vahepeal kui pathide-routide kallale minnakse. Test feilib peale seda nagu vaja. Meil tuleb lisada õige route ja view sisu:

config/routes.rb-sse lisame `match '/signup', to: 'users#new'`

ja app/views/users/new.html.erb-sse lisame/muudame 

    <% provide(:title, 'Sign up') %>
    <h1>Sign up</h1>

Test PEAKS toimima. Nojah.

Singup lehe linkimine failis app/views/static_pages/home.html.erb

asendame # signup_path-iga: `<%= link_to "Sign up now!", signup_path, class: "btn btn-large btn-primary" %>`








