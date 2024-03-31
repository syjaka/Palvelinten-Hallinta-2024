# KESKENERÄINEN

# h 1 Viisikko

x) [Lue ja tiivistä](https://github.com/syjaka/Palvelinten-Hallinta-2024/new/main#x-lue-ja-tiivist%C3%A4)

a) [Hello Mac Salt World]()

b) [Hello Vagrant]()

c) [Tee Vagrantilla uusi Linux Virtuaalikone]()

d) [Asenna Salt (salt-minion) Linuxille]()

e) [Viisi tärkeintä]()

f) [Idempotentti]()

g) [Tietoa koneesta]()

y) [Käyttöympäristö]()

z) [Alkutoimet]()

## x) Lue ja tiivistä

---
### Run Salt command locally - Karvinen 2023

> - Kyseisessä kirjoituksessa opastetaan miten salt komentoja voidaan ajaa paikallisesti ja nähdä tulokset välittömästi. Esitellyt komennot siis opastavat kuinka Saltia voidaan käyttää paikallisesti yksittäisten hallintatehtävien suorittamiseksi ilman verkon yli tapahtuvaa master-slave arkkitehtuuria. Alkuun opastetaan Saltin-minionin asennus muutamalla komennolla, jonka jälkeen on aina hyvä tarkistaa asennuksen onnistuminen.
> - Seuraavaksi mainitaan että paketinhallintasovellus tulee olla asennettu ja esitellään tree-paketin asennus ja poistokomennot.
> - Kaikki Linuxin asetukset ovat tekstitiedostoja, joten seuraavaksi luotiin/tarkistettiin tmp/hellotero tiedoston olemassaolo, sekä luotiin tai tarkistettiin tmp/moitero tiedoston olemassaolo ja tallennettiin sinne sisällöksi `foo`.
> - `$ sudo salt-call --local -l info state.single file.absent /tmp/hellotero`varmistaa että tmp/hellotero tiedostoa ei ole olemassa.
> - Palveluiden hallinta
>   - `$ sudo salt-call --local -l info state.single service.running apache2 enable=True` Varmistaa että Apache2 on käynnissä ja `$ sudo salt-call --local -l info state.single service.dead apache2 enable=False` tomii päinvastoin.
> - Seuraavaksi opastetaan käyttäjänhallintaa eli käyttäjän luonnin tai poiston.
> - Komentojen suorittaminen:
>    - `$ sudo salt-call --local -l info state.single cmd.run 'touch /tmp/foo' creates="/tmp/foo"`  luo  tyhjän tiedoston, mikäli sitä ei vielä ole. Komennossa siis esitetään idempotenssin käsitettä, eli suoritetaan vain jos määritetty ehto ei täyty. 
> Viimeiseksi  `$ sudo salt-call --local sys.state_doc` komennolla saadaan näytettyä dokumentaatio saatavilla olevista Salt state-toiminnoista paikallisesti (local). (Karvinen/b 2023)

### Create Web page using Github - Karvinen 2023

> Artikkelissa opastetaan vaihe vaiheelta verkkosivun julkaiseminen Githubissa. Alkuun palveluun tulee rekisteröityä, jonka jälkeen luodaan repository. Luotuun repositoryyn päästään luomaan eri tiedostoja MarkDownilla eli tiedostosto tallennetaan .md päätteellä. Artikkelissa kerrotaan myös md alkeet, joilla saadaan aikaan helposti luettavaa jäsennettyä tekstiä. (Karvinen/a)

### Raportin kirjoittaminen - Karvinen 2023

> Koska olen tämän tiivistelmän kirjoittanut jo edellisellä kurssilla ja pyörää ei kannattane keksiä uudestaan, käytän tämän palautukseen aiemman [tiivistelmääni](https://github.com/syjaka/Linux-Palvelimet-2024/blob/main/h1_OmaLinux.md#1-raportointiohjeen-tiivistelm%C3%A4) lyhentämättömänä. 

Raportin kirjoittaminen

Hyvä raportointitapa tehostaa työskentelyä ja oppimista jäsentämällä ja selkeyttämällä koko työskentelyprosessia. Hyvään raportointiin kuuluu muutamia peruselementtejä:

Toistettavuus, Hyvän raportin perusteella koko työnkulku pitäisi olla toistettavissa samassa ympäristössä.
1. Täsmällisyys, Hyvässä raportissa on selkeästi kirjattu kaikki annetut komennot ja niiden seuraukset.
2. Helppolukuisuus, Hyvää raporttia on helppo lukea sen järjestelmällisen rakenteen ja hyvän kielen ansiosta.
3. Hyvässä raportissa on lähteet listattu perusteellisesti.
Pahimpia mokia raporttia kirjoittaessa ovat asioiden keksiminen sekä plagiointi. Tärkeää on tehdä annetut tehtävät ja dokumentoida tämä helppolukuisesti ja selkeästi. (Karvinen/c 2024)

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/new/main#h-1-viisikko)

---

## y) Käyttöympäristö
> Tehtävä toteutettiin MacBook Retina 12-inch, koneella jossa host OS on Ventura 13.6.1 käyttöjärjestelmä Suomen maa-asetuksilla ja suomen kielellä. Koneessa on 1,3GHz kaksiytiminen Intel Core i5 prosessori ja 8Gt 1867 MHz LPDDR3 muistia. Näytönohjain on Intel HD Graphics 615 jossa VRAM 1536 Mt.
> Guest OS on Debian GNU/Linux 12 (bookworm) joka pyörii Virtual Boxin 7.0 versiossa.

## z) Alkutoimet

## a) Hello Mac Salt World
> Hello Windows/Mac Salt World! Näytä jollain Salt-komennolla, että olet onnistunut asentamaan Saltin (salt-minion) Windowsille tai Macille. Jos et ole vielä asentanut Saltia, raportoi myös asennus. (Karvinen 2024)
Koska asensin Saltin jo tunnilla [saltproject](https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/macos.html#install-macos) ohjeiden mukaan, en sitä enää tässä dokumentoi.
Saltin Onnistunut asennus näkyy ao. kuvassa:
> ![a-001]()

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/new/main#h-1-viisikko)

---

## b) Hello Vagrant
> Hello Vagrant! Osoita jollain komennolla, että Vagrant toimii. Jos et ole vielä asentanut niitä, raportoi myös Vagrant ja VirtualBox asennukset. (Karvinen 2024)

Itse Vagrant tuli asennettua viime kurssilla ja siitä raporttia [täällä](https://github.com/syjaka/Linux-Palvelimet-2024/blob/main/h5_Uudestaan.md#m-vagrant) (Syrjä 2024).
> ![a-002]()

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/new/main#h-1-viisikko)v

---

## c) Tee Vagrantilla uusi Linux-virtuaalikone













## Lähteet

Karvinen T/a. Create a Web Page Using Github, 2023. Luettavissa: https://terokarvinen.com/2023/create-a-web-page-using-github/. Luettu 31.03.2023. 
Karvinen T/b. Run Salt kommand locally 2023. Luettavissa: https://terokarvinen.com/2021/salt-run-command-locally/. Luettu 31.03.2024
Karvinen T/c. Raportin kirjoittaminen, 2023. Luettavissa: https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/. Luettu 31.03.2024
Syrjä K. h1 Oma Linux, 2024. Luettavissa https://github.com/syjaka/Linux-Palvelimet-2024/blob/main/h1_OmaLinux.md#1-
raportointiohjeen-tiivistelm%C3%A4. Luettu 31.03.2024.
Syrjä K. h5 Uudestaan, 2024. Luettavissa;: https://github.com/syjaka/Linux-Palvelimet-2024/blob/main/h5_Uudestaan.md#kertaus-on-opintojen-%C3%A4iti. Luettu 31.03.2024.
