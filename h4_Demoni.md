# Keskeneräinen

# h4 Demoni

a) [Hello SLS](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#a-hello-sls)

b) [Top](https://github.com/syjaka/Palvelinten-Hallinta-2024/edit/main/h4_Demoni.md#b-top)

c) [Apache easy mode](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#c-apache-easy-mode)

d) [SSHouto](https://github.com/syjaka/Palvelinten-Hallinta-2024/edit/main/h4_Demoni.md#d-sshouto)

e) [Vapaaehtoinen: Apache](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#e-vapaaehtoinen-apache)

f) [Vapaaehtoinen: Caddy](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#f-vapaaehtoinen-caddy)

g) [Vapaaehtoinen: Nginx](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#g-vapaaehtoinen-nginx)

X ) [Lue ja tiivistä](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#x-lue-ja-tiivist%C3%A4)

y) [Käyttöympäristö](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#y-k%C3%A4ytt%C3%B6ymp%C3%A4rist%C3%B6)

z) [Alkutoimet](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#z-alkutoimet)

--- 

Kaikki seuraavien osioiden tehtävänannot ovat peräisin Tero Karvisen - [Infra As a Code - Palvelinten hallinta 2024 kurssisivulta](https://terokarvinen.com/2024/configuration-management-2024-spring/#h4-demoni).

---
## x) Lue ja tiivistä. 

#### 1. Karvinen 2023: [Salt Vagrant - automatically provision one master and two slaves](https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file), vain kohdat
  -  Infra as Code - Your wishes as a text file
      - Luodaan hakemisto Saltin conffille, luodaan ja muokataan Saltin tilatiedosto jonne määritellään file.managed-tila ja sovelletaan luotua tilaa käyttäen Saltia.
  -  top.sls - What Slave Runs What States
    - Top-file on tiedosto joka määrittää mitkä tilat milläkin koneella ajetaan. Tekstissä ensin keskeytetään mahdollinen käynnissä ollut komento. Tämän jälkeen luodaan/muokataan top-file, siten että se ajaa kaikille (`'*'`) Saltin hallinnassa oleville koneille **hello** tilan. Lopuksi *state apply* ajaa top-filessa määritellyt tilat `'*'`-koneille.
#### 2. Salt contributors: [Salt overview](https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml), kohdat
  -  Rules of YAML & Lists and dictionaries - YAML block structures
    - YAML on merkintäkieli jota Saltissa käytetään conffien hallintaan. Siihen liittyy muutamia perusperiaatteita joita ovat mm:
     - Tieto on järjestetty **avain: arvo** pareihin.
     - Kaikki avaimet ovat kirjainkoosta riippuvaisia
     - Sisennyksety tulee tehdä `space`lla, `tab`kielletty. Esim. alla mainitut listat ja dictionaryt ovat jäsennetty sisennyksien avulla, joka on yleensä 2 x `space`.
     - Kommentit merkitään `#`
  -  YAML simple structure - koostuu kolmesta peruselementistä:
      - **Scalars** - Perus avain: arvo -parit
      - **Lists** - Avain jota seuraa luettelo arvoista
      - **Dictonary** - Kokoelma avain:arvo - pareja ja listoja

#### 3. Karvinen 2018: [Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port](https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh)
Artikkelissa esitellään miten SSH-portin vaihtaminen automatisoidaan Salt-tilan avulla. Tekstissä on luotu SSH-tila, joka alkuun varmistaa rttä SSH-server on asennettu. Sen jälkeen se korvaa SSHoletusconf-tiedoston `sshd_config` tiedostolla, jota on muokattu poistamalla kommentti ja vaihtamalla portti 8888. Loppuun määritellään että sshd-palvelun tulee olla käynnissä ja asetetaan `watch`-parametri havaitsemaan m,ahdolliset conf-tiedostoon tehdyt muutokset ja näitä havaitessaan käynnistämään palvelun uudelleen.
Tilan luonnin jälkeen se suoritetaan ja lopputulosta testataan kahdella eri menetelmällä.

#### 4. Silmäile Saltin ohjeet tilafunktioille pkg, file ja service.
  1. Saltin paketinhallintatoiminnot.
     -Salt käyttää `pkg`-tilamoduulia ohjelmistopakettien hallinnassa. Tämän avulla voi mm. määrittää asennettavat, päivitettävät, tai poistettavat ohjelmistot.
     
    $ sudo salt-call --local sys.state_doc pkg # johdanto + silmäile pkg.installed, pkg.purged, pkgs
 
   - `pkg.installed` varmistaa että nimetty paketti on asennettu.
   - `pkg.purged` poistaa asennukset täydellisesti
   - `pkgs` argumentti sallii useamman paketin hallinnan samalla.

  2. Saltin tiedostonhallinnan toiminnot.
        - `file` moduuli nimensä mukaisesti hallinnoi tiedostoja. Tila mahdollistaa mm. tiedostojen lataamisen Salt masterilta kohdekoneille.
    
    $ sudo salt-call --local sys.state_doc file # johdanto + silmäile file.managed, file.absent, file.symlink
    
   - `file.managed` mahdollistaa tiedostojen dynaamisen muokkauksen käyttäen eri mallinnustyökaluja.
   - `file.absent` varmistaa että tietty tiedosto ei ole määritellyssä sijainnissa
   - `file.symlink` luo symbolisen linkin tiedostoon
     
     3. Service moduulin toiminnot
        - Service -tilat mahdollistavat Saltin palveluyiden hallinnan. Sillä voi mm käynnistää, pysäyttää ta tarkistaa tila.

    $ sudo salt-call --local sys.state_doc service # johdanto + silmäile service.running, service.dead, enable

   - `service running` varmistaa nimetyn palvelu käynnissä olemisen
   - `service.dead` on päinvastainen, eli se varmistaa ettei tila ole käynnissä
   - `enable` määrittää tuleeko jokin palvelu käynnistyä automaattisesti järjestelmän käynnistyessä


[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#h4-demoni)

---


## y) Käyttöympäristö
Tehtävä toteutettiin MacBook Retina 12-inch, koneella jossa, host OS on Ventura 13.6.1 käyttöjärjestelmä Suomen maa-asetuksilla ja suomen kielellä. Koneessa on 1,3GHz kaksiytiminen Intel Core i5 prosessori ja 8Gt 1867 MHz LPDDR3 muistia. Näytönohjain on Intel HD Graphics 615 jossa VRAM 1536 Mt.

- Koneeseen asennettu Vagrant versio on 2.4.1.
- z- kohdassa määritetyt virtuaalikoneet ovat Linux Bullseye 5.10.0-28-amd64.

## z) Alkutoimet
Koneen ja pääte-ohjelman käynnistys.
Aloitan tämän tehtävänannon tyhjältä pöydältä. Joten loin ensin virtuaalikoneet k001 ja k002 Vagrantilla kansioon /Vagrant/Demonit komennolla `vagrant up`. Ennen komentoa tallensin demonit-hakemistoon vagrantfilen kuten alla:

    # -*- mode: ruby -*-
    # vi: set ft=ruby :
    # Lahde josta muokattu /copyright 2019-2021 Tero Karvinen http://TeroKarvinen.com
    
    $tscript = <<TSCRIPT
    set -o verbose
    apt-get update
    apt-get -y install ufw curl netcat micro bash-completion
    # echo "export EDITOR='micro'" >> /etc/bash.bashrc
    
    
    echo "valmista"
    TSCRIPT 
    
    
    Vagrant.configure("2") do |config|
    	config.vm.synced_folder ".", "/vagrant", disabled: true
  
    	config.vm.provision "shell", inline: $tscript
    	config.vm.box = "debian/bullseye64"
    
    	config.vm.define "k001" do |k001|
    		k001.vm.hostname = "k001"
    		k001.vm.network "private_network", ip: "192.168.88.101"
    	end
    
    	config.vm.define "k002", primary: true do |k002|
    		k002.vm.hostname = "k002"
    		k002.vm.network "private_network", ip: "192.168.88.102"
    	end
    	
    end
    
Koneiden luonnin jälkeen jälkeen asensin niille ensin palomuurit aukkoineen toimintaan komennoilla:
              
    sudo ufw allow 22,80,4505,4506/tcp
    sudo ufw enable
    sudo systemctl restart ufw
    
Seuraavaksi  asensin Saltin (minion koneelle k002 ja master koneelle k001) seuraten tehtävärapsani h2_Soitto_kotiin [- Kaksi vituaalikonetta samassa verkossa - ](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h2_Soitto_kotiin.md#b-asenna-saltin-herra-orja-arkkitehtuuri-toimimaan-verkon-yli---08042024-klo-1345---1420-eet) steppejä.

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#h4-demoni)

---

## a) Hello SLS! 
Tehtävän suoritus 19.04.2024 klo 11.28 - 14.52 EET.
Tee Hei maailma -tila kirjoittamalla se tekstitiedostoon, esim /srv/salt/hello/init.sls (Karvinen 2024). 

1. Loin uuden kansion **hello** polkuun `master$ sudo mkdir /srv/salt/hello/` ja siirryin sinne.
2. Loin **hello* halkemistoon tiedoston init.sls
  !h4-001
3. Testasin luotua tilaa `master$ sudo salt '*' state.apply hello` ja sain virheen.
  !h4-002
   - Tarkistin ensin että yhteys varmasti on kunnossa
     !h4-003
   - Poistin `#` kommentoinnin `sudoedit /etc/saslt/master` - tiedoston **file_roots**-kohdasta jotta varmistan oikean hakemiston käytön - ei auttanut eli sama herja jatkuu.
   - Tarkistin kaikki oikeudet, että miniuonilla on pääsy tiedostoon ja ne on kunnossa.
   - Tarkistin että polku on varmasti oikea.
     !h4-004
   - Testasin onnistuuko tiedoston luonti suoralla komennolla `master$ sudo salt '*' state.single file.managed '/tmp/network-broblem-solving`. Tämä jäi kellottamaan pitkäksi aikaa joka viitta yhteysongelmiin.
   - Keskeytin suorituksen `ctrl c` ja käynnistin molemmat uudelleen `minion$ sudo systemctl restart salt-minion`/`master$ sudo systemctl restart salt-master` ja tarkistin lokin `master$ sudo tail -f /var/log/salt/master` ja `minion$ sudo tail -f /var/log/salt/minion`
    
         2024-04-19 09:56:42,004 [salt.utils.parsers:1104][WARNING ][10684] Master received a SIGTERM. Exiting. #Masterin
         2024-04-19 09:56:30,569 [salt.utils.parsers:1104][WARNING ][4274] Minion received a SIGTERM. Exiting.. #Minionin
   - Näissä ei ollut mitään muita tapahtumia kuin uudelleenkäynnistys. Tarkastin että molemmat ovat varmasti käynnissä:
    !h4-005
    !h4-006
   - Pingasin uudelleen ja minion vastaa. Pitkällisen googlettelun ja ratkaisunetsinnän jälkeen oivalsin että isäntäkoneen toisessa hakemistossa on samannimiset koneet, poistin kaikiken ja aloitin alusta.
   - Suoritin uudelleen virtuaalikoneiden luonnin ja saltin asennuksen kuten yllä. Tällä kertaa nimesin koneet doh001 ja doh002. Uudelleentehdessä huomasin virheeni. Olin luonut polun **/srv/salt/hello/** manuaalisti askel kerrallaan **/home/vagrant** hakemistoon juuren sijasta. Uusi asennus auttoi ja luotu tila toimi.
4. Testin suoritin uudelleen komennolla `master$ sudo salt '*' state.apply hello` ja nyt sasin toivotun vastauksen.
   !h4-007

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#h4-demoni)

---

## b) Top. 
Tehtävän suoritus 19.04.2024 klo 14.54 - 15.47
Tee top.sls niin, että useita valitsemiasi tiloja ajetaan automaattisesti, esim komennolla "sudo salt '*' state.apply" tai "sudo salt-call --local state.apply" (Karvinen 2024). 

1. Tein ensin tilat samoin kuin yllä **hello**-tilan.
   - Favorites ohjelmat
   - Luo käyttäjä tilan
   - 
2. Loin topfilen jonne määritelin nämä kaksi sekä aiemmin luodun **hello*n. Nyt /srv/salt hakemisto sisältöineen on kuten kuvassa.
   !h4-008
3.  Ajoin luodut tilat topfilen avulla käyttäen komentoa `sudo salt '*' state.apply`
    - Lopputuloksena onnistunut ajo
      !h4-009
      !h4-010
      (lempparit muutokset ei kyvassa pituutensa vuoksi)
    - Kokeilin vielä muokattuna komentoa niin että se näyttää mitä tapahtuu ja että lopputulos olisi lyhyempi `sudo salt '*' state.apply -l info --state-output=terse`. Nyt tietenkin kun muutoksia ei tehty, ei toiminnotkaan tulostu.
      !h4-011
       
[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#h4-demoni)

---

## c) Apache easy mode. 
Tehtävän suoritus 19.04.2024 klo 16.00 - 18.32 ja 19.00 - 19-27 EET. Tehtävän suoritin kokonaan salt Masterilla.
Asenna Apache, korvaa sen testisivu ja varmista, että demoni käynnistyy.
Ensin käsin, vasta sitten automaattisesti.
Kirjoita tila sls-tiedostoon.
pkg-file-service
Tässä ei tarvita service:ssä watch, koska index.html ei ole asetustiedosto (Karvinen 2024)

1. Alkuun asensin käsin
   - Alkutilanne osoittaa että apache ei ole asennettu:
     !h4-016
   - `sudo apt-get install apache2` asensi apachen
   - Alussa olin jo aukottanut palomuurin, joten se ei ole nyt tarpeen.
   - Korvasin defaultsivun sisällön `echo "Default"|sudo tee /var/www/html/index.html`ja testasin että apache vastaa.
     !h4-014
   - `mkdir -p /home/vagrant/publicsites/testisivu.example.com/` loi testisivulle hakemiston
   - `echo tämä on testisivu > /home/vagrant/publicsites/testisivu.example.com/index.html` loi tiedoston **index.html** jonne sivun sisältö "tämä on testisivu" tallennetaan.
      !h4-012
   - `sudoedit /etc/apache2/sites-available/testisivu.example.com.conf`luo conf-tiedoston joka ohjaa verkkokyselyt äsken luotuun sisältöön
      !h4-013
   - Nyt saatavilla oli vain defaultsivu. Poistin sen käytöstä `sudo a2dissite 000-default.conf` ja otin luomani confin käyttöön `sudo a2ensite testisivu.example.com.conf`
   - Potkaisin apachen uudelleen käyntiin jotta muutokset tulee voimaan `sudo systemctl restart apache2`.
   - `curl localhost` toi testisivu.example.com hakemistoon luodun index.html-sivun näkyviin.
   - Apachen poisto komennolla `sudo apt-get purge apache2` ja testisivu hakemisto komennolla `rm -r testisivu.example.com/` suoritettuna publicsites hakemistossa
      !h4-015

2. Seuraavaksi automatisoin saman
   - **/srv/salt/** hakemistoon uusi hakemisto `sudo mkdir apache` ja sinne `sudoedit init.sls`
   - Testasin ensin että tämä vastaa **Hello worldillä** luomalla lyhyen file.managed tilan.
   - `sudo salt-call --local -l info state.apply apache`komentoon apache-tila vastasi onnistuneella suorituksella.
     !h4-017 
   - Koska edellisessä tehtävässä olin poistanut kaikki apachen määritykset, loin uuden conf-tiedoston kadi.conf ja hakemiston sivuston sisällölle.

         vagrant@doh001:/etc/apache2/sites-available$ cat kadi.conf 
         <VirtualHost *:80>
              DocumentRoot /home/vagrant/publicsites/kadi/
              <Directory /home/vagrant/publicsites/kadi/>
                  Require all granted
              </Directory>
          </VirtualHost>
      ja

          vagrant@doh001:/etc/apache2/sites-available$ cd
          vagrant@doh001:~$ ls
          publicsites  shared
          vagrant@doh001:~$ cd publicsites/
          vagrant@doh001:~/publicsites$ mkdir kadi
      
     
   - vaihdoin tilan sisällöksi ao. Tätä init-tiedostoa muokatessa testasin joka lisäyksen jälkeen, että toimii.


          apache2:
            pkg.installed
          
          /etc/apache2/sites-available/kadi.conf:
            file.managed:
              - source: "salt://apache/kadi.conf"
         /etc/apache2/sites-enabled/000-default.conf:
            file.absent
              
         /etc/apache2/sites-enabled/kadi.conf:
            file.symlink:
              -target: "/etc/apache2/sites-enabled/kadi.conf"
            
          apache2.service:
            service.running
  
     (Salt man)
             
     - Loppuun poistin apachen `sudo apt-get purge apache2` ja suoritin `sudo salt-call --local -l info --state-output=terse state.apply apache`
     - !h4-018
  

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#h4-demoni)

---

## d) SSHouto. 
Tehtävän suoritus 19.04.2024 klo 19.30 - 20.08 EET.
Lisää uusi portti, jossa SSHd kuuntelee.
Jos käytät Vagrantia, muista jättää portti 22/tcp auki - se on oma yhteytesi koneeseen. SSHd:n asetustiedostoon voi tehdä yksinkertaisesti kaksi "Port" riviä, molemmat portit avataan.
Löydät oikean asetuksen katsomalla SSH:n asetustiedostoa
Nyt tarvitaan service-watch, jotta demoni käynnistetään uudelleen, jos asetustiedosto muuttuu masterilla

1. sshd_config tiedoston luonti
   - Kopioin sshd conf-tiedoston `sudo cp /etc/ssh/sshd_config /srv/salt/sshd/sshd_config`.
   - Poistin portista kommentoinnin ja lisäsin uuden portin
     !h4-019
     
3. SSH-tilan luonti
   - /srv/salt hakemistossa `micro sshd.sls` ja sinne tallensin:

         openssh-server:
           pkg.installed
         /etc/ssh/sshd_config:
           file.managed:
             - source: salt://sshd_config
         sshd:
           service.running:
             - watch:
               - file: /etc/ssh/sshd_config
   - `sudo salt '*' state.apply sshd -l info --state-output=terse`suoritti onnistuneen ajon. Itse ssh oli jo asennettu alkutoimien kohdalla.
     !h4-020
4. Testi
   - `nc -vz 192.168.88.102 8888` komento antoi onnistuneen palautteen
     !h4-021


[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#h4-demoni)

---

## e) Vapaaehtoinen: Apache. 
Asenna Apache tarjoilemaan weppisivua. Weppisivun tulee näkyä palvelimen etusivulla (localhost). HTML:n tulee olla jonkun käyttäjän kotihakemistossa, ja olla muokattavissa normaalin käyttäjän oikeuksin, ilman sudoa.

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#h4-demoni)

---

## f) Vapaaehtoinen: Caddy. 
Asenna Caddy tarjoilemaan weppisivua. Weppisivun tulee näkyä palvelimen etusivulla (localhost). HTML:n tulee olla jonkun käyttäjän kotihakemistossa, ja olla muokattavissa normaalin käyttäjän oikeuksin, ilman sudoa.

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#h4-demoni)

---

## g) Vapaaehtoinen: Nginx. 
Asenna Nginx (lausutaan engine-X) tarjoilemaan weppisivua. Weppisivun tulee näkyä palvelimen etusivulla (localhost). HTML:n tulee olla jonkun käyttäjän kotihakemistossa, ja olla muokattavissa normaalin käyttäjän oikeuksin, ilman sudoa.

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#h4-demoni)

---

## Lähteet: 

Karvinen T. 2024, Infra as Code - Palvelinten hallinta 2024. Luettavissa: https://terokarvinen.com/2024/configuration-management-2024-spring/#h4-demoni. Luettu 18.04.2024

Karvinen T. 2018, Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port. Luettavissa: https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh. Luettu 18.04.2024.

Karvinen T. 2023, Salt Vagrant - automatically provision one master and two slaves. Luettavissa: https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file. Luettu 18.04.2024

Salt Contributors 2024, Salt Overviev. Luettavissa: https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml.mLuettu 18.04.2024

Salt user guides, States 2024. Luettavissa: https://docs.saltproject.io/salt/user-guide/en/latest/topics/states.html. Luettu 19.04.2024

<VirtualHost *:80>
    DocumentRoot /home/vagrant/publicsites/testisivu.example.com/
    <Directory /home/vagrant/publicsites/testisivu.example.com/>
        Require all granted
    </Directory>
</VirtualHost>

 
