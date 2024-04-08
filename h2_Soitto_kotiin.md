# Keskeneräinen

# h2 Soitto kotiin


a) [ Kaksi virtuaalikonetta samassa verkossa ]()

b) [ Saltin herra-orja arkkitehtuuri toimii verkon yli ]()

c) [ Shell-komento orjalla]()

d) [ Idempotentit komennot master-slave yhteyden yli]()

e) [ Orjien tekniset tiedot]()

f) [ Hello, IaC]()

2x)[ Lue ja tiivistä]()

y) [ Käyttöympäristö]()

z) [ Alkutoimet]()

---

## 2x) Lue ja tiivistä. 
### [Two Machine Virtual Network With Debian 11 Bullseye and Vagrant - Karvinen 2021: ](https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/)
Artikkelissa opastetaan kahden koneen virtuaaliverkon rakennus muutamassa minuutissa. Työ toteutetasan Vagrantin avulla joinka asennus neuvotaan alussa. 

- Teksitssä neuvotaan luomaan oma hakemisto projektille joinne tallennetaan annettu vagrantfilen sisältö. Tämä tiedosto on Vagrant-konftiedosto jossa määritellään ja automatisoidaan virtuaalisten tietokoneiden ja verkon luonnin ja hallinnan.
- Jotta ymmärrän esitetyn toimen paremmin avaan tähän enemmän itse artikkelin sisältöä. Eli varsinainen vagrantfile ei ole avattu enempää artikeilissa vaan tämä on oma lisäykseni.
  1. Skriptimuuttuja `$tscript`sisälktää Shell-komennon joka päivittää pakettien tietokannan ja asentaa `tree`paketin. Tämän jälkeen muuttuja tulostaa viestin `Done - set ...`
  2. Vagrant conffi
     -  `Vagrant.configure("2") do |config|`Aloittaa Vagrant conffin "2" version mukaan (Hashicorp1)
     -  `config.vm.synced_folder ".", "/vagrant", disabled: true` Poistaa oletuskansion `/vagrant` synkronoinnin käytöstä.
     -  `config.vm.synced_folder "shared/", "/home/vagrant/shared", create: true` Määrittelee uuden jaetun kansion `shared/` isäntäkoneelta joka nsynkronoidaan virtuaalikoneedeen polkuun `/home/vagrant/shared`. Mikäli kansiota ei ole se luodaan.
     -  `config.vm.provision "shell", inline: $tscript` suorittaa alussa määritellyn skriptin.
     -  `config.vm.box = "debian/bullseye64"` Määrittää bullseyen käytettäväksi määritettävän virtuaalikoneen peruskuvaksi (Hashicorp2)
  3. Virtuaalikoneisen määrittelyt
     - Konfiguraatiotiedostossa mnääritellään kaksi virtuaalikonetta `t001`ja `t002`
     - Molemmille määritellään omat hoitsnimet `t001.vm.hostname = "t001` ja `t002.vm.hostname = "t002"`jotka ovat myös niiden sisäisen verkon nimiet `t001.vm.network "private_network"` ja  `t002.vm.network "private_network"`
     - Molemmat saavat omat yksityiset IP-osoitteensa `ip: "192.168.88.101"` ja `ip: "192.168.88.102"`
- Lopuksi neuvotaan koneisiin loggautuminen ja poistuminen, käyttö sekä luotujen koneiden tuohoaminen.
 

### [Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux - Karvinen 2018:](https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux)
Artikkelkissa esitellään Saltin master-Slave arkkitehtuurin pystytys lyhyesti.
- Alkuun asennetaan Master ja Slave jonka jälkeen Master-palvelimella suoritetaan `sudo salt-key-.A`komento.
- Kyseinen komento hallinnoin avaimia joita Salt käyttää turvallisen yhteyden muodostamiseen masterin ja minionin välillä. Jokaisella minionilla on oma yksilöllinen avaimensa jaka tulkee hyväksyä masterilla. kuitenkin mon´mennossa oleva `-A`tarkoittaa että kaikki tällä hetkellä hyväksymättömät avaimet hyväksytään.
- Loppuun vielä testataan asennuksen onnistuminen.


### [Hello Salt Infra-as-Code - Karvinen 2014:](https://terokarvinen.com/2024/hello-salt-infra-as-code/)
Saltin avulla voidaan hallinnoida tuhansia koneita Iac'n avulla. Tämä artikkeli esittelee "Hello World" vastineen Saltin configuraationhallintajärjestelmässä. Alkuun aloitetaan luomalla uusi tila "state" joka varmistaa tietyn tekstitiedoston olemassaolon.

- Alkuun opastetaan Saltin ja Micron asennus.
- Seuraavaksi luodaan Hello moduuli:
  - IaC (infra as a Code) kirjoitetaan kansion `/srv/salt/hello/` `init.sls`-tiedostoon jonne luodaan idempotenttia koodia:
  
         /tmp/hellotero:
        file.managed '
 - `sudo salt-call --local state.apply hello`-komento käynnistää luodun Hello-tilan paikallisesti ja palautteena saadaan yksityisj´kohtainen selitys suoritetuista toimista.
 - Tarkistus että kaikki toteutettiin kuin piti onnistuu `ls /tmp/hellotero`.
 - Loppuun avataan vielä idempotenssin konseptia esittämällä että järjestelmän tilan pitäisi pysyä muuttumattomana, vaikka samaa moduulia sovellettaisiin useita kertoja. Kun suoritat "hello" tilan uudelleen, muutoksia ei enää tehdä, koska järjestelmä on jo oikeassa tilassa.

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
2. Luonnin jälkeen siirryin kyseiseen hake,ostoon ja loin sinne vagrantfilen:
   > ![h2_001]()
3. Komennolla `vagrant up` luon virtuaalikoneet käyttämällä äsken luotuo conf-tiedostoa- Lopputuloksena minulla on kaksi virtuaalikonetta k001 ja k002.
4. Testaan että pytstyn käyttämään molempia luotuja koneita loggautumalla niille ja pingaan toinen toistaan, sekä googlen nimipalvelimen.
   > ![h2_002]()
   > ![h2_0021]()
(Karvinen 2021)

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h2_Soitto_kotiin.md#h2-soitto-kotiin)

___

## b) Asenna Saltin herra-orja arkkitehtuuri toimimaan verkon yli - 08.04.2024 klo 13.45 - 14.20 EET.

Verkko voi olla virtuaalinen verkko paikallisten virtuaalikoneiden välillä, kuten muissakin alakohdissa (Karvinen 2024).

1. Siirryin k001 koneelle `vagrant ssh 001`
2. Aloitin päivittämällä paketit `sudo apt-get update`ja asentamalla salt masterin `sudo apt-get install salt-master`
3. Tarkistin Masterin IP-osoitteen
   > ![h02_003]()
4.  Poistuin Masterista èxit`ja siissryin k002-koneelle `vagrant ssh k002`. Siellä aluksi päivitin paketit `sudo apt-get update`.
5.  `sudo apt-get install salt-minion` asensi Salt-minionin.
6.  Seuraavaksi lisään minionin asetustiedostoon masterin IP-osoitteen sekä annan minionille oman id:n `sudoedit /etc/salt/minion`
 ![h02_004]()
7.  
8.  `sudo systemctl restart salt-minion.service`potkasee minionin jotta muutokset tulee käyttöön.
9.  Siirryn masteriin `exit` ja `vagrant ssh k001`
10.  `sudo salt-key -A` ja `y` hyväksyy orjan salakirjoitusavaimen.
11.  Testaan `sudo salt '*' cmd.run 'whoami'` joka kysyy kaikkia kuulolla olevia minioneita vastaamaan. Tuloksena minionk1 vastaa.
![h2_005]()
    
[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h2_Soitto_kotiin.md#h2-soitto-kotiin)

---

## c) Aja shell-komento orjalla Saltin master-slave yhteyden yli. 08.04.2024 klo 14.30 - 14.39 EET.

1. `sudo salt '*' state.single file.managed '/tmp/network-master-greets-minions` luo network-master-greets-minions tiedoston minionin tmp-hakemistoon
![h2_006]()
Komento `sudo salt '*' cmd.run 'ls -l /tmp/'`  todentaa luonnin onnistuneen
[h2_007]()

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h2_Soitto_kotiin.md#h2-soitto-kotiin)

---

## d) Aja useita idempotentteja (state.single) komentoja master-slave yhteyden yli. 08.04.2024 klo 14.45 - 14. 56 EET.

1. Yllä esitetyn komennon `sudo salt '*' state.single file.managed '/tmp/network-master-greets-minions` uudelleenajo todisti komennon olevan idempotentti
![h2_008]()
2. Komento `sudo salt '*' state.single user.present name=minon-clone`luo minonille käyttäjän minion-clone hja komennen uudelleenajo näyttää idempotentin luonteen ajamalla komennon muuttamatta mitään
![h2_009]()
3. Komento ``toimii samoin
![h2_010]()
![h2_011]()

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h2_Soitto_kotiin.md#h2-soitto-kotiin)

---

## e) Kerää teknistä tietoa orjista verkon yli (grains.item) 08.04.2024 klo 14.59 - 15.01

Komento `sudo salt '*' grains.item os ipv4 master osfinger`palauttaa seuraavat:
![h2_012]()

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h2_Soitto_kotiin.md#h2-soitto-kotiin)

---

## f) Hello, IaC 08.04.2024 klo 15.05 - 
Tee infraa koodina kirjoittamalla /srv/salt/hello/init.sls. Aja tila jollekin orjalle. Tila voi esimerkiksi tehdä esimerkkitiedoston johonkin hakemistoon. Testaa toisella komennolla, että pyytämäsi muutos on todella tehty (Karvinen 2024).

1. Aloitin asentamalla micron `sudo apt-get -y install micro` ja määritän sen defaultiksi `export EDITOR=micro`
2. Luon uuden kansion hello `sudo mkdir -p /srv/salt/hello/` ja siirryn sinne `cd /srv/salt/hello/`
3. Luon siellä init.sls tiedoston `sudoedit init.sls` jonne tallennan
![h02_013]()
4. Yo. toimet ovat siis luoneet hello moduulin/kansion saltin srv hakemiostossa.
5. komennolla `sudo salt '*' state.apply hello` suoritan
6. Koska hakemisto oli jo aiemmin luotu ei muutoksia tehty mutta komennon ajo onnistui.
![h2_014]()
7. Muokkaan luotavan hakemiston nimeä - IaC ja testaan uudelleen
![h2_015]()
Ensimmäinen ajo osoittaa että uusi hakemisto luotiin, toinen että muutoksia ei tarvinnut tehdä.
9. `sudo salt '*' cmd.run 'ls -l /tmp/'` tarkisti että hakemistot ovat luotu kuten pitää.
![h2_016]()
10. Orjalla tehty tuplatsekkaus paljastaa että näin todella on
![h2_017]()

(Karvinen 2024).



## Lähteet

Hashicorp1, Vagrant Documentation, Configuration Version. Luettavissa: https://developer.hashicorp.com/vagrant/docs/vagrantfile/version. Luettu 08.04.2024.

Hashicorp2, Vagrant Documentation, Config.vm. Luettavissa: https://developer.hashicorp.com/vagrant/docs/vagrantfile/machine_settings. Luettu 08.04.2024.

Karvinen T. Infra as Code - Palvelinten hallinta 2024. Luettavissa: https://terokarvinen.com/2024/configuration-management-2024-spring/#h2-soitto-kotiin. Luettu 08.04.2024

Karvinen T. Hello Salt Infra-as-Code 2014. Luettavissa https://terokarvinen.com/2024/hello-salt-infra-as-code/. Luettu 08.04.2024

Karvinen T. Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux 2018. Luettavissa: https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux. Luettu 08.04.2024

Karvinen T. Two Machine Virtual Network With Debian 11 Bullseye and Vagrant 2021. Luettavissa: https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/. Luettu 08.04.2024



