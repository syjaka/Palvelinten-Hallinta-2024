# Keskeneräinen

# h3 Toimiva versio

x) [Lue ja tiivistä]()

a) [ Online]()

b) [ Dolly]()

c) [ Doh!]() 

d) [ Tukki]()

e) [ Suolattu rakki]()

f) [ Vapaaehtoinen ykkönen - Se toinen järjestelmä]() 

g) [ Vapaaehtoinen kakkonen -  Yhteistyöbonus, eli ota kaveri mukaan]()

y) [ Käyttöympäristö]()

z) [ Alkutoimet]()

---

## x) Lue ja tiivistä. 

(Tässä x-alakohdassa ei tarvitse tehdä testejä tietokoneella, vain lukeminen tai kuunteleminen ja tiivistelmä riittää. Tiivistämiseen riittää muutama ranskalainen viiva. Kannattaa lisätä mukaan myös jokin oma havainto, idea tai kysymys.)

1 . [Chacon and Straub 2014: Pro Git, 2ed: 1.3 Getting Started - What is Git?](https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F)

 Kirjan kappaleessa 1.3 opetetaan Gitin perusteita toiminnan logiikasta ja Gitin eroista muihin varsionhallintajärjestelmiin. Tekstissä tuodaan esiin Gitin ainutlaatuisuutta tavassa käsitellä datan muutoksia enemmänkin tiedostojen tilannevedoksina, kuin aina uusina tiedostoina ja tiedostoina tehdyistä muutoksista. 
 - Suuri osa gitin muutoksista toimii paikallisesti, mikä nopeuttaa työskentelyä ja vapauttaa serveriyhteyden välttämättömyydestä.
 - Datan eheys varmistetaan käyttämällä SHA-1 hash tarkistussummaa.
 - Gitin tiedostot voivat olla kolmessa tilassa; muokattu, staged ja committed.


2. Gitin käyttö on lähinnä 'git add . && git commit; git pull && git push'. 
  -Selitä tuon komennon jokainen osa. Käytä apuna itse valitsemiasi lähteitä ja viittaa niihin.

   1. *git add*
    - `git add` Kun projektin tehdään muutoksia ne tulee "manuaalisti" sisällyttää seuraavaan committiin, eli lavastaa commitoitavaksi. Tämä tapahtuu  `git add`-komennolla. Komennon seurauksena git on päivittänyt indeksinsä vastaamaan komennon suorittamisen aikaista tilaa. Kyseisen komennon voi suorittaa useita kertoja ennen varsinaista committia. (Git documentation -a 2024)
   2. `git commit` On luontainen seuraus edelliselle komennolle joka on lavastanut muutokset commitoitavaksi. Eli komento luo uuden commitin joka sisältää nykyisen indexin ja annetun lokiviestin commitista. Uusin kommit on yleensä nykyisen haaran kärki ja haara päivitetään automaattisesti osoittamaan siihen. (Git documentation - b 2024)
   3. `git pull` - komento yhdistää muutokset etävarastosta paikalliseen varaston nykyiseen haaraan. Mikäli haarat ovat erkaantuneet tulee haarat sovittaa yhteen `rebase` tai `--no rebase` toiminnoilla (Git documentation - c 2024).
   4. `git push` päivittää etävarastot käyttäen paikallisia varastoja. Komennon yhteydessä on annettava toivottuja konfiguraatioita tai komentorivin määrityksiä komennolla. Mikäli näitä ei anneta, työnnetään nykyinen haara vastaavaan ylähaaraan. Jos ylähaaran nimi ei vastaa paikallista keskeytetään komento (Git documentation - d 2024).

   
4. Varaston [terokarvinen/suolax/](https://github.com/terokarvinen/suolax/) historia - 11.4 klo 12.45 - 13.30 EET
  - eli loki ja muutokset. Kätevimmin komentokehotteesta 'git clone https://github.com/terokarvinen/suolax.git; cd suolax/; git log --patch --color|less -R'. Wepistäkin saattaa onnistua kliksuttelemalla "Commits". (Karvinen 2024)

  Tein tehtävän komentorivin kautta.
  1. Avasin ssh yjteyden aiemmin Vagrantilla luotuun virtuaalikoneeseen joka sijaitsi koneeni kotihakemistossa. komennolla `vagrant ssh`. Koneelle oli git asennettu jo tunnilla.
  2. Etäyhteyden avauduttua siirryin `cd code ` - hakemistoon, annoin komennon `git clone https://github.com/terokarvinen/suolax.git` ja siirryin komennot tuomaan suolax hakemistoon `cd suolax`.
    ![h3-001]()
  3. Komento `git log --patch --color|less -R` tulosti kyseisen varaston historian.
  4. Tehtävänannossa ei ollut tarkennusta mitä tällä historialla olisi tarkoitus tehdä. Koska historiaa on useampi sivu, en lähde kaikke analysoimaan, mutta alla muutama:
    ![h3-002]()
    - Kyseisessä lokissa on aluksi tehdyn commitin SHA-1-arvo (40 merkkiä sisältävä hexadesimaalinumero). Tällä git tunnistaa jokaisen commitin yksilöllisesti.
    - Seuraavaksi näkyy tekijä *Author* ja ajankohta *Date*.
    - Initial commit kertoo että kyseessä on ensimmäinen tallennus, eli tämä oli kyseisen varaston luonnista syntynyt loki.
    - Seuraavilla riveillä kerrotaan lisenssitiedon lisäämisestä, lisättyjen rivien määrä, sekä viimeiseksi vihreällä koko lisätty teksti. Kuvakaappauksessa on vain kaksi ensimmäistä riviä lisenssistä mutta rivit siis jatkuvat seuraavat 672 riviä lisää.
    - Lisenssitekstin jälkeen tulee vielä README-tiedostoa koskeva lisenssitiedoston lisäämistä vastaava info.

  ![h3-003]()
 - Tässä lokissa on pääpiirteissään vastaavat tiedot kuin edellisessä.
 - Poikkeuksena kommitille annettu message " Improve ysage instructions"
 - Punaisella lokissa näkyy "poistettu" rivi ja vihreällä "lisätty". Eli jokainen muutettu rivi tulostuu aina konaisuudessaan, vaikka muutos olisi pelkän pisteen lisääminen.
 - Vertailun vuoksi alla githubista poimittu sama loki.
  ![h03-004]()

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_toimiva_versio.md#h3-toimiva-versio)

---

## y) Käyttöympäristö
Tehtävä toteutettiin MacBook Retina 12-inch, koneella jossa, host OS on Ventura 13.6.1 käyttöjärjestelmä Suomen maa-asetuksilla ja suomen kielellä. Koneessa on 1,3GHz kaksiytiminen Intel Core i5 prosessori ja 8Gt 1867 MHz LPDDR3 muistia. Näytönohjain on Intel HD Graphics 615 jossa VRAM 1536 Mt.

---

## z) Alkutoimet
Koneen ja pääte-työkalun käynnistys.

---

Kaikki seuraavien osion tehtävänannot ovat peräisin Tero Karvisen - [Infra As a Code - Palvelinten hallinta 2024 kurssisivulta](https://terokarvinen.com/2024/configuration-management-2024-spring/#h3-toimiva-versio).

## a) Online. 
Tee uusi varasto GitHubiin (tai Gitlabiin tai mihin vain vastaavaan palveluun). Varaston nimessä ja lyhyessä kuvauksessa tulee olla sana "summer". Aiemmin tehty varasto ei kelpaa. (Muista tehdä varastoon tiedostoja luomisvaiheessa, esim README.md ja GNU General Public License 3)

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_toimiva_versio.md#h3-toimiva-versio)

---

## b) Dolly
Kloonaa edellisessä kohdassa tehty uusi varasto itsellesi, tee muutoksia omalla koneella, puske ne palvelimelle, ja näytä, että ne ilmestyvät weppiliittymään.

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_toimiva_versio.md#h3-toimiva-versio)

---

## c) Doh! 
Tee tyhmä muutos gittiin, älä tee commit:tia. Tuhoa huonot muutokset ‘git reset --hard’. Huomaa, että tässä toiminnossa ei ole peruutusnappia.

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_toimiva_versio.md#h3-toimiva-versio)

---

## d) Tukki 
Tarkastele ja selitä varastosi lokia. Tarkista, että nimesi ja sähköpostiosoitteesi näkyy haluamallasi tavalla ja korjaa tarvittaessa.

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_toimiva_versio.md#h3-toimiva-versio)

---

## e) Suolattu rakki
Aja Salt-tiloja omasta varastostasi. (Salt tiedostot mistä vain hakemistosta "--file-root teronSaltHakemisto". Esimerkiksi 'sudo salt-call --local --file-root srv/salt/ state.apply', huomaa suhteellinen polku.)

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_toimiva_versio.md#h3-toimiva-versio)

---

## f) Vapaaehtoinen ykkönen - Se toinen järjestelmä
Kokeile Gittiä eri käyttöjärjestelmällä kuin sillä, millä teit muut harjoitukset. Selitä niin, että kyseistä järjestelmää osaamatonkin onnistuu. Mahdollisuuksia on runsaasti: Debian, Fedora, Windows, OSX...

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_toimiva_versio.md#h3-toimiva-versio)

---

## g) Vapaaehtoinen kakkonen - Yhteistyöbonus, eli ota kaveri mukaan
Anna kaverillesi (tai alter egollesi) oikeus kirjoittaa varastoosi (commit access). Tehkää molemmat muutoksia varastoon gitillä.

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_toimiva_versio.md#h3-toimiva-versio)

---

## Lähteet

Chacon and Straub 2014: Pro Git, 2ed: 1.3 Getting Started - What is Git? Luettavissa: https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F. Luettu 11.04.2024

Git documentation - a, git-add 2024. Luettavissa: https://git-scm.com/docs/git-add. Luettu 11.04.2024

Git documentation - b, git-commit 2024. Luettavissa: https://git-scm.com/docs/git-commit. Luettu 11.04.2024

Git documentation - c, git-pull 2024. Luettavissa: https://git-scm.com/docs/git-pull. Luettu 11.04.2024

Git documentation - d, git-push 2024. Luettavissa: https://git-scm.com/docs/git-pull. Luettu 11.04.2024


Tero Karvinen, Infra as Code, 2024. Luettavissa: https://terokarvinen.com/2024/configuration-management-2024-spring/. Luettu 11.04.2024
