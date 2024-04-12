
# h3 Toimiva versio

x) [Lue ja tiivistä](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_Toimiva_versio.md#x-lue-ja-tiivist%C3%A4)

a) [ Online](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_Toimiva_versio.md#a-online---11042024-klo-1330---1343-eet)

b) [ Dolly](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_Toimiva_versio.md#b-dolly---11042024-klo-1345---1406-eet)

c) [ Doh!](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_Toimiva_versio.md#c-doh---11042024-klo-1418---1433-eet) 

d) [ Tukki](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_Toimiva_versio.md#d-tukki---11042024-klo-1445---1505-eet)

e) [ Suolattu rakki](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_Toimiva_versio.md#e-suolattu-rakki---11042024-klo-1510---1740-eet)

f) [ Vapaaehtoinen ykkönen - Se toinen järjestelmä](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_Toimiva_versio.md#f-vapaaehtoinen-ykk%C3%B6nen---se-toinen-j%C3%A4rjestelm%C3%A4---12042024-klo-0945---1025-eet) 

g) [ Vapaaehtoinen kakkonen -  Yhteistyöbonus, eli ota kaveri mukaan](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_Toimiva_versio.md#g-vapaaehtoinen-kakkonen---yhteisty%C3%B6bonus-eli-ota-kaveri-mukaan---12042024-klo-1025---1049-eet)

y) [ Käyttöympäristö](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_Toimiva_versio.md#y-k%C3%A4ytt%C3%B6ymp%C3%A4rist%C3%B6)

z) [ Alkutoimet](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_Toimiva_versio.md#z-alkutoimet)

---

## x) Lue ja tiivistä. 

### 1. [Chacon and Straub 2014: Pro Git, 2ed: 1.3 Getting Started - What is Git?](https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F)
   - Kirjan kappaleessa 1.3 opetetaan Gitin perusteita sen toiminnan logiikasta ja Gitin eroista muihin versionhallintajärjestelmiin. Tekstissä tuodaan esiin Gitin ainutlaatuisuutta tavassa käsitellä datan muutoksia enemmänkin tiedostojen tilannevedoksina, kuin aina uusina tiedostoina ja tiedostoina tehdyistä muutoksista.
   - Suuri osa Gitin muutoksista toimii paikallisesti, mikä nopeuttaa työskentelyä ja vapauttaa serveriyhteyden välttämättömyydestä.
   - Datan eheys varmistetaan käyttämällä SHA-1 hash tarkistussummaa.
   - Gitin tiedostot voivat olla kolmessa tilassa; muokattu, staged ja committed.


### 2. Gitin käyttö on lähinnä 'git add . && git commit; git pull && git push'. 
Selitä tuon komennon jokainen osa. Käytä apuna itse valitsemiasi lähteitä ja viittaa niihin.

   - `git add` Kun projektin tehdään muutoksia, tulee ne "manuaalisti" sisällyttää seuraavaan committiin, eli lavastaa commitoitavaksi. Tämä tapahtuu `git add`-komennolla. Komennon seurauksena git on päivittänyt indeksinsä vastaamaan komennon suorittamisen aikaista tilaa. Kyseisen komennon voi suorittaa useita kertoja ennen varsinaista committia. (Git documentation -a 2024)
   - `git commit` On luontainen seuraus edelliselle komennolle, joka on lavastanut muutokset commitoitavaksi. Eli komento luo uuden commitin joka sisältää nykyisen indexin ja annetun lokiviestin commitista. Uusin kommit on yleensä nykyisen haaran kärki ja haara päivitetään automaattisesti osoittamaan siihen. (Git documentation - b 2024)
   - `git pull` - komento yhdistää muutokset etävarastosta paikalliseen varaston nykyiseen haaraan. Mikäli haarat ovat erkaantuneet tulee haarat sovittaa yhteen `rebase` tai `--no rebase` toiminnoilla (Git documentation - c 2024).
   - `git push` päivittää etävarastot käyttäen paikallisia varastoja. Komennon yhteydessä on annettava toivottuja konfiguraatioita tai komentorivin määrityksiä komennolla. Mikäli näitä ei anneta, työnnetään nykyinen haara vastaavaan ylähaaraan. Jos ylähaaran nimi ei vastaa paikallista keskeytetään komento (Git documentation - d 2024).

   
### 3. Varaston [terokarvinen/suolax/](https://github.com/terokarvinen/suolax/) historia - 11.4 klo 12.45 - 13.30 EET
eli loki ja muutokset (Karvinen 2024).

   - Tein tehtävän komentorivin kautta.
   1. Avasin ssh yhteyden aiemmin Vagrantilla luotuun virtuaalikoneeseen *Bookworm*, joka sijaitsi koneeni kotihakemistossa. Tein tämän komennolla `vagrant ssh`. Tälle koneelle oli Git asennettu jo tunnilla.
   2. Etäyhteyden avauduttua siirryin `cd code ` - hakemistoon (joka oli myös tunnilla luotu)
   3. Toin githubin opettajan repon tuonne hakemistoon kloonaamalla sen komennolla `git clone https://github.com/terokarvinen/suolax.git` ja siirryin komennot tuomaan suolax hakemistoon `cd suolax`.
    ![h3-001](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-001.png)
   4. Komento `git log --patch --color|less -R` tulosti kyseisen varaston historian.
   5. Tehtävänannossa ei ollut tarkennusta, mitä tällä historialla olisi tarkoitus tehdä. Päätin analysoida muutaman tapahtuman:    ![h3-002](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-002.png)
      - Kyseisessä lokissa on aluksi tehdyn commitin SHA-1-arvo (40 merkkiä sisältävä hexadesimaalinumero). Tällä git tunnistaa jokaisen commitin yksilöllisesti.
      - Seuraavaksi näkyy tekijä *Author* ja ajankohta *Date*.
      - Initial commit kertoo, että kyseessä on ensimmäinen tallennus, eli tämä oli kyseisen varaston luonnista syntynyt loki.
      - Seuraavilla riveillä kerrotaan lisenssitiedon lisäämisestä, lisättyjen rivien määrä, sekä viimeiseksi vihreällä koko lisätty teksti. Kuvakaappauksessa on vain kaksi ensimmäistä riviä lisenssistä, mutta rivit  jatkuvat seuraavat 1 672 riviä lisää.
      - Lisenssitekstin jälkeen tulee vielä README-tiedostoa koskeva lisenssitiedoston lisäämistä vastaava info joka kuuluu samaan committiin.

         ![h3-003](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-003.png)
      - Tässä lokissa on pääpiirteissään vastaavat tiedot kuin edellisessä.
      - Poikkeuksena commitille annettu message " Improve usage instructions"
      - Punaisella lokissa näkyy "poistettu" rivi ja vihreällä "lisätty". Eli jokainen muutettu rivi tulostuu aina kokonaisuudessaan, vaikka muutos olisi pelkän pisteen lisääminen.
      - Vertailun vuoksi alla githubista poimittu sama loki.
        ![h03-004](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-004.png)
(Karvinen Github 2024)

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_Toimiva_versio.md#h3-toimiva-versio)

---

## y) Käyttöympäristö
Tehtävä toteutettiin MacBook Retina 12-inch, koneella jossa, host OS on Ventura 13.6.1 käyttöjärjestelmä Suomen maa-asetuksilla ja suomen kielellä. Koneessa on 1,3GHz kaksiytiminen Intel Core i5 prosessori ja 8Gt 1867 MHz LPDDR3 muistia. Näytönohjain on Intel HD Graphics 615 jossa VRAM 1536 Mt.
- Koneeseen asennettu Vagrant versio on 2.4.1.
- Tehtävässä x.3 ja b on käytetty Linux bookworm 6.1.0-18-amd64
- muissa tehtävissä on käytetty Linux Bullseye 5.10.0-28-amd64

---

## z) Alkutoimet
Koneen ja pääte-ohjelman käynnistys.

---

Kaikki seuraavien osioiden tehtävänannot ovat peräisin Tero Karvisen - Infra As a Code - [Palvelinten hallinta 2024 kurssisivulta](https://terokarvinen.com/2024/configuration-management-2024-spring/#h3-toimiva-versio).

---


## a) Online - 11.04.2024 klo 13.30 - 13.43 EET.
Tee uusi varasto GitHubiin. Varaston nimessä ja lyhyessä kuvauksessa tulee olla sana "summer" (Karvinen 2024).

1. Omaan Githubiini kirjautuneena sivuston pääsivulta valitsin `new`
2. Avautuvasta ikkunasta annoin varastolle nimen *summer*. Jätin varaston näkyvyyden julkiseksi. Valitsin README-filen lisättäväksi, sekä valitsin lisenssiksi GNU General Public Licensen. Viimeistelin luonnin `Create repository`.
3. Lopputuloksena Githubissa on uusi repo nimeltään *summer*.
![h3-005](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-005.png)

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_Toimiva_versio.md#h3-toimiva-versio)

---

## b) Dolly - 11.04.2024 klo 13.45 - 14.06 EET
Kloonaa edellisessä kohdassa tehty uusi varasto itsellesi, tee muutoksia omalla koneella, puske ne palvelimelle, ja näytä, että ne ilmestyvät weppiliittymään (Karvinen 2024).

Jatkoin tässä tehtävässä työskentelyä samalla virtuaalikoneella kuin kohdassa x.

1. Kopioin repon etusivulla `code-painikkeen` local- välilehdeltä löytyvän repon SSH-osoitteen jonka liitin myöhemmin `git clone`-komentoon.
![h3-006](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-006.png)
2. Siirryin kotihakemistossa sijaitsevaan code hakemistoon `cd code`
3. Komennolla `git clone git@github.com:syjaka/summer.git` toin luodun repon paikalliseen virtuaalikoneeseeni.
![03-007](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-007.png)
4. `cd summer` siirryin kopioituun repoon.
5. `micro vamos` avasi microlla vamos nimisen tiedoston ja `ctrl+s` & `ctrl+q` tallensi la lopetti micron.
6. `git add . && git commit` tunkee tiedoston ja commitin etärepoon.
7. Paitsi ei tunkenutkaan, vaan vain "lavasti" ja teki commitin. Eli lisäsin myös `git push` komennon, ja homma toimi.
![h03-008](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h03-008.png)
8. Selaimessa aikaleimat  näyttivät erikoiselta. Lisenssi ja README oli lisätty noin puoli tuntia sitten ja juuri lisäämäni vamos 14 tuntia sitten.
9. Lokia tarkastellessa tämä selittyi. Virtuaalikoneeni oli vielä eilisessä (korjasin tämän vasta myöhemmin tehtävässä).
![h3-009](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-009.png)
   
[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_Toimiva_versio.md#h3-toimiva-versio)

---

## c) Doh! - 11.04.2024 klo 14.18 - 14.33 EET.
Tee tyhmä muutos gittiin, älä tee commit:tia. Tuhoa huonot muutokset ‘git reset --hard’. Huomaa, että tässä toiminnossa ei ole peruutusnappia (Karvinen 2024).

1. Tein aluksi tyhmän muutoksen `micro vamos` + muutos sisältöön + `git add .`.
2. Muutoksen teko näkyi `git status` komennolla.
3. Halusin nähdä myös muutoksen sisällön, jossa ChatGPT auttoi. `git diff --cached` toi esiin tehdyn muutoksen (ChatGpt 2024).
4. Lopuksi `git reset --hard` poisti tuon muutoksen.
![h3-010](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-010.png)

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_Toimiva_versio.md#h3-toimiva-versio)

---

## d) Tukki - 11.04.2024 klo 14.45 - 15.05 EET.
Tarkastele ja selitä varastosi lokia. Tarkista, että nimesi ja sähköpostiosoitteesi näkyy haluamallasi tavalla ja korjaa tarvittaessa (Karvinen 2024).

1. Varaston loki tuli esiin `git log --patch --color|less -R`.
![h3-011](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-011.png)
2. Analyysiä 
    - **Commit** on kyseisen commitin yksilöllinen tunniste eli SHA-1 arvo.
    - **Author** näytti nimeni ja meiliosoitteeni. Nämä säädin oikeaksi jo eilisellä tunnilla käyttäen komentoja `git config --global user.email "mun meili"` ja `git config --global user.name "mun nimi"`.
    - **Date** kertoi commitin ajankohdan. Tässä ekan ja tokan välillä ristiriita, sillä virtuaalikoneeni ei ollut ajan tasalla.
    - Seuraavaksi näkyi Commit messaget, tässä kahden commitin **initial commit** ja **add file vamos**.
    - **diff --git a/vamos b/vamos** identifioi tiedoston ennen ja jälkeen muutoksen.
    - **new file mode 100644** kertoi uudesta tiedostosta ja sen oikeuksista.
    - **index 0000000..64cbbea** viittasi tiedoston index-tilaan.
    - **+++ b/vamos** ja **+++ B/LICENSE** kertoi lisätyt tiedostot.
    - **@@ -0,0 +1 @@** ja **@@ -0,0 +1,674 @@** kertoi lisättyjen rivien lukumäärän ja viimeiseksi vihreällä näkyi lisätyt rivit sisältöineen.
    - Kuvassa jää **Initial commit** vajaaksi sillä lisenssin 1 674 rivin jälkeen siellä näkyy vielä commitin README-filen lisäysosuus.

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_Toimiva_versio.md#h3-toimiva-versio)

---

## e) Suolattu rakki - 11.04.2024 klo 15.10 - 17.40 EET.
Aja Salt-tiloja omasta varastostasi. (Salt tiedostot mistä vain hakemistosta "--file-root teronSaltHakemisto". Esimerkiksi 'sudo salt-call --local --file-root srv/salt/ state.apply', huomaa suhteellinen polku.) (Karvinen 2024).

Tämän osion lähteinä on käytetty 10.04.2024 luentomuistiinpanoja, sekä Tero Karvisen suolax-repoa, joka tehtiin luennolla. Muut lähteet ovat merkitty tekstiviitteisiin. 

Tähän tehtävään otin käyttöön viime viikon tehtävässä h2 luodun virtuaalikoneen k002, jossa Salt oli valmiina.
1. Aloitin asentamalla Gitin ja muuta, sekä Määrittämällä Githubin repon koneen käyttöön:
   - Siirryin emokoneellani kansioon `cd twohost` ja otin yhteyden koneeseen `vagrant  ssh k002`
   - Aloitin asentamalla Gitin ja muutamia muita ohjelmia:
     - `sudo apt-get update` ja `sudo apt-get -y install bash-completion pwgen micro git ssh tree`
   - Loin ssh avainparin `ssh-keygen`+ `3xreturn`
   - Kopioin julkisen avaimen `cat /home/vagrant/.ssh/id_rsa.pub` ja liitin sen Githubin settings sivun SSH and GPG keyes - osioon. Tämä autentikoin k002 muokkaamaan **syjaka*-tilin Githubia.
   - Loin Githubissa uuden repon **suolaxkadi** ja kopioin sieltä SSH-osoitteen. Tämän liitin ao. komentoon.
   - Loin kotihakemistoon code kansion, jonne laitan vastaisuudessakin kaikki repot `mkdir code` ja siirryin sinne `cd code`.
   - Annoin koneelle komennon `git clone  git@github.com:syjaka/suolaxkadi.git` joka kloonasi Githubiin luodun repon.
   - Siirryin kloonattuun repoon ja kaikki näyttää olevan kunnossa.
     ![h03-12](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-012.png)
   
2. Aloitin testaamalla Hello worldilla.
   - Loin suolaxkadi hakemistoon srv/salt hakemiston `mkdir - p srv/salt` ja sinne loin `mkdir hello`.
   - `micro init.sls` avasi microlla init.sls-nimisen tiedoston, jonne tallensin:

         /tmp/GitSalt-greets:
             file.managed
   - Testasin `sudo salt-call --local --file-root srv/salt/ state.apply hello`, joka palautti onnistuneesti yhden tehdyn muutoksen:
![h3-013](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-013.png)
   - `git add . && git commit; git pull && git push` komento palautti ao. virheen eli minun piti lisäsätä aluksi nimeni ja meili.
   
         vagrant@k002:~/code/suolaxkadi$ git add . && git commit; git pull && git push
         Author identity unknown
    
         *** Please tell me who you are.
    
         Run
    
         git config --global user.email "you@example.com"
         git config --global user.name "Your Name"

         to set your account's default identity.
         Omit --global to set the identity only in this repository.
    
         fatal: empty ident name (for <vagrant@k002>) not allowed
   
   - Annoin komennot `git config --global user.email "kadriye.syrja@myy.haaga-helia.fi"` ja `git config --global user.name "Kadi Syrjä @k001"` ja kokeilin  uudelleen `git add . && git commit; git pull && git push`, joka onnistuneesti päästi tallentamaan commitin. Kuvassa lopputulos Githubissa.
     ![03-014](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-014.png)
   - Väärä aikaleima harmitti, joten päivitin sen `sudo apt-get -y install ntp`ja `sudo systemctl enable --now ntp`
 ja  tarkistin vielä `date` että kone on ajan tasalla.

3. Seuraavaksi tein **lempparit** moduulin, joka ajaa kaikki suosikkiohjelmat `mkdir lempparit`.
    - `cd lempparit`ja `micro init.sls` jonne tallensin:
    
          favourite-packages:
            pkg.installed
              - pkgs:
              - git
              - bash-completion
              - pwgen
              - micro
              - ssh
              - tree
              - cowsay
              - cmatrix
              - trash-cli
              - wget
              - curl
      
    - Testasin `sudo salt-call --local -l info --file-root srv/salt/ state.apply lempparit`.
    - Lopputuloksena onnistunut ajo:
     ![03-015](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-015.png)
     ![03-016](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-016.png)
    - `git add . && git commit; git pull && git push` synkkasi muutokset Githubiin, josta vielä tuplatsekkasin, että ne siirtyivät onnistuneesti.

4. Seuraavaksi loin Makefilen joka ajaa `make` komennolla kyseiseen tiedostoon tallennetut komennot. File luotiin repon päähakemistossa `micro Makefile` ja sinne tallensin lempparit moduulin ajokomennon.

        all:
             sudo salt-call --local -l info --file-root srv/salt/ state.apply lempparit
   
   - Komento `make`antoi palautteena, että command not found ja google kertoi, että se pitää asentaa komennolla `sudo apt-get install make` jonka jälkeen `make` toimi odotetusti. (Ramuglia 2024)
![h3-017](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-017.png)

5. Tein vielä topfilen, jolle voi antaa eri konetyyppejä, joiden mukaan taas se osaa asentaa eri konetyypeille määrätyt moduulit.
   - Poistin Makefilen ajettavasta komennosta, ajettavan moduulin nimen, jolloin komennoksi jäi `sudo salt-call --local -l info --file-root srv/salt/ state.apply`
   - siirryin `srv/salt` hakemistoon ja siellä `micro top.sls` komennolla luon topfilen, jonne tallensin:

         base:
            '*':
               - hello
               - lempprit
     
      - Tämä sisältö ajaa Hello ja lempparit moduulit kaikille `'*'` koneille. `make` suolaxkadi-hakemistossa paljasti, että homma toimii.
       
6. Vielä viimeiseksi `git add . && git commit; git pull && git push`.
   

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_Toimiva_versio.md#h3-toimiva-versio)

---

## f) Vapaaehtoinen ykkönen - Se toinen järjestelmä - 12.04.2024 klo 09.45 - 10.25 EET.
Kokeile Gittiä eri käyttöjärjestelmällä kuin sillä, millä teit muut harjoitukset. Selitä niin, että kyseistä järjestelmää osaamatonkin onnistuu. Mahdollisuuksia on runsaasti: Debian, Fedora, Windows, OSX... (Karvinen 2024).

Kokeilin Gittiä oman emokoneeni käyttöjärjestelmällä. Minulla on jo *brew* asennettu, joten asensin sen avulla Gitin käyttäen komentoa `brew install git`. Mikäli **brewtä** ei olisi ollut, olisi sen asennus onnistunut komennolla `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`
1. Koneen autentikointi Githubiin ja edellisen osion *summer* repon kloonaaminen paikallisesti koneeseen.
   - SSH-avainparin luonti onnistui komennolla `ssh-keygen -t rsa -b 4096`, joka loi RSA-tyypin 4096 bittiä pitkän avaimen.
   - `cat /Users/kadriyesamaletdin/.ssh/id_rsa.pub` tulosti julkisen avaimen terminaaliin, josta kopioin sen Githubini asetuksien SSH-avainten listaan.
   - `mkdir git` loi git-nimisen hakemiston jonne kloonasin summer-repon SSH linkin komennolla `git clone git@github.com:syjaka/summer.git`.
   - `cd summer` siellä `ls` tuo esiin saman hakemistorakenteen kuin a-tehtävässä tehty.
      ![h3-018](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-018.png)
   - Loin vielä uuden kansion ja tiedoston ja synkkasin ne Githubiin kuten aiemminkin tehtävissä olin tehnyt.
   - Commit-ruutu aukesi **vimillä**, sillä en ollut asentanut microa koneelle.

         # Please enter the commit message for your changes. Lines starting
         # with '#' will be ignored, and an empty message aborts the commit.
         #
         # On branch main
         # Your branch is up to date with 'origin/main'.
         #
         # Changes to be committed:
         #       new file:   uusi
         #
         add new folder makilla, add new file uusi
     
   -  Viestin kirjoittamisen jälkeen tallensin ja suljin editorin. `esc` palasi normaalitilaan ja `:wq`ja return tallensi ja sulki editorin.
      ![h3-019](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-019.png)
   -  Sama muutos näkyi githubissa.
      ![h3-020](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-020.png)
      
   -  Asensin micron ja asetin sen oletukseksi, koska sitä on mukavampi käyttää.
      - `brew install micro` asensi micron.
      - `echo "export EDITOR='micro'" >> ~/.zshrc` Tämä asetti micron oletuseditoriksi määrittelemällä sen EDITOR-ympäristömuuttujaan. Koska käytössä on zsh-shell oikea tiedosto on kotihakemistostani löytyvä .zshrc.
   - Testasin vielä muokkaamalla **makilla.uusi** tiedostoa ja synkkaamalla sen Githubiin. Nyt aukesi toivottu editori. 
     ![h3-021](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-021.png)
   - Kirjoitin commit viestin ja `ctrl+s` ja `ctrl+q` tallensi ja poistui editorista. Synkkaus meni läpi ja Githubissa näkyi uusi commit-viesti.
     ![h3-022](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-022.png)

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_Toimiva_versio.md#h3-toimiva-versio)

---

## g) Vapaaehtoinen kakkonen - Yhteistyöbonus, eli ota kaveri mukaan - 12.04.2024 klo 10.25 - 10.49 EET.

Anna kaverillesi (tai alter egollesi) oikeus kirjoittaa varastoosi (commit access). Tehkää molemmat muutoksia varastoon gitillä (Karvinen 2024).

Kurssin tehtäväsivulle oli Anja lähettänyt oman reponsa [osoitteen](https://github.com/anha2/configdemo). Oletin, että tätä tehtävää ajatellen. Annoin Anjalle oikeuden kirjoittaa minun summer repoon. 
1. Siirryin repon pääsivulle ja sieltä valitsin settings.
![h3-023](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-023.png)
2. Asetuksista klikkasin `Collaborators`.
![h3-024](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-024.png)
3. Täällä valitsin ensin add people ja avautuvaan ruutuun kirjoitin `anja2` ja `add anhs2to ...` jolloin repossa näkyi, että yksi kutsu voimassa.
![h3-025](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-025.png)
![h3-026](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-026.png)
6. Jatkan tehtävää palautuksen jälkeen, kun saan muokkausoikeudet jonkun toisen repoon.

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_Toimiva_versio.md#h3-toimiva-versio)

---

## Lähteet

Chacon and Straub 2014: Pro Git, 2ed: 1.3 Getting Started - What is Git? Luettavissa: https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F. Luettu 11.04.2024

ChatGPT 3,5 kysymyksellä, miten näen staged git muutoksen ennen committia.

Git documentation - a, git-add 2024. Luettavissa: https://git-scm.com/docs/git-add. Luettu 11.04.2024

Git documentation - b, git-commit 2024. Luettavissa: https://git-scm.com/docs/git-commit. Luettu 11.04.2024

Git documentation - c, git-pull 2024. Luettavissa: https://git-scm.com/docs/git-pull. Luettu 11.04.2024

Git documentation - d, git-push 2024. Luettavissa: https://git-scm.com/docs/git-pull. Luettu 11.04.2024

Karvinen T. Infra as Code, 2024. Luettavissa: https://terokarvinen.com/2024/configuration-management-2024-spring/. Luettu 11.04.2024

Karvinen T. Github Suolax 2024. mLuettavissa:https://github.com/terokarvinen/suolax/tree/main. Luettu 10.04.2024.

Ramuglia G, Intro to ‘make’ Linux Command: Installation and Usage 2024. Luettavissa: https://ioflood.com/blog/install-make-command-linux/. Luettu 11.04.2024.

Syjaka Palvelinten hallinta 2024/h2_Soitto kotiin 2024. Luettavissa: https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h2_Soitto_kotiin.md#f-hello-iac-08042024-klo-1505---1530-eet. Luettu 11.04.2024

