# h4 Demoni

a) [Hello SLS](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#a-hello-sls)

b) [Top](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#b-top)

c) [Apache easy mode](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#c-apache-easy-mode)

d) [SSHouto](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#d-sshouto)

e) [Vapaaehtoinen: Apache](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#e-vapaaehtoinen-apache)

f) [Vapaaehtoinen: Caddy](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#f-vapaaehtoinen-caddy) - Keskeneräinen

g) [Vapaaehtoinen: Nginx](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#g-vapaaehtoinen-nginx) - Keskeneräinen

X ) [Lue ja tiivistä](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#x-lue-ja-tiivist%C3%A4)

y) [Käyttöympäristö](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#y-k%C3%A4ytt%C3%B6ymp%C3%A4rist%C3%B6)

z) [Alkutoimet](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#z-alkutoimet)

--- 

Kaikki seuraavien osioiden tehtävänannot ovat peräisin Tero Karvisen - [Infra As a Code - Palvelinten hallinta 2024 kurssisivulta](https://terokarvinen.com/2024/configuration-management-2024-spring/#h4-demoni).

---
## x) Lue ja tiivistä. 

#### 1. Karvinen 2023: [Salt Vagrant - automatically provision one master and two slaves](https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file), vain kohdat:
  -  Infra as Code - Your wishes as a text file
      - Luodaan hakemisto Saltin conffille, luodaan ja muokataan Saltin tilatiedosto jonne määritellään file.managed-tila ja sovelletaan luotua tilaa käyttäen Saltia.
  -  top.sls - What Slave Runs What States
    - Top-file on tiedosto joka määrittää mitkä tilat milläkin koneella ajetaan. Tekstissä ensin keskeytetään mahdollinen käynnissä ollut komento. Tämän jälkeen luodaan/muokataan top-file, siten että se ajaa kaikille (`'*'`) Saltin hallinnassa oleville koneille **hello** tilan. Lopuksi *state apply* ajaa top-filessa määritellyt tilat `'*'`-koneille.
#### 2. Salt contributors: [Salt overview](https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml), kohdat:
  -  Rules of YAML & Lists and dictionaries - YAML block structures
    - YAML on merkintäkieli jota Saltissa käytetään conffien hallintaan. Siihen liittyy muutamia perusperiaatteita joita ovat mm:
     - Tieto on järjestetty **avain: arvo** pareihin.
     - Kaikki avaimet ovat kirjainkoosta riippuvaisia
     - Sisennykset tulee tehdä `space`lla, `tab` kielletty. Esim. alla mainitut listat ja dictionaryt ovat jäsennetty sisennyksien avulla, joka on yleensä 2 x `space`.
     - Kommentit merkitään `#`
  -  YAML simple structure - koostuu kolmesta peruselementistä:
      - **Scalars** - Perus avain: arvo -parit
      - **Lists** - Avain jota seuraa luettelo arvoista
      - **Dictonary** - Kokoelma avain:arvo - pareja ja listoja

#### 3. Karvinen 2018: [Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port](https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh)
Artikkelissa esitellään miten SSH-portin vaihtaminen automatisoidaan Salt-tilan avulla. Tekstissä on luotu SSH-tila, joka alkuun varmistaa että SSH-server on asennettu. Sen jälkeen se korvaa SSH oletusconf-tiedoston `sshd_config` tiedostolla, jota on muokattu poistamalla kommentti ja vaihtamalla portti 8888. Loppuun määritellään että sshd-palvelun tulee olla käynnissä ja asetetaan `watch`-parametri havaitsemaan mahdolliset conf-tiedostoon tehdyt muutokset ja näitä havaitessaan käynnistämään palvelun uudelleen.
Tilan luonnin jälkeen se suoritetaan ja lopputulosta testataan kahdella eri menetelmällä.

#### 4. Silmäile Saltin ohjeet tilafunktioille pkg, file ja service.
  1. Saltin paketinhallintatoiminnot.
     -Salt käyttää `pkg`-tilamoduulia ohjelmistopakettien hallinnassa. Tämän avulla voi mm. määrittää asennettavat, päivitettävät, tai poistettavat ohjelmistot.
     
    $ sudo salt-call --local sys.state_doc pkg # johdanto + silmäile pkg.installed, pkg.purged, pkgs
 
   - `pkg.installed` varmistaa että nimetty paketti on asennettu.
   - `pkg.purged` poistaa asennukset täydellisesti.
   - `pkgs` argumentti sallii useamman paketin hallinnan samalla.

  2. Saltin tiedostonhallinnan toiminnot.
        - `file` moduuli nimensä mukaisesti hallinnoi tiedostoja. Tila mahdollistaa mm. tiedostojen lataamisen Salt masterilta kohdekoneille.
    
    $ sudo salt-call --local sys.state_doc file # johdanto + silmäile file.managed, file.absent, file.symlink
    
   - `file.managed` mahdollistaa tiedostojen dynaamisen muokkauksen käyttäen eri mallinnustyökaluja.
   - `file.absent` varmistaa että tietty tiedosto ei ole määritellyssä sijainnissa
   - `file.symlink` luo symbolisen linkin tiedostoon
     
  3. Service moduulin toiminnot
        - Service -tilat mahdollistavat Saltin palveluiden hallinnan. Sillä voi mm. käynnistää, pysäyttää ta tarkistaa tila.

    $ sudo salt-call --local sys.state_doc service # johdanto + silmäile service.running, service.dead, enable

   - `service running` varmistaa nimetyn palvelu käynnissä olemisen.
   - `service.dead` on päinvastainen, eli se varmistaa ettei palvelu ole käynnissä.
   - `enable` määrittää tuleeko jokin palvelu käynnistyä automaattisesti järjestelmän käynnistyessä.


[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#h4-demoni)

---


## y) Käyttöympäristö
Tehtävä toteutettiin MacBook Retina 12-inch, koneella jossa, host OS on Ventura 13.6.1 käyttöjärjestelmä Suomen maa-asetuksilla ja suomen kielellä. Koneessa on 1,3GHz kaksiytiminen Intel Core i5 prosessori ja 8Gt 1867 MHz LPDDR3 muistia. Näytönohjain on Intel HD Graphics 615 jossa VRAM 1536 Mt.

- Koneeseen asennettu Vagrant versio on 2.4.1.
- z- kohdassa määritetyt virtuaalikoneet ovat Linux Bullseye 5.10.0-28-amd64.

## z) Alkutoimet
Koneen ja pääte-ohjelman käynnistys.

Aloitan tämän tehtävänannon tyhjältä pöydältä. Loin ensin virtuaalikoneet k001 ja k002 Vagrantilla kansioon /Vagrant/Demonit komennolla `vagrant up`. 
Ennen komentoa tallensin demonit-hakemistoon vagrantfilen kuten alla:

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

Kaikkien tehtävien suorituksissa on käytetty lähteenä Karvisen 18.04 luentoa sekä yllä tiivistettyjä tekstejä. Muut lähteet ovat merkitty tekstiin.

--- 

## a) Hello SLS! 
Tehtävän suoritus 19.04.2024 klo 11.28 - 14.52 EET.
Tee Hei maailma -tila kirjoittamalla se tekstitiedostoon, esim /srv/salt/hello/init.sls (Karvinen 2024). 

1. Loin uuden kansion **hello** polkuun `master$ sudo mkdir /srv/salt/hello/` ja siirryin sinne.
2. Loin **hello* halkemistoon tiedoston init.sls.
  ![h4-001](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-001.png)
3. Testasin luotua tilaa `master$ sudo salt '*' state.apply hello` ja sain virheen.
  ![h4-002](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-002.png)
   - Tarkistin ensin että yhteys varmasti on kunnossa.
     ![h4-003](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-003.png)
   - Poistin `#` kommentoinnin `sudoedit /etc/saslt/master` - tiedoston **file_roots**-kohdasta jotta varmistan oikean hakemiston käytön - ei auttanut eli sama herja jatkui.
   - Tarkistin kaikki oikeudet, että minionilla on päädsy tiedostoon ja ne on kunnossa.
   - Tarkistin että polku on varmasti oikea.
     ![h4-004](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-004.png)
   - Testasin onnistuuko tiedoston luonti suoralla komennolla `master$ sudo salt '*' state.single file.managed '/tmp/network-broblem-solving`. Tämä jäi kellottamaan pitkäksi aikaa joka viittasi yhteysongelmiin.
   - Keskeytin suorituksen `ctrl c` ja käynnistin molemmat koneet uudelleen `minion$ sudo systemctl restart salt-minion`/`master$ sudo systemctl restart salt-master` ja tarkistin lokin `master$ sudo tail -f /var/log/salt/master` ja `minion$ sudo tail -f /var/log/salt/minion`
    
         2024-04-19 09:56:42,004 [salt.utils.parsers:1104][WARNING ][10684] Master received a SIGTERM. Exiting. #Masterin
         2024-04-19 09:56:30,569 [salt.utils.parsers:1104][WARNING ][4274] Minion received a SIGTERM. Exiting.. #Minionin
   - Lokeissa ei ollut mitään muita tapahtumia kuin uudelleenkäynnistys. Tarkastin että molemmat ovat varmasti käynnissä:
    ![h4-005](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-005.png)
    ![h4-006](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-006.png)
   - Pingasin uudelleen ja minion vastasi. Pitkällisen googlettelun ja ratkaisunetsinnän jälkeen oivalsin, että isäntäkoneeni toisessa hakemistossa oli jo samannimiset koneet aiempien harjoitusten jäljiltä, poistin kaikiken ja aloitin alusta.
   - Suoritin uudelleen virtuaalikoneiden luonnin ja saltin asennuksen kuten yllä. Tällä kertaa nimesin koneet doh001 ja doh002. Uudelleentehdessä huomasin toisen ongelmia aiheuttaneen virheeni. Olin luonut polun **/srv/salt/hello/** manuaalisti askel kerrallaan **/home/vagrant** hakemistoon juuren sijasta. Uusi asennus auttoi ja luotu tila toimi.
4. Testin suoritin uudelleen komennolla `master$ sudo salt '*' state.apply hello` ja nyt sain toivotun vastauksen.
   ![h4-007](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-007.png)

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#h4-demoni)

---

## b) Top. 
Tehtävän suoritus 19.04.2024 klo 14.54 - 15.47
Tee top.sls niin, että useita valitsemiasi tiloja ajetaan automaattisesti, esim komennolla "sudo salt '*' state.apply" tai "sudo salt-call --local state.apply" (Karvinen 2024). 

1. Tein ensin tilat, samoin kuin yllä  tehdyn **hello**-tilan.
   - Favorites ohjelmat
   - Luo käyttäjä tilan
   - 
2. Loin topfilen jonne määritelin nämä kaksi, sekä aiemmin luodun **hello**n. Nyt /srv/salt hakemisto sisältöineen oli kuten kuvassa.
   ![h4-008](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-008.png)
3.  Ajoin luodut tilat topfilen avulla käyttäen komentoa `sudo salt '*' state.apply`
    - Lopputuloksena onnistunut ajo
      ![h4-009](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-009.png)
      ![h4-010](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-010.png)
      (lempparit muutokset ei kuvassa pituutensa vuoksi)
    - Kokeilin vielä muokattuna komentoa niin, että se näyttää mitä tapahtuu ja niin, että lopputulos olisi lyhyempi `sudo salt '*' state.apply -l info --state-output=terse`. Nyt tietenkin, kun muutoksia ei tehty, ei toiminnotkaan tulostu.
      ![h4-011](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-011.png)
       
[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#h4-demoni)

---

## c) Apache easy mode. 
Tehtävän suoritus 19.04.2024 klo 16.00 - 18.32 ja 19.00 - 19-27 EET. Tehtävän suoritin kokonaan salt Masterilla.
Asenna Apache, korvaa sen testisivu ja varmista, että demoni käynnistyy.
Ensin käsin, vasta sitten automaattisesti.
Kirjoita tila sls-tiedostoon.
pkg-file-service
Tässä ei tarvita service:ssä watch, koska index.html ei ole asetustiedosto (Karvinen 2024)

1. Alkuun asensin käsin.
   - Alkutilanne osoitti että apache ei ole asennettu:
     ![h4-016](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-016.png)
   - `sudo apt-get install apache2` asensi apachen.
   - Alussa olin jo aukottanut palomuurin, joten se ei ollut nyt tarpeen.
   - Korvasin defaultsivun sisällön `echo "Default"|sudo tee /var/www/html/index.html` ja testasin että apache vastaa.
     ![h4-014](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-014.png)
   - `mkdir -p /home/vagrant/publicsites/testisivu.example.com/` loi testisivulle hakemiston.
   - `echo tämä on testisivu > /home/vagrant/publicsites/testisivu.example.com/index.html` loi tiedoston **index.html** jonne tallentui sivun sisältö "tämä on testisivu".
      ![h4-012](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-012.png)
   - `sudoedit /etc/apache2/sites-available/testisivu.example.com.conf` luo conf-tiedoston, joka ohjaa verkkokyselyt äsken luotuun sisältöön.
      ![h4-013](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-013.png)
   - Nyt saatavilla oli vain defaultsivu. Poistin sen käytöstä `sudo a2dissite 000-default.conf` ja otin luomani confin käyttöön `sudo a2ensite testisivu.example.com.conf`.
   - Potkaisin apachen uudelleen käyntiin jotta muutokset tulee voimaan `sudo systemctl restart apache2`.
   - `curl localhost` toi testisivu.example.com hakemistoon luodun index.html-sivun näkyviin.
     ![h4-015](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-015.png)
   - Apachen poisto komennolla `sudo apt-get purge apache2` ja testisivu hakemisto komennolla `rm -r testisivu.example.com/` suoritettuna publicsites hakemistossa.


2. Seuraavaksi automatisoin saman
   - Loin **/srv/salt/** hakemistoon uuden hakemiston `sudo mkdir apache` ja sinne `sudoedit init.sls`.
   - Testasin ensin, että tämä vastaa **Hello worldillä**, luomalla lyhyen file.managed tilan.
   - Komentoon `sudo salt-call --local -l info state.apply apache` apache-tila vastasi onnistuneella suorituksella.
     ![h4-017](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-017.png) 
   - Koska edellisessä tehtävässä olin poistanut apachen määritykset, loin uuden conf-tiedoston kadi.conf ja hakemiston sivuston sisällölle.

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
      
     
   - Vaihdoin tilan sisällöksi ao. Tätä init-tiedostoa muokatessa testasin joka lisäyksen jälkeen, että toimii.


          apache2:
            pkg.installed
          
          /etc/apache2/sites-available/kadi.conf:
            file.managed:
              - source: "salt://apache/kadi.conf"
         /etc/apache2/sites-enabled/000-default.conf:
            file.absent
              
         /etc/apache2/sites-enabled/kadi.conf:
            file.symlink:
              -target: "/etc/apache2/sites-available/kadi.conf"
            
          apache2.service:
            service.running
  
     (Salt man)
             
     - Loppuun poistin apachen `sudo apt-get purge apache2` ja suoritin `sudo salt-call --local -l info --state-output=terse state.apply apache`, joka onnistui.
     - ![h4-018](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-018.png)
  

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
     ![h4-019](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-019.png)
     
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
   - `sudo salt '*' state.apply sshd -l info --state-output=terse` suoritti onnistuneen ajon. Itse ssh oli jo asennettu alkutoimien kohdalla.
     
     ![h4-020](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-020.png)
4. Testi
   - `nc -vz 192.168.88.102 8888` komento antoi onnistuneen palautteen.
     ![h4-021](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-021.png)


[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#h4-demoni)

---

## e) Vapaaehtoinen: Apache. 
Tehtävän suoritus 19.04.2024 klo 20.15 - 22.15 ja 23.04 klo 9.30 - 12.00.

Asenna Apache tarjoilemaan weppisivua. Weppisivun tulee näkyä palvelimen etusivulla (localhost). HTML:n tulee olla jonkun käyttäjän kotihakemistossa, ja olla muokattavissa normaalin käyttäjän oikeuksin, ilman sudoa.

Jatkoin osion **c** automatisoinnin pohjalta, eli ryhdyin muokkaamaan apachen hakemistossa sijaitsevaa init-tiedostoa.
  Tavoitteena oli luoda sinne tilat jotka luovat polun /home/vagrant/**publicfiles/kadi** ja sinne **index.html** tiedoston. Tämän lisäksi nämä tulee olla tavallisen käyttäjän muokattavisaa, eli oikeuksia piti säätää. Käytän lähteenä salt- manualia.
   
1. Ensiksi lisäsin index.html tiedoston luonnin **apache2*-tilaan
  
        /home/vagrant/publicsites/kadi/index.html:
          file.managed:
            - source: "salt://apache/index.html"
   
   Testasin `sudo salt-call --local -l info --state-output=terse state.apply apache`

   ![h4-022](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-022.png) 
2. Seuraavaksi sallin kansiorakenteen luonnin tiedostonluonnin yhteydessä lisäämällä äsken lisättyyn.

        /home/vagrant/publicsites/kadi/index.html:
          file.managed:
            - source: "salt://apache/index.html"
            - makedirs: True
   Testasin `sudo salt-call --local -l info --state-output=terse state.apply apache`
    ![h4-023](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-023.png) 
5. Seuraavaksi määritin kansiorakenteen ja tiedoston käyttäjäksi tavallisen käyttäjän. Sitä varten muokkasin aiemmin b-osiossa luotua **user** tilaa seuraavasti:

       create_group:
         group.present:
           - name: basic_group
      
       create_user:
         user.present:
            - name: basic_user
            - password: ############ Tämä piti generoida erikseen komennolla **openssl passwd -1 "salasana"**
            - gid: basic_group
            - shell: /bin/bash
            - home: /home/basic_user
   
   Lisäksi lisäsin, **apache2** tilaan file.managed toimintoon, määrityksen käyttäjälle:
   
        /home/vagrant/publicsites/kadi/index.html:
          file.managed:
            - source: "salt://apache/index.html"
            - makdirs: True
            - user: basic_user
            - group: basic_group
            - mode: 644
   Nyt piti myös **topfile** päivittää ja ajaa tila sen kautta.
   ![h4-024](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-024.png)
   ![h4-025](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-025.png)
6. Lopputuloksena onnistunut suoritus mutta **publicsites/kadi** ovat yhä rootin omistuksessa
   ![h4-026](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-026.png)
7. Muutin **apache** tilaa siten että hakemisto määritellään erikseen. Nyt koko **tila** näytti tältä:

       apache2:
          pkg.installed
        
       /etc/apache2/sites-available/kadi.conf:
          file.managed:
            - source: "salt://apache/kadi.conf"
        
       /etc/apache2/sites-enabled/000-default.conf:
          file.absent
            
       /etc/apache2/sites-enabled/kadi.conf:
          file.symlink:
            - target: "/etc/apache2/sites-enabled/kadi.conf"
        
       /home/vagrant/publicsites/kadi:
          file.directory:
            - name: /home/vagrant/publicsites/kadi/
            - user: basic_user
            - group: basic_group
            - dir_mode: 755
 
       /home/vagrant/publicsites/kadi/index.html:
          file.managed:
            - source: "salt://apache/index.html"
            - user: basic_user
            - group: basic_group
            - mode: 644
   Ja suoritus onnistui
    ![h4-027](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-027.png)
   Mutta basic_userin **publicsites** oli yhä rootin. En ollut huomannut määritellä sen omistajuutta. Lisäsin init.sls-tiedostoon:

        /home/vagrant/publicsites:
          file.directory:
            - user: basic_user
            - group: basic_group
            - dir_mode: 755 
   

9. Tämä tepsi ja nyt kaikki saltilla luodut hakemistot ja tiedostot ovat oikeilla oikeuksilla.
   ![h4-028](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-028.png)
10. `curl localhost`ei kutenkaan tuonut toivottua lopputulosta, sillä se vastasi yhä oletussivulla "default".
    Tarkisitn kaikki tiedostot ja oikeudet, jotka olivat kunnossa. Seuraavaksi tarkistin conf-tiedoston joka sekin kunnossa, mutta `/sites.enabled/kadi.conf` näytti oudolta.
    ![h4-029](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-029.png)
12. Palasin tarkastelemaan apache-moduulia josta virhe löytyi. Jossain vaiheessa tiedostoa muokatessani linkki oli vaihtunut viittaamaan itseensä, jolloin se ei tietenkään voinut toimia.
    
        /etc/apache2/sites-enabled/kadi.conf:
          file.symlink:
            - target: "/etc/apache2/sites-enabled/kadi.conf"
14. Korjasin sen oikeaan muotoon ja samalla huomasin että palvelun boottaus oli tippunut lopusta. Lisäsin senkin *watchilla* höystettynä.
    
        /etc/apache2/sites-available/kadi.conf:
          file.symlink:
            - target: "/etc/apache2/sites-enabled/kadi.conf"

        apache2.service:
          service.running:
            - name: apache2
            - enable: Truecd 
            - restart: True
            - watch:
              - file: /etc/apache2/sites-available/kadi.conf
              - file: /etc/apache2/sites-enabled/kadi.conf
              - file: /home/vagrant/publicsites/kadi/index.html
    Tässä vaiheessa keskeytin työn ja palasin tehtävään tiistaina 23.04. aamusta.
16. Nyt conf-tiedoston korjauksien myötä tei uudelleenajon `sudo salt-call --local -l info state.apply apache`. Se ei mennyt odotetusti. Alla virhe joka viittasi vikaan ajankohdassa. Tarkistin koneen ajan ja se oli kolme päivää jäljessä:
    ![h4-030](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-030.png)
17. Tämän virheen takia tietenkään muutkaan apacheen liittyvät toimet eivät onnistuneet. Korjasin ajan, ja tarkistin että se on nyt oikeassa:
    ![h4-031](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-031.png)
    ![h4-032](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-032.png)
19. `sudo salt-call --local -l info state.apply apache` testasi uudelleen, ja lopputulos oli toivotun mukainen.
    ![h4-033](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-033.png)
20. Testasin `curl localhost` joka palautti toivotun lopputuloksen.
    ![h4-034](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-034.png)
22. Kävin vielä basic_userina muokkaamassa **index.html**-tiedostoa ja varmistin että toimii.
    ![h4-035](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-035.png)
23. Viimeiseksi testasin ajamalla saman komennon **doh002**-minionille `sudo salt '*' state.apply apache` mutta sain saman virheen väärästä ajasta joka olikin saman kolme päivää myöhässä.
    ![h4-036](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-036.png)
24. Päätin testata onnistuisinko lisäämään **time** tilan, joka tekisi tämän automaattisesti ennen **apache** tila ajoa.
    - Tein uuden tilan **time** /srv/salt- hakemistoon komennilla `sudo mkdir ntp` ja loin sinne `sudo micro init.sls`.
    - Tiedostoon tallensin seuraavat:

          ntp:
            pkg.installed
    
          ntp.service:
            service.running:
              - name: ntp
              - enable: True
              - restart: True 
    - Testasin paikallisesti `sudo salt-call --local -l info state.apply apache`, jonka lopputuloksena onnistunut ajo:
      ![h4-037](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-037.png)
    - Muokkasin osiossa **b)** luotua topfilea lisäämällä sinne ntp-moduulin.
      ![h4-038](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-038.png)
    - Testasin topfileä paikallisesti komennilla `sudo salt-call --local -l info state.apply` joka onnistui. Alla kuvassa ainoat muutoskset jotka johtuivat basic_userin aiemmin tekememästä testistä index.html tiedostoon.
      ![h4-039](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-039.png)
    -  Testasin minionille `sudo salt '*' state.apply` mutta ntp-paketin ajo ei onnistunut koneen väärän ajan johdosta.
       ![h4-040](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-040.png)
    -  Pitkän googlettelun jälkeen päädyin kyselemään chatGPT:ltä apua, sillä en keksinyt miten ajan voi päivittää jos aikatyökalua ei saa asennettua. Se ehdotti ntp-moduulin muokkaamista eri tavoin, joista jokainen tuotti eri errorin. Tässä vaiheessa luovutin ja päivitin ajan manuaalisti, sillä se ei ollut osa tehtävänantoa. Ajan päivitin kuten edellä päivitin masterin suoraan **doh002** koneelta. Lisäksi poistin ntp-moduulin top-filestä.
    -  Uuden testin jälkeen sain onnistuneen lopputuloksen.
       ![h4-041](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-041.png)
       ![h4-042](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-042.png)
    - Vielä testaus minionilla:
      ![h4-043](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h4-043.png)
      

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#h4-demoni)

---

## f) Vapaaehtoinen: Caddy. 
Asenna Caddy tarjoilemaan weppisivua. Weppisivun tulee näkyä palvelimen etusivulla (localhost). HTML:n tulee olla jonkun käyttäjän kotihakemistossa, ja olla muokattavissa normaalin käyttäjän oikeuksin, ilman sudoa (Karvinen 2024)

Aloitin ensin Caddyn käyttöönoton manuaalisti. 
- Ensin Caddyn asennus

      sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https curl
      curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg
      curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
      sudo apt-get update
      sudo apt install caddy
  (Caddy install 2024)
- Ja sitten käyttöönotto. 
  - Caddy käyntiin `caddy run`.
  - 
- 
- 

  

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#h4-demoni)

---

## g) Vapaaehtoinen: Nginx. 
Asenna Nginx (lausutaan engine-X) tarjoilemaan weppisivua. Weppisivun tulee näkyä palvelimen etusivulla (localhost). HTML:n tulee olla jonkun käyttäjän kotihakemistossa, ja olla muokattavissa normaalin käyttäjän oikeuksin, ilman sudoa.

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#h4-demoni)

---

## Lähteet: 

Caddy Documentation 2024, Install caddy. Luettavissa https://caddyserver.com/docs/install. Luettu 23.04.2024.

Karvinen T. 2024, Infra as Code - Palvelinten hallinta 2024. Luettavissa: https://terokarvinen.com/2024/configuration-management-2024-spring/#h4-demoni. Luettu 18.04.2024

Karvinen T. 2018, Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port. Luettavissa: https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh. Luettu 18.04.2024.

Karvinen T. 2023, Salt Vagrant - automatically provision one master and two slaves. Luettavissa: https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file. Luettu 18.04.2024

Salt Contributors 2024, Salt Overviev. Luettavissa: https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml.mLuettu 18.04.2024

Salt user guides, States 2024. Luettavissa: https://docs.saltproject.io/salt/user-guide/en/latest/topics/states.html. Luettu 19.04.2024


