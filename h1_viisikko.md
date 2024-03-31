
# h 1 Viisikko

x) [Lue ja tiivistä](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h1_viisikko.md#x-lue-ja-tiivist%C3%A4)

a) [Hello Mac Salt World](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h1_viisikko.md#a-hello-mac-salt-world)

b) [Hello Vagrant](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h1_viisikko.md#b-hello-vagrant)

c) [Tee Vagrantilla uusi Linux Virtuaalikone](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h1_viisikko.md#c-tee-vagrantilla-uusi-linux-virtuaalikone)

d) [Asenna Salt (salt-minion) Linuxille](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h1_viisikko.md#d-a-asenna-salt-salt-minion-linuxille-uuteen-virtuaalikoneeseesi)

e) [Viisi tärkeintä](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h1_viisikko.md#e-viisi-t%C3%A4rkeint%C3%A4)

f) [Idempotentti](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h1_viisikko.md#f-idempotentti-anna-esimerkki-idempotenssista)

g) [Tietoa koneesta](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h1_viisikko.md#g-tietoa-koneesta)

y) [Käyttöympäristö](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h1_viisikko.md#x-lue-ja-tiivist%C3%A4)

z) [Alkutoimet](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h1_viisikko.md#z-alkutoimet)

---

## x) Lue ja tiivistä

---
### Run Salt command locally - Karvinen 2023

> - Kyseisessä kirjoituksessa opastetaan miten salt komentoja voidaan ajaa paikallisesti ja nähdä tulokset välittömästi. Esitellyt komennot siis opastavat kuinka Saltia voidaan käyttää paikallisesti yksittäisten hallintatehtävien suorittamiseksi ilman verkon yli tapahtuvaa master-slave arkkitehtuuria. Alkuun opastetaan Saltin-minionin asennus muutamalla komennolla, jonka jälkeen on aina hyvä tarkistaa asennuksen onnistuminen.
> - Seuraavaksi mainitaan, että paketinhallintasovellus tulee olla asennettu ja esitellään tree-paketin asennus ja poistokomennot.
> - Kaikki Linuxin asetukset ovat tekstitiedostoja, joten seuraavaksi luotiin/tarkistettiin tmp/hellotero tiedoston olemassaolo, sekä luotiin tai tarkistettiin tmp/moitero tiedoston olemassaolo ja tallennettiin sinne sisällöksi `foo`.
> - `$ sudo salt-call --local -l info state.single file.absent /tmp/hellotero` varmistaa että tmp/hellotero tiedostoa ei ole olemassa.
> - Palveluiden hallinta
>   - `$ sudo salt-call --local -l info state.single service.running apache2 enable=True` varmistaa että Apache2 on käynnissä ja `$ sudo salt-call --local -l info state.single service.dead apache2 enable=False` toimii päinvastoin.
> - Seuraavaksi opastetaan käyttäjänhallintaa eli käyttäjän luonnin tai poiston.
> - Komentojen suorittaminen:
>    - `$ sudo salt-call --local -l info state.single cmd.run 'touch /tmp/foo' creates="/tmp/foo"`  luo  tyhjän tiedoston, mikäli sitä ei vielä ole. Komennossa siis esitetään idempotenssin käsitettä, eli suoritetaan vain, jos määritetty ehto ei täyty. 
> Viimeiseksi  `$ sudo salt-call --local sys.state_doc` komennolla saadaan näytettyä dokumentaatio saatavilla olevista Salt state-toiminnoista paikallisesti (local). (Karvinen/b 2023)

### Create Web page using Github - Karvinen 2023

> Artikkelissa opastetaan vaihe vaiheelta verkkosivun julkaiseminen Githubissa. Alkuun palveluun tulee rekisteröityä, jonka jälkeen luodaan repository. Luotuun repositoryyn päästään luomaan eri tiedostoja MarkDownilla eli tiedosto tallennetaan .md päätteellä. Artikkelissa kerrotaan myös md alkeet, joilla saadaan aikaan helposti luettavaa jäsennettyä tekstiä. (Karvinen/a)

### Raportin kirjoittaminen - Karvinen 2023

Koska olen tämän tiivistelmän kirjoittanut jo edellisellä kurssilla ja pyörää ei kannattane keksiä uudestaan, käytän tämän palautukseen aiemman [tiivistelmääni](https://github.com/syjaka/Linux-Palvelimet-2024/blob/main/h1_OmaLinux.md#1-raportointiohjeen-tiivistelm%C3%A4) lyhentämättömänä. 

> Raportin kirjoittaminen

> Hyvä raportointitapa tehostaa työskentelyä ja oppimista jäsentämällä ja selkeyttämällä koko työskentelyprosessia. Hyvään raportointiin kuuluu muutamia peruselementtejä:

> Toistettavuus, Hyvän raportin perusteella koko työnkulku pitäisi olla toistettavissa samassa ympäristössä.
> 1. Täsmällisyys, Hyvässä raportissa on selkeästi kirjattu kaikki annetut komennot ja niiden seuraukset.
> 2. Helppolukuisuus, Hyvää raporttia on helppo lukea sen järjestelmällisen rakenteen ja hyvän kielen ansiosta.
> 3. Hyvässä raportissa on lähteet listattu perusteellisesti.
> Pahimpia mokia raporttia kirjoittaessa ovat asioiden keksiminen sekä plagiointi. Tärkeää on tehdä annetut tehtävät ja dokumentoida tämä helppolukuisesti ja selkeästi. (Karvinen/c 2024)

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h1_viisikko.md#h-1-viisikko)

---

## y) Käyttöympäristö
Tehtävä toteutettiin MacBook Retina 12-inch, koneella jossa, host OS on Ventura 13.6.1 käyttöjärjestelmä Suomen maa-asetuksilla ja suomen kielellä. Koneessa on 1,3GHz kaksiytiminen Intel Core i5 prosessori ja 8Gt 1867 MHz LPDDR3 muistia. Näytönohjain on Intel HD Graphics 615 jossa VRAM 1536 Mt.

## z) Alkutoimet

Koneen ja pääte-työkalun käynnistys.


Kaikki seuraavien osion tehtävänannot ovat peräisin Tero Karvisen - Infra As a Code - Palvelinten hallinta 2024 [kurssisivulta](https://terokarvinen.com/2024/configuration-management-2024-spring/#h1-viisikko). 

## a) Hello Mac Salt World
Näytä jollain Salt-komennolla, että olet onnistunut asentamaan Saltin (salt-minion) Windowsille tai Macille. Jos et ole vielä asentanut Saltia, raportoi myös asennus. (Karvinen 2024)
Koska asensin Saltin jo tunnilla [saltproject](https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/macos.html#install-macos) ohjeiden mukaan, en sitä enää tässä dokumentoi.
Saltin onnistunut asennus näkyy ao. kuvassa:
> ![a-001](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h1-001.png)

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h1_viisikko.md#h-1-viisikko)

---

## b) Hello Vagrant
Osoita jollain komennolla, että Vagrant toimii. Jos et ole vielä asentanut niitä, raportoi myös Vagrant ja VirtualBox asennukset. (Karvinen 2024)

Itse Vagrant tuli asennettua viime kurssilla ja siitä raporttia [täällä](https://github.com/syjaka/Linux-Palvelimet-2024/blob/main/h5_Uudestaan.md#m-vagrant) (Syrjä 2024).
> ![a-002](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h1-002.png)

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h1_viisikko.md#h-1-viisikko)

---

## c) Tee Vagrantilla uusi Linux-virtuaalikone
suoritus kesti noin 5 min.

Virtuaalikoneen teko Vagrantilla oli nopeaa. Loin aluksi uuden kansion Bullseyelle ja sen jälkeen suoritin tarvittavat komennot:

>     vagrant init debian/bullseye64
>     vagrant up

Asennus käynnistyi ja hetken kuluttua oli valmista. Uusi virtuaalikone oli ilmestynyt Virtualboxiin:
> ![a-003](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h1-003.png)

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h1_viisikko.md#h-1-viisikko)

---

## d) a) Asenna Salt (salt-minion) Linuxille (uuteen virtuaalikoneeseesi)
suoritus kesti noin 8 min.

- Avaan yhteyden edellä luotuun virtuaalikoneeseen.
    
      vagrant ssh 
> ![a-004](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h1-004.png)

- Haen päivitykset

      sudo apt-get update
- Asennan minionin ja tarkistan asennuksen version. Lisäksi tarkistin vielä, että minion vastaa. Vastaus osoitti asennuksen onnistuneen.

      sudo apt-get -y install salt-minion
      sudo salt-call --version
      sudo salt-call --local grains.item osfinger virtual
> ![a-005](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h1-005.png)

(Karvinen/b 2023).

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h1_viisikko.md#h-1-viisikko)

---

## e) Viisi tärkeintä. 
Loppuosoin suoritus alkoi 31.03.2024 klo 15.00 ETC ja päättyi 17.23 ETC.
Näytä Linuxissa esimerkit viidestä tärkeimmästä Saltin tilafunktiosta: pkg, file, service, user, cmd. Analysoi ja selitä tulokset.
### 1. Paketinhallinta - *pkg*  on nimensä mukaisesti paketinhallintatyökalu, eli sillä asennetaan erilaisia sovelluspaketteja.
- tree -ohjelman asennus komennolla:

       salt-call --local -l info state.single pkg.installed tree

> ![a-006](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h1-006.png)
 
- ID: kertoo mitä käsiteltiin eli tree ohjelma.
- Function: kertoo mitä funktiota asennukseen käytettiin.
- Result: kertoo lopputuloksen, True - yo. funktion asennus onnistui.
- Comment summaa toteutetun toiminnon.
- Started: aloitusaika.
- Duration: asennuksen kesto.
- Changes: mitä muutoksia tehtiin eli nyt asennettiin uusi ohjelma tree versiolla 1.8.0-1+b1, ja vanhaa versiota ei ollut.
- Summary: kertaa montako onnistunutta ja epäonnistunutta operaatiota suoritettiin ja niiden suoritusaika.


### 2. Tiedostojen hallinta - *file* 
- kaditestaa tiedoston luonti komennolla:

       sudo salt-call --local -l info state.single file.managed /tmp/kaditestaa
> ![a-007](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h1-007.png)

 - Tässä palautteessa alun *[WARNING]* osa osoittaa hyvän esimerkin idempotenssista. Vaikka `replace` arvo on asetettu `true`, ei ole mitään määriteltyä lähdettä, sisältöä tai korvaavia parametrejä, joten salt ei tiedä millä olemassa oleva tiedosto korvattaisiin, jos sellainen olisi. Tämän vuoksi salt asettaa `replace` arvoksi `false`. Tämä varmistaa idempotentin toteutumisen - jos tiedostoa ei ole, se luodaan, mutta jos se on olemassa, sitä ei muokata ilman selkeitä ohjeita.
- ID: kertoo mitä käsiteltiin eli /tmp/kaditestaa/.
- Function: kertoo mitä funktiota asennukseen käytettiin.
- Result: kertoo lopputuloksen, True - yo. funktion suoritus onnistui
- Comment summaa toteutetun toiminnon
- Started: aloitusaika
- Duration: asennuksen kesto
- Changes: mitä muutoksia tehtiin eli luotiin /tmp/kaditestaa tiedosto.
- Summary: kertaa montako onnistunutta ja epäonnistunutta operaatiota suoritettiin ja niiden suoritusaika.


### 3. Palveluiden hallinta - *service* - huolehtii eri palvelujen käyttöönotosta tai deaktivoimisesta.
- Apachen käyttöönotto komennolla:

       sudo salt-call --local -l info state.single service.running apache2 enable=True
> ![a-008](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h1-008.png)
 
- *[ERROR]* kertoo että kyseistä palvelua ei ole saatavilla - tämä tietenkin ilmiselvää, sillä apachea ei luotuun koneeseen ole asennettu.
- ID: kertoo mitä käsiteltiin eli apache2.
- Function: kertoo mitä funktiota käytettiin.
- Result: kertoo lopputuloksen, False, eli funktion ajo ei onnistunut.
- Comment summaa toteutetun toiminnon eli kertoo että apache2 ei ole saatavilla.
- Started: aloitusaika
- Duration: asennuksen kesto
- Changes: mitä muutoksia tehtiin - tässä tapauksessa ei mitään.
- Summary: kertaa montako onnistunutta ja epäonnistunutta operaatiota suoritettiin ja niiden suoritusaika.


### 4. Käyttäjien hallinta -  *user* - 
- Käyttäjän kadisa001 luonti komennolla

       sudo salt-call --local -l info state.single user.present kadisa001
> ![a-009](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h1-009.png)
- ID: Luotiin kadisa001
- Function: millä funktiolla
- Result: Onnistunut lopputulos *True*
- Comment: Kertoo että uusi käyttäjä luotiin
- Started: luontiaika
- Duration: toiminnon kesto
- Changes: tehdyt muutokset, joista gid on käyttäjäryhmä 1001, groups on kadisa001 oma ryhmä, home esitteleee käyttäjän kotihakemistopolun, name on käyttäjänimi, salasanaa ei ole määritetty, shell on oletuskomentotulkki ja uid on käyttäjän id.
- Summary taas kertaa tehdyt toimet.


### 5. Komentojen ajo tietyin ehdoin *cmd.run*
- cmd-tilamoduuli hallinnoi suoritettujen komentojen täytäntöönpanoa - tila antaa täytäntöönpanolle ehdot. Ao-komennolla suoritin salt-tilan luomaan /tmp/foo tiedoston.
  
       sudo salt-call --local -l info state.single cmd.run 'touch /tmp/foo' creates="/tmp/foo"
> ![a-010](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h1-010.png)
- Jälleen samat kuin yllä.
- Changes - kohta tuo lisää vaihtelua tuloksiin. pid: kertoo prosessin tunnisteen ja retcode palautuskoodin (Kaspersky 2024).
- Lopussa taas listattu tehdyt toimet ja niiden specsit.

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h1_viisikko.md#h-1-viisikko)

---

## f) Idempotentti. Anna esimerkki idempotenssista. 
Aja `salt-call --local` komentoja, analysoi tulokset, selitä miten idempotenssi ilmenee. 

Alkuun halusin selvitellä idempotenssin käsitettä selkeämmäksi. Luennolta jäi jo mieleen, että toiminto tulee suoritetuksi vain, jos sen lopputulos on eri kuin lähtötila. Toisesta suunnasta tarkasteltuna toimintoa ei siis suoriteta, mikäli alku ja lopputilanne on sama. Saltstack sivulla todetaan että Saltin määritellessä tilan olevan jo toivotunlainen, ei muutoksia tehdä lainkaan. (Saltstack 2016)

Aiemmin olin luonut tiedoston /tmp/kaditestaa jonka palaute oli:
>  ![a-007](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h1-007.png)

Suoritan komennon `sudo salt-call --local -l info state.single file.managed /tmp/kaditestaa` uudelleen ja lopputulos on:
>  ![a-011](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h1-011.png)

Eli kommenttiosiossa maininta, että kyseinen tiedosto on olemassa ja ei muutoksia tehty. Ajoin komennon lukuisia kertoja ja lopputulos aina sama, vaikka funktio saatiin onnistuneesti toteutettua. Eli komento oli idempotentti.
>  ![a-012](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h1-012.png)

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h1_viisikko.md#h-1-viisikko)

---

## g) Tietoa koneesta. 
Kerää tietoja koneesta Saltin grains.items -tekniikalla. Poimi kolme kiinnostavaa kohtaa, näytä tulokset 'grains.item osfinger virtual' ja analysoi ne.

- Aloitin ao. komennolla, joka tulosti kattavasti käyttämäni virtuaalikoneen tiedot.
  
      sudo salt-call --local grains.items
- Seuraavaan komentoon poimin kolme nostoa.

      sudo salt-call --local grains.item  lsb_distrib_description kernel biosreleasedate
  Palautteena sain seuraavat:
  > ![a-013](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h1-013.png)
  - BIOS julkaisupäivä 2006, tämä tarkoittaa Linuxin Biosia.
  - Kernel - Linux
  - käyttöjärjestelmän kuvaus - Debian GNU/Linux 11 Bullseye
 
  [Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h1_viisikko.md#h-1-viisikko)

  ---

## Lähteet

Karvinen T/a. Create a Web Page Using Github, 2023. Luettavissa: https://terokarvinen.com/2023/create-a-web-page-using-github/. Luettu 31.03.2023. 

Karvinen T/b. Run Salt command locally 2023. Luettavissa: https://terokarvinen.com/2021/salt-run-command-locally/. Luettu 31.03.2024

Karvinen T/c. Raportin kirjoittaminen, 2023. Luettavissa: https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/. Luettu 31.03.2024.

Kaspersky How to get a Process Identifier (PID or Process ID) in Windows, 2023. Luettavissa: https://support.kaspersky.com/common/windows/6325. Luettu 31.03.2024.

Salt Stack, salt.states.cmd. Luettavissa: https://salt-zh.readthedocs.io/en/latest/ref/states/all/salt.states.cmd.html. Luettu 31.03.2024.

Salt Stack, Create a salt state, 2016. Luettavissa: https://docs.saltproject.io/en/getstarted/fundamentals/states.html. Luettu 31.03.2024.

Syrjä K. h1 Oma Linux, 2024. Luettavissa https://github.com/syjaka/Linux-Palvelimet-2024/blob/main/h1_OmaLinux.md#1-
raportointiohjeen-tiivistelm%C3%A4. Luettu 31.03.2024.

Syrjä K. h5 Uudestaan, 2024. Luettavissa;: https://github.com/syjaka/Linux-Palvelimet-2024/blob/main/h5_Uudestaan.md#kertaus-on-opintojen-%C3%A4iti. Luettu 31.03.2024.
