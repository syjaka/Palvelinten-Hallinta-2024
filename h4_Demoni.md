# Keskeneräinen

# h4 Demoni

X ) [Lue ja tiivistä](https://github.com/syjaka/Palvelinten-Hallinta-2024/new/main#x-lue-ja-tiivist%C3%A4)

a) [Hello SLS](https://github.com/syjaka/Palvelinten-Hallinta-2024/new/main#y-k%C3%A4ytt%C3%B6ymp%C3%A4rist%C3%B6)

b) Top

c) Apache easy mode

d) SSHouto

e) Vapaaehtoinen: Apache

f) Vapaaehtoinen: Caddy

g) Vapaaehtoinen: Nginx

y) Käyttöympäristö

z) Alkutoimet


## x) Lue ja tiivistä. 

1. Karvinen 2023: [Salt Vagrant - automatically provision one master and two slaves](https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file), vain kohdat
  -  Infra as Code - Your wishes as a text file
  -  top.sls - What Slave Runs What States
2. Salt contributors: [Salt overview](https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml), kohdat
  -  Rules of YAML
  -  YAML simple structure
  -  Lists and dictionaries - YAML block structures
3. Karvinen 2018: [Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port](https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh)
  -  Artikkelissa on jonkun toisen Linux-version tiedosto. Jos tekisit samanlaisen, niin käyttäisit tietysti oman järjestelmäsi asetustiedostoa pohjana.
4. Silmäile Saltin ohjeet tilafunktioille pkg, file ja service. Nämä artikkelit ovat pitkiä, riittää kun luet vain johdannon ja silmäilet maintut komennot. Ei kannata yrittää opetella satoja itselle tarpeettomia parametreja ulkoa. (Less-vinkit alla)
   
        $ sudo salt-call --local sys.state_doc pkg # johdanto + silmäile pkg.installed, pkg.purged, pkgs
        $ sudo salt-call --local sys.state_doc file # johdanto + silmäile file.managed, file.absent, file.symlink
        $ sudo salt-call --local sys.state_doc service # johdanto + silmäile service.running, service.dead, enable

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/new/main#h4-demoni)

---


## y) Käyttöympäristö
Tehtävä toteutettiin MacBook Retina 12-inch, koneella jossa, host OS on Ventura 13.6.1 käyttöjärjestelmä Suomen maa-asetuksilla ja suomen kielellä. Koneessa on 1,3GHz kaksiytiminen Intel Core i5 prosessori ja 8Gt 1867 MHz LPDDR3 muistia. Näytönohjain on Intel HD Graphics 615 jossa VRAM 1536 Mt.

- Koneeseen asennettu Vagrant versio on 2.4.1.

## z) Alkutoimet
Koneen ja pääte-ohjelman käynnistys.

## a) Hello SLS! 
Tee Hei maailma -tila kirjoittamalla se tekstitiedostoon, esim /srv/salt/hello/init.sls.
b) Top. 
Tee top.sls niin, että useita valitsemiasi tiloja ajetaan automaattisesti, esim komennolla "sudo salt '*' state.apply" tai "sudo salt-call --local state.apply".

## c) Apache easy mode. 
Asenna Apache, korvaa sen testisivu ja varmista, että demoni käynnistyy.
Ensin käsin, vasta sitten automaattisesti.
Kirjoita tila sls-tiedostoon.
pkg-file-service
Tässä ei tarvita service:ssä watch, koska index.html ei ole asetustiedosto

## d) SSHouto. Lisää uusi portti, jossa SSHd kuuntelee.
Jos käytät Vagrantia, muista jättää portti 22/tcp auki - se on oma yhteytesi koneeseen. SSHd:n asetustiedostoon voi tehdä yksinkertaisesti kaksi "Port" riviä, molemmat portit avataan.
Löydät oikean asetuksen katsomalla SSH:n asetustiedostoa
Nyt tarvitaan service-watch, jotta demoni käynnistetään uudelleen, jos asetustiedosto muuttuu masterilla

## e) Vapaaehtoinen: Apache. 
Asenna Apache tarjoilemaan weppisivua. Weppisivun tulee näkyä palvelimen etusivulla (localhost). HTML:n tulee olla jonkun käyttäjän kotihakemistossa, ja olla muokattavissa normaalin käyttäjän oikeuksin, ilman sudoa.

## f) Vapaaehtoinen: Caddy. 
Asenna Caddy tarjoilemaan weppisivua. Weppisivun tulee näkyä palvelimen etusivulla (localhost). HTML:n tulee olla jonkun käyttäjän kotihakemistossa, ja olla muokattavissa normaalin käyttäjän oikeuksin, ilman sudoa.

## g) Vapaaehtoinen: Nginx. 
Asenna Nginx (lausutaan engine-X) tarjoilemaan weppisivua. Weppisivun tulee näkyä palvelimen etusivulla (localhost). HTML:n tulee olla jonkun käyttäjän kotihakemistossa, ja olla muokattavissa normaalin käyttäjän oikeuksin, ilman sudoa.
