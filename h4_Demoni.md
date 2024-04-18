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

1. Karvinen 2023: [Salt Vagrant - automatically provision one master and two slaves](https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file), vain kohdat
  -  Infra as Code - Your wishes as a text file
      - Luodaan hakemisto Saltin conffille, luodaan ja muokataan Saltin tilatiedosto jonne määritellään file.managed-tila ja sovelletaan luotua tilaa käyttäen Saltia.
  -  top.sls - What Slave Runs What States
    - Top-file on tiedosto joka määrittää mitkä tilat milläkin koneella ajetaan. Tekstissä ensin keskeytetään mahdollinen käynnissä ollut komento. Tämän jälkeen luodaan/muokataan top-file, siten että se ajaa kaikille (`'*'`) Saltin hallinnassa oleville koneille **hello** tilan. Lopuksi *state apply* ajaa top-filessa määritellyt tilat `'*'`-koneille.
2. Salt contributors: [Salt overview](https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml), kohdat
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

3. Karvinen 2018: [Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port](https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh)
Artikkelissa esitellään miten SSH-portin vaihtaminen automatisoidaan Salt-tilan avulla. Tekstissä on luotu SSH-tila, joka alkuun varmistaa rttä SSH-server on asennettu. Sen jälkeen se korvaa SSHoletusconf-tiedoston `sshd_config` tiedostolla, jota on muokattu poistamalla kommentti ja vaihtamalla portti 8888. Loppuun määritellään että sshd-palvelun tulee olla käynnissä ja asetetaan `watch`-parametri havaitsemaan m,ahdolliset conf-tiedostoon tehdyt muutokset ja näitä havaitessaan käynnistämään palvelun uudelleen.
Tilan luonnin jälkeen se suoritetaan ja lopputulosta testataan kahdella eri menetelmällä.

5. Silmäile Saltin ohjeet tilafunktioille pkg, file ja service. Nämä artikkelit ovat pitkiä, riittää kun luet vain johdannon ja silmäilet maintut komennot. Ei kannata yrittää opetella satoja itselle tarpeettomia parametreja ulkoa. (Less-vinkit alla)
   
        $ sudo salt-call --local sys.state_doc pkg # johdanto + silmäile pkg.installed, pkg.purged, pkgs
        $ sudo salt-call --local sys.state_doc file # johdanto + silmäile file.managed, file.absent, file.symlink
        $ sudo salt-call --local sys.state_doc service # johdanto + silmäile service.running, service.dead, enable

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#h4-demoni)

---


## y) Käyttöympäristö
Tehtävä toteutettiin MacBook Retina 12-inch, koneella jossa, host OS on Ventura 13.6.1 käyttöjärjestelmä Suomen maa-asetuksilla ja suomen kielellä. Koneessa on 1,3GHz kaksiytiminen Intel Core i5 prosessori ja 8Gt 1867 MHz LPDDR3 muistia. Näytönohjain on Intel HD Graphics 615 jossa VRAM 1536 Mt.

- Koneeseen asennettu Vagrant versio on 2.4.1.

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
    
Koneiden luonnin jälkeen jälkeen asensin niille Saltin seuraten tehtävärapsani h2_Soitto_kotiin [- Kaksi vituaalikonetta samassa verkossa - ](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h2_Soitto_kotiin.md#b-asenna-saltin-herra-orja-arkkitehtuuri-toimimaan-verkon-yli---08042024-klo-1345---1420-eet) steppejä.

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#h4-demoni)

---

## a) Hello SLS! 
Tee Hei maailma -tila kirjoittamalla se tekstitiedostoon, esim /srv/salt/hello/init.sls.

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#h4-demoni)

---

## b) Top. 
Tee top.sls niin, että useita valitsemiasi tiloja ajetaan automaattisesti, esim komennolla "sudo salt '*' state.apply" tai "sudo salt-call --local state.apply".

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#h4-demoni)

---

## c) Apache easy mode. 
Asenna Apache, korvaa sen testisivu ja varmista, että demoni käynnistyy.
Ensin käsin, vasta sitten automaattisesti.
Kirjoita tila sls-tiedostoon.
pkg-file-service
Tässä ei tarvita service:ssä watch, koska index.html ei ole asetustiedosto

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#h4-demoni)

---

## d) SSHouto. 
Lisää uusi portti, jossa SSHd kuuntelee.
Jos käytät Vagrantia, muista jättää portti 22/tcp auki - se on oma yhteytesi koneeseen. SSHd:n asetustiedostoon voi tehdä yksinkertaisesti kaksi "Port" riviä, molemmat portit avataan.
Löydät oikean asetuksen katsomalla SSH:n asetustiedostoa
Nyt tarvitaan service-watch, jotta demoni käynnistetään uudelleen, jos asetustiedosto muuttuu masterilla

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


