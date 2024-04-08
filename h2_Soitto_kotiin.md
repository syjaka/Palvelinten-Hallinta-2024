# Keskeneräinen

# h2 Soitto kotiin


a) [ Kaksi virtuaalikonetta samassa verkossa ](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h2_Soitto_kotiin.md#a-kaksi-virtuaalikonetta-samassa-verkossa---08042024-klo-1311---1335-eet)

b) [ Saltin herra-orja arkkitehtuuri toimii verkon yli ](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h2_Soitto_kotiin.md#b-asenna-saltin-herra-orja-arkkitehtuuri-toimimaan-verkon-yli---08042024-klo-1345---1420-eet)

c) [ Shell-komento orjalla](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h2_Soitto_kotiin.md#c-aja-shell-komento-orjalla-saltin-master-slave-yhteyden-yli-08042024-klo-1430---1439-eet)

d) [ Idempotentit komennot master-slave yhteyden yli](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h2_Soitto_kotiin.md#d-aja-useita-idempotentteja-statesingle-komentoja-master-slave-yhteyden-yli-08042024-klo-1445---14-56-eet)

e) [ Orjien tekniset tiedot](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h2_Soitto_kotiin.md#e-ker%C3%A4%C3%A4-teknist%C3%A4-tietoa-orjista-verkon-yli-grainsitem-08042024-klo-1459---1501-eet)

f) [ Hello, IaC](https://github.com/syjaka/Palvelinten-Hallinta-2024/edit/main/h2_Soitto_kotiin.md#f-hello-iac-08042024-klo-1505---1530-eet)

x)[ Lue ja tiivistä](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h2_Soitto_kotiin.md#x-lue-ja-tiivist%C3%A4)

y) [ Käyttöympäristö](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h2_Soitto_kotiin.md#y-k%C3%A4ytt%C3%B6ymp%C3%A4rist%C3%B6)

z) [ Alkutoimet](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h2_Soitto_kotiin.md#z-alkutoimet)

---

## x) Lue ja tiivistä. 
### [Two Machine Virtual Network With Debian 11 Bullseye and Vagrant - Karvinen 2021: ](https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/)
Artikkelissa opastetaan kahden koneen virtuaaliverkon rakennus muutamassa minuutissa. Työ toteutetaan Vagrantin avulla, jonka asennus neuvotaan alkuun. 

- Tekstissä neuvotaan luomaan oma hakemisto projektille, jonne tallennetaan annettu vagrantfilen sisältö. Tämä tiedosto on Vagrant-konftiedosto, jossa määritellään ja automatisoidaan virtuaalisten tietokoneiden ja verkon luonnin ja hallinnan.
- Jotta ymmärrän esitetyn paremmin, avaan tähän enemmän itse artikkelin sisältöä. Eli varsinainen vagrantfilen sisältö ei ole avattu artikkelissa vaan tämä on oma lisäykseni.
  1. Skriptimuuttuja `$tscript`sisältää Shell-komennon, joka päivittää pakettien tietokannan ja asentaa `tree`paketin. Tämän jälkeen muuttuja tulostaa viestin `Done - set ...`
  2. Vagrant conffi
     -  `Vagrant.configure("2") do |config|`Aloittaa Vagrant conffin "2" version mukaan (Hashicorp1)
     -  `config.vm.synced_folder ".", "/vagrant", disabled: true` Poistaa oletuskansion `/vagrant` synkronoinnin käytöstä.
     -  `config.vm.synced_folder "shared/", "/home/vagrant/shared", create: true` Määrittelee uuden jaetun kansion `shared/` isäntäkoneelta joka synkronoidaan virtuaalikoneen polkuun `/home/vagrant/shared`. Mikäli kansiota ei ole se luodaan.
     -  `config.vm.provision "shell", inline: $tscript` suorittaa alussa määritellyn skriptin.
     -  `config.vm.box = "debian/bullseye64"` Määrittää bullseyen käytettäväksi määritettävän virtuaalikoneen peruskuvaksi (Hashicorp2)
  3. Virtuaalikoneisen määrittelyt
     - Konfiguraatiotiedostossa määritellään kaksi virtuaalikonetta `t001`ja `t002`
     - Molemmille määritellään omat hostnimet `t001.vm.hostname = "t001` ja `t002.vm.hostname = "t002"`, jotka ovat myös niiden sisäisten verkkojen nimet `t001.vm.network "private_network"` ja  `t002.vm.network "private_network"`
     - Molemmat saavat omat yksityiset IP-osoitteensa `ip: "192.168.88.101"` ja `ip: "192.168.88.102"`
- Lopuksi neuvotaan koneisiin loggautuminen ja poistuminen, käyttö, sekä luotujen koneiden tuhoaminen.
 

### [Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux - Karvinen 2018:](https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux)
Artikkelissa esitellään Saltin Master-Slave arkkitehtuurin pystytys lyhyesti.
- Alkuun asennetaan Master ja Slave jonka jälkeen Master-palvelimella suoritetaan `sudo salt-key-.A` komento.
- Kyseinen komento hallinnoin avaimia, joita Salt käyttää turvallisen yhteyden muodostamiseen masterin ja minionin välillä. Jokaisella minionilla on oma yksilöllinen avaimensa joka tulee hyväksyä masterilla. Komemennossa oleva `-A` tarkoittaa että kaikki tällä hetkellä hyväksymättömät avaimet hyväksytään.
- Loppuun vielä testataan asennuksen onnistuminen.


### [Hello Salt Infra-as-Code - Karvinen 2014:](https://terokarvinen.com/2024/hello-salt-infra-as-code/)
Saltin avulla voidaan hallinnoida tuhansia koneita IaC'ta hyödyntäen. Tämä artikkeli esittelee "Hello World" vastineen Saltin konfiguraationhallintajärjestelmässä. Alkuun aloitetaan luomalla uusi tila "state" joka varmistaa tietyn tekstitiedoston olemassaolon.

- Alkuun opastetaan Saltin ja Micron asennus.
- Seuraavaksi luodaan Hello moduuli:
  - IaC (infra as a Code) kirjoitetaan kansion `/srv/salt/hello/` `init.sls`-tiedostoon jonne luodaan idempotenttia koodia:
  
         /tmp/hellotero:
        file.managed '
 - `sudo salt-call --local state.apply hello`-komento käynnistää luodun Hello-tilan paikallisesti ja palautteena saadaan yksityiskohtainen selitys suoritetuista toimista.
 - Tarkistus että kaikki toteutettiin kuin pitää onnistuu `ls /tmp/hellotero`.
 - Loppuun avataan vielä idempotenssin konseptia esittämällä, että järjestelmän tilan pitäisi pysyä muuttumattomana, vaikka samaa moduulia sovellettaisiin useita kertoja. Kun suoritat "hello" tilan uudelleen, muutoksia ei enää tehdä, koska järjestelmä on jo oikeassa tilassa.

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h2_Soitto_kotiin.md#h2-soitto-kotiin)

---

## y) Käyttöympäristö

Tehtävä toteutettiin MacBook Retina 12-inch, koneella jossa, host OS on Ventura 13.6.1 käyttöjärjestelmä Suomen maa-asetuksilla ja suomen kielellä. Koneessa on 1,3GHz kaksiytiminen Intel Core i5 prosessori ja 8Gt 1867 MHz LPDDR3 muistia. Näytönohjain on Intel HD Graphics 615 jossa VRAM 1536 Mt.


---
## z) Alkutoimet

Koneen ja pääte-työkalun käynnistys.

Kaikki seuraavien osion tehtävänannot ovat peräisin Tero Karvisen - Infra As a Code - Palvelinten hallinta 2024 kurssisivulta.

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h2_Soitto_kotiin.md#h2-soitto-kotiin)

---

## a) Kaksi virtuaalikonetta samassa verkossa - 08.04.2024 klo 13.11. - 13.35 EET

Asenna kaksi virtuaalikonetta samaan verkkoon. Osoita, että pystyt käyttämään kumpaakin konetta (esim 'vagrant ssh t001'). Osoita, että koneet voivat pingata toisiaan. (Tämä tehtävä on helpointa tehdä Vagrantilla)(Karvinen 2024).

1. Koneessani oli jo Vagrant asennettu, joten aloitin tehtävän suoraan uuden projektihakemiston luonnilla - `mkdir twohost/`.
2. Luonnin jälkeen siirryin kyseiseen hakemistoon ja loin sinne vagrantfilen:
   > ![h2_001](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h2_001.png)
3. Komennolla `vagrant up` loin virtuaalikoneet käyttämällä äsken luotua conf-tiedostoa. Lopputuloksena minulla oli kaksi virtuaalikonetta k001 ja k002.
4. Testasin että pystyn käyttämään molempia luotuja koneita loggautumalla niille ja pingasin toinen toistaan, sekä googlen nimipalvelinta.
   > ![h2_002](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h2_002.png)
   > ![h2_0021](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h2_0021.png)
(Karvinen 2021)

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h2_Soitto_kotiin.md#h2-soitto-kotiin)

___

## b) Asenna Saltin herra-orja arkkitehtuuri toimimaan verkon yli - 08.04.2024 klo 13.45 - 14.20 EET.

Verkko voi olla virtuaalinen verkko paikallisten virtuaalikoneiden välillä, kuten muissakin alakohdissa (Karvinen 2024).

1. Siirryin k001 koneelle `vagrant ssh 001`
2. Aloitin päivittämällä paketit `sudo apt-get update` ja asentamalla salt masterin `sudo apt-get install salt-master`.
3. Tarkistin Masterin IP-osoitteen:
   > ![h02_003](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h2_003.png)
4.  Poistuin Masterista `exit` ja siirryin k002-koneelle `vagrant ssh k002`. Siellä aluksi päivitin paketit `sudo apt-get update`.
5.  `sudo apt-get install salt-minion` asensi Salt-minionin.
6.  Seuraavaksi lisäsin minionin asetustiedostoon masterin IP-osoitteen sekä annoin minionille oman id:n `sudoedit /etc/salt/minion`.
>  ![h02_004](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h2_004.png)
7. `sudo systemctl restart salt-minion.service` potkasi minionin, jotta muutokset tulivat käyttöön.
9.  Siirryn masteriin `exit` ja `vagrant ssh k001`.
10.  `sudo salt-key -A` ja `y` hyväksyi orjan salakirjoitusavaimen.
11.  Testaan `sudo salt '*' cmd.run 'whoami'` joka kysyy kaikkia kuulolla olevia minioneita vastaamaan. Tuloksena minionk1 vastaa.
>  ![h2_005](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h2_005.png)
    
[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h2_Soitto_kotiin.md#h2-soitto-kotiin)

---

## c) Aja shell-komento orjalla Saltin master-slave yhteyden yli - 08.04.2024 klo 14.30 - 14.39 EET.

1. `sudo salt '*' state.single file.managed '/tmp/network-master-greets-minions` loi network-master-greets-minions tiedoston minionin tmp-hakemistoon.
>  ![h2_006](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h2_006.png)
Komento `sudo salt '*' cmd.run 'ls -l /tmp/'` todentaa luonnin onnistuneen.
>  ![h2_007](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h2_007.png)

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h2_Soitto_kotiin.md#h2-soitto-kotiin)

---

## d) Aja useita idempotentteja (state.single) komentoja master-slave yhteyden yli - 08.04.2024 klo 14.45 - 14. 56 EET.

1. Komennon `sudo salt '*' state.single file.managed '/tmp/network-master-greets-minions` uudelleenajo todisti komennon olevan idempotentti, sillä onnistuneesta ajosta huolimatta muutoksia ei tehty.
>  ![h2_008](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h2_008.png)
2. Komento `sudo salt '*' state.single user.present name=minon-clone` loi minonille käyttäjän `minion-clone` ja komennen uudelleenajo näytti idempotentin luonteen ajamalla komennon onnistuneesti, muuttamatta mitään.
>  ![h2_009](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h2_009.png)
3. Komento `sudo salt '*' state.single pkg.installed name=cowsay` toimi samoin.
>  ![h2_010](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h2_010.png)
>  ![h2_011](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h2_011.png)

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h2_Soitto_kotiin.md#h2-soitto-kotiin)

---

## e) Kerää teknistä tietoa orjista verkon yli (grains.item), 08.04.2024 klo 14.59 - 15.01 EET.

Komento `sudo salt '*' grains.item os ipv4 master osfinger` palauttaa seuraavat:
![h2_012](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h2_012.png)

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h2_Soitto_kotiin.md#h2-soitto-kotiin)

---

## f) Hello IaC, 08.04.2024 klo 15.05 - 15.30 EET.
Tee infraa koodina kirjoittamalla /srv/salt/hello/init.sls. Aja tila jollekin orjalle. Tila voi esimerkiksi tehdä esimerkkitiedoston johonkin hakemistoon. Testaa toisella komennolla, että pyytämäsi muutos on todella tehty (Karvinen 2024).

1. Aloitin asentamalla micron `sudo apt-get -y install micro` ja määritin sen defaultiksi `export EDITOR=micro`
2. Loin uuden kansion hello `sudo mkdir -p /srv/salt/hello/` ja siirryin sinne `cd /srv/salt/hello/`
3. Loin siellä init.sls tiedoston `sudoedit init.sls` jonne tallensin
![h02_013](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h2_013.png)
4. Yo. toimet ovat siis luoneet hello moduulin/kansion saltin srv hakemistossa.
5. Komennolla `sudo salt '*' state.apply hello` suoritin luodun moduulin.
6. Koska hakemisto oli jo aiemmin luotu ei muutoksia tehty mutta komennon ajo onnistui.
![h2_014](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h2_014.png)
7. Muokkasin luotavan hakemiston nimeä - IaC ja testsin uudelleen
![h2_015](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h2_015.png)
Ensimmäinen ajo osoitti, että uusi hakemisto luotiin, toinen että muutoksia ei tarvinnut tehdä.
9. `sudo salt '*' cmd.run 'ls -l /tmp/'` tarkisti että hakemistot ovat luotu kuten pitää.
![h2_016](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h2_016.png)
10. Orjalla tehty tuplatsekkaus paljasti, että näin todella on.
![h2_017](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h2_017.png)

(Karvinen 2024).



## Lähteet

Hashicorp1, Vagrant Documentation, Configuration Version. Luettavissa: https://developer.hashicorp.com/vagrant/docs/vagrantfile/version. Luettu 08.04.2024.

Hashicorp2, Vagrant Documentation, Config.vm. Luettavissa: https://developer.hashicorp.com/vagrant/docs/vagrantfile/machine_settings. Luettu 08.04.2024.

Karvinen T. Infra as Code - Palvelinten hallinta 2024. Luettavissa: https://terokarvinen.com/2024/configuration-management-2024-spring/#h2-soitto-kotiin. Luettu 08.04.2024

Karvinen T. Hello Salt Infra-as-Code 2014. Luettavissa https://terokarvinen.com/2024/hello-salt-infra-as-code/. Luettu 08.04.2024

Karvinen T. Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux 2018. Luettavissa: https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux. Luettu 08.04.2024

Karvinen T. Two Machine Virtual Network With Debian 11 Bullseye and Vagrant 2021. Luettavissa: https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/. Luettu 08.04.2024



