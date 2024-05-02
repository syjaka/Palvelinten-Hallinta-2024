# KESKENERÄINEN

# h6 Benchmark


a) Paketti Windowsia

b) Benchmark

c) Testbench

d) Viisi ideaa

x) Lue ja tiivistä

y) Käyttöympäristö



## x) Lue ja tiivistä

Windows Package Manager: 
- Introduction
  - Salt tarjoaa Windowsille paketinhallintatyökalun jota voi soveltaa etä ympäristöjen hallinnassa (vastaava kuin Linuxin `apt`).
  - Tätä toteutetaan paketinmääritystiedoston avulla jos sisältää mm ohjelmistopaketin nimen , sekä sen lataussijainnin. Näitä tiedostoja voi hostata Git-repoissa.
  - Pakettien asentamiseen käytetyt sls-tiedostot tulee kloonata olestusvarastosta **salt-winrepo-ng**.
  - `pkg.install`asentaa paketin ja `pkg.installed`tarkistaa paketin asennuksen tilan.
- Install libraries
  - `git python` tai `git pygit` asentaminen mahdollistaa sujuvan Git-varastojen käsittelyn mikäli käytät Saltin Git-varaston hostaamia paketinmääritystiedostoja.
- Populate the local Git repository
  - `salt-run winrepo.update_git_repos` kloonaa **salt-winrepo-ng** repon Salt-masterille **winrepo_dir_ng**:n määrittelemään sijaintiin. 
  - `salt-call --local winrepo.update_git_repos` komennolla "itsenäinen" minon voi suorittaa saman.
- Update minion database
  - `pkg.refresh_db` päivittää minionien tietokannan pakettimäärittelytiedostoja varten. Komento voidaan suorittaa masterilta kaikille minioneille muododssa `salt -G 'os:windows' pkg.refresh_db`tai itsenäisellä minionilla muodossa `salt-call --local pkg.refresh_db`.
- Install software package - Alla luetelluissa komennoissa on sama syntaksi masterille tai itsenäisellä minionilla, kuin yllä esitellyt.
  - Kun olketusvarastot on kloonattu ja tietokannat päivitetty voidaan softaa asentaa masterilta `salt * pkg.install 'firefox_x64'` tai itsenäisellä minionilla `salt-call --local pkg.install "firefox_x64"`.
- Usage
  - `pkg.list_pkgs` Listaa kaikki järjestelmään asennetut paketit. Komennon tulosteesta voi päätellä onko asennettu ohjelma Saltin kautta hallittavissa vai ei, eli löytyyko paketin vastaavuus winrepo-tietokannasta.
  - `pkg.list_available` Listaa saatavilla olevista versiot tietylle paketille. Haluttu paketin nimi lisätään komennon loppuun.
  - `pkg.install` Asentaa komennossa nimetyn paketit/paketit. Paketin nimeen voi ölisätä vielä halutun versiotiedon.
  - `pkg.remove` Poistaa komennossa nimetyn paketin asennuksen.
  (Salt 2024)

##y) Käyttöympäristö

Tehtävä toteutettiin MacBook Retina 12-inch, koneella jossa, host OS on Ventura 13.6.1 käyttöjärjestelmä Suomen maa-asetuksilla ja suomen kielellä. Koneessa on 1,3GHz kaksiytiminen Intel Core i5 prosessori ja 8Gt 1867 MHz LPDDR3 muistia. Näytönohjain on Intel HD Graphics 615 jossa VRAM 1536 Mt.

Koneeseen asennettu Vagrant versio on 2.4.1.
z- kohdassa määritetyt virtuaalikoneet ovat Linux Bullseye 5.10.0-28-amd64.


## a) Paketti Windowsia
Asenna Windowsiin tai Macciin ohjelmia Saltin pkg.installed -funktiolla (Karvinen 2024).

Tehtävän suoritus 02.05.2024 klo 11.35 - 

1. Aloitin tmuxin asennuksella, sillä koen sen olevat hyödyllinen lisä CLI-työskentelyyn
   -  `brew install tmux` kännisti asennuksen. Sen valmistuttua sain palautteen:
      !h6-001
   -  `tmux` käynnisti ja uusia istuntoja sai joko `ctrl+b ja "`=vaaka ja `ctrl+b ja %`= pysty. `ctrl+b ja nuoli`vaijtaa paneelia ja `ctrl+b ja  x`sulkee paneelin. `ctrl+b ja s` luetteloi istunnon paneelit ja `exit` lopettaa istunnon.
   -  Hyvin toimi ja vaikutti hyödylliseltä (Choi 2028)
2. Seuraavaksi asensin vielä `brew install cowsay speedtest-cli`
Kaikki näytti toimivan mainiosti.
!h6-002

Takaisin ylös
___ 

## b) Benchmark

Etsi 3-7 keskitetyn hallinnan projektia, esimerkiksi tämän kurssin "Oma moduli" lopputyötä. Työn tulee olla modernia keskitettyä hallintaa (idempotentti, infra koodina, yksi totuus). Esimerkiksi pelkkä shell script ei kelpaa. Työ saa käyttää mitä vain työkalua, esim Salt, Puppet, Ansible, Chef, Conftero, CFEngine (Karvinen 2024).
#### 1. [samikul - ph-moduuli Githubissa](https://github.com/samikul/ph-moduuli)

1. Tarkoitus
   - Tämän moduulin taerkoitus on konfiguroida palvelin valmiiksi Flask web-applikaatioiden testikehitykseen ja tuotantoon.
3. Lisenssi
   - Lisenssi löytyy heti repon tiedostoissa sekä README tiedoston infosta. Työhön on valittu GNU - General Public License (GPL) joka on vapaiden ohjelmistojen lisenssi. Se antaa käyttäjille oikeuden käyttää jakaa ja muokata ohjelmistoa. Lisenssi myös velvoittaa käyttäjäänsä säilyttämään alkuperäisen tekijän tietoa, sekä jakamaan muokatut versiot samaa lisenssiä käyttäen. Pääasiallinen juridinen vaikutus on se, että mikäli hyödynnät lisenssin vaikutuksen alaista materiaalia, sitoudut samalla noudattamaan sen ehtoja. 
5. Moduulin tekijä on Sami Kulonpää ja viosi 2021
6. Riippuvuudet:
   - Moduuli on toteutettu Linux-käyttöjärjestelmällä. Varsinaista kehitysversiota en kyennyt vahvistamaan, sillä varsinainen työn raportointi ei anetusta linkistä, eikä Samin verkkosivuilta löytynyt. Lisäksi moduuli vaati Salt-Tackin asennuksen ja käyttöönoton.
8. Kiinnostavaa:
   - Työssä kiinnostavaa oli sen aihe, sillä se on juuri samaa, mitä olemme kurssilla harjoitelleet. Tässä työssä on tiivistettynä kaikki tämän ja Linux-palvelinkurssien hyödyt kauniiseen pakettiin joka tekee työstä myös opiskelijan näkökulmasta hyödylliusen. Lisäksi työn tarkoitus vastaa palttiarallaa sisällöltään sitä, mitä itse olin pyöritellyt oman moduulin aiheeksi. Tämä tietenkin ymmärrettävää, sillä kuten sanottu, työtiivistää ja tarjoilee koko opitun sisällön. 
10. Avoimet kysymykset:
    - Miten toteuttaa oma moduuli jotta siitä syntyy jollain tasolla originaali ja mahdollisesti hyödyllinen, eikä vain tehdyn toisintoa?
(Kulonpää 2021)

1. Tarkoitus
2. Lisenssi - Missä tuossa työssä se lisenssi lukee - Mitä lisenssi tarkoittaa, eli pääasiallinen jurdiinen vaikutus
3. Tekijä ja vuosi
4. Riippuvuudet: Alusta (käyttöjärjestelmä, jokin tietty pilvi...), verkkoympäristö tms.
5. Kiinnostavaa, esim - Hyödyllinen lopputulos - Kiinnostava tekniikka, esim. jokin tapa käyttää Saltia
6. Avoimet kysymykset ja muut huomiot

1. Tarkoitus
2. Lisenssi - Missä tuossa työssä se lisenssi lukee - Mitä lisenssi tarkoittaa, eli pääasiallinen jurdiinen vaikutus
3. Tekijä ja vuosi
4. Riippuvuudet: Alusta (käyttöjärjestelmä, jokin tietty pilvi...), verkkoympäristö tms.
5. Kiinnostavaa, esim - Hyödyllinen lopputulos - Kiinnostava tekniikka, esim. jokin tapa käyttää Saltia
6. Avoimet kysymykset ja muut huomiot

Listaa kustakin
Tarkoitus (eli "mitä hyötyä tästä on" eli "business purpose" eli "miksi haluaisin asentaa tämän".)
Kyllä näin: (business purpose): "Robotti kuljettaa minulla jääkaapista limpparia"
Ei näin, tekniikoiden luetteleminen ei ole sovelluksen tarkoitus: "ESP32 ja Arduino ohjaavat servoja, jotka LIDAR:lla väistelevät kappaleita C++-ohjelmalla; tartuntakomponentti käyttää PDI-säädintä..."
Lisenssi
Lisenssin nimi
Missä tuossa työssä se lisenssi lukee
Mitä lisenssi tarkoittaa, eli pääasiallinen jurdiinen vaikutus
Tekijä ja vuosi
Riippuvuudet: Alusta (käyttöjärjestelmä, jokin tietty pilvi...), verkkoympäristö tms.
Kiinnostavaa, esim
Hyödyllinen lopputulos
Kiinnostava tekniikka, esim. jokin tapa käyttää Saltia
Avoimet kysymykset ja muut huomiot

## c) Testbench
Aja toisen tekemä tila.
Valitse jokin edellisessä kohdassa tutkimasi moduli. Perustele valintasi.
Tarkista koodi.
Lataako koodi binäärejä? Lataako paketinhallinnan ulkopuolelta? Onko luotettavia ohjelmistolähteitä?
Aja koodi. Käytä tarvittaessa virtuaaliympäristöä tai muuta eristystä.
Testaa lopputulos.
Ota ruutukaappauksia sopivassa laajuudessa.
Kommentoi ja arvioi modulia.
Modulin kaikkia bugeja ei tarvitse korjata, tarkoitus on ajaa modulia ja arvioida sitä.
Jos jokin moduli vaikuttaa täysin toimimattomalta, kirjaa ylös yrityksesi ja kokeile toista modulia.


## d) Viisi ideaa
Listaa viisi ideaa omalle modulille, kurssin lopputehtävälle. Modulilla tulee olla tarkoistus. Sen ei tarvitse silti ratkaista mitään oikeaa liiketoiminnan ongelmaa, vaan tarkoitus voi olla keksitty. Kunkin idean kuvaukseen riittää yksi virke. Ensi kerralla katsomme yhdessä aiheen valintaa ja sopivia vinkkejä. Tarvitsen pohjaksi omia ideoitasi, jotta voin antaa hyödyllisiä ja juuri sinulle sopivia neuvoja.

## Lähteet

Choi J. Install tmux on OSX and Basics Commands for Beginners, 2018. Luettavissa: Install tmux on OSX and Basics Commands for Beginners. Luettu 02.05.2024.

Karvinen T. Infra as Code - Palvelinten hallinta 2024. Luettavissa: https://terokarvinen.com/2024/configuration-management-2024-spring/#h6-benchmark. Luettu 02.05.2024.

Kulonpää S. ph-moduuli 2021. Luettavissa: https://github.com/samikul/ph-moduuli. Luettu 02.05.2024.

Salt Project - Windows package manager 2024. Luettavissa: https://github.com/therealhalonen/PhishSticks/blob/master/notes/ollikainen/windows.md. Luettu 02.05.2024
