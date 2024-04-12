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

1 . [Chacon and Straub 2014: Pro Git, 2ed: 1.3 Getting Started - What is Git?](https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F)

 Kirjan kappaleessa 1.3 opetetaan Gitin perusteita toiminnan logiikasta ja Gitin eroista muihin varsionhallintajärjestelmiin. Tekstissä tuodaan esiin Gitin ainutlaatuisuutta tavassa käsitellä datan muutoksia enemmänkin tiedostojen tilannevedoksina, kuin aina uusina tiedostoina ja tiedostoina tehdyistä muutoksista. 
 - Suuri osa gitin muutoksista toimii paikallisesti, mikä nopeuttaa työskentelyä ja vapauttaa serveriyhteyden välttämättömyydestä.
 - Datan eheys varmistetaan käyttämällä SHA-1 hash tarkistussummaa.
 - Gitin tiedostot voivat olla kolmessa tilassa; muokattu, staged ja committed.


2. Gitin käyttö on lähinnä 'git add . && git commit; git pull && git push'. 
  -Selitä tuon komennon jokainen osa. Käytä apuna itse valitsemiasi lähteitä ja viittaa niihin.

    - `git add` Kun projektin tehdään muutoksia ne tulee "manuaalisti" sisällyttää seuraavaan committiin, eli lavastaa commitoitavaksi. Tämä tapahtuu  `git add`-komennolla. Komennon seurauksena git on päivittänyt indeksinsä vastaamaan komennon suorittamisen aikaista tilaa. Kyseisen komennon voi suorittaa useita kertoja ennen varsinaista committia. (Git documentation -a 2024)
    - `git commit` On luontainen seuraus edelliselle komennolle joka on lavastanut muutokset commitoitavaksi. Eli komento luo uuden commitin joka sisältää nykyisen indexin ja annetun lokiviestin commitista. Uusin kommit on yleensä nykyisen haaran kärki ja haara päivitetään automaattisesti osoittamaan siihen. (Git documentation - b 2024)
    - `git pull` - komento yhdistää muutokset etävarastosta paikalliseen varaston nykyiseen haaraan. Mikäli haarat ovat erkaantuneet tulee haarat sovittaa yhteen `rebase` tai `--no rebase` toiminnoilla (Git documentation - c 2024).
    - `git push` päivittää etävarastot käyttäen paikallisia varastoja. Komennon yhteydessä on annettava toivottuja konfiguraatioita tai komentorivin määrityksiä komennolla. Mikäli näitä ei anneta, työnnetään nykyinen haara vastaavaan ylähaaraan. Jos ylähaaran nimi ei vastaa paikallista keskeytetään komento (Git documentation - d 2024).

   
3. Varaston [terokarvinen/suolax/](https://github.com/terokarvinen/suolax/) historia - 11.4 klo 12.45 - 13.30 EET
  - eli loki ja muutokset. Kätevimmin komentokehotteesta 'git clone https://github.com/terokarvinen/suolax.git; cd suolax/; git log --patch --color|less -R'. Wepistäkin saattaa onnistua kliksuttelemalla "Commits". (Karvinen 2024)

   Tein tehtävän komentorivin kautta.
  1. Avasin ssh yhteyden aiemmin Vagrantilla luotuun virtuaalikoneeseen joka sijaitsi koneeni kotihakemistossa. komennolla `vagrant ssh`. Koneelle oli git asennettu jo tunnilla.
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

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_Toimiva_versio.md#h3-toimiva-versio)

---

## y) Käyttöympäristö
Tehtävä toteutettiin MacBook Retina 12-inch, koneella jossa, host OS on Ventura 13.6.1 käyttöjärjestelmä Suomen maa-asetuksilla ja suomen kielellä. Koneessa on 1,3GHz kaksiytiminen Intel Core i5 prosessori ja 8Gt 1867 MHz LPDDR3 muistia. Näytönohjain on Intel HD Graphics 615 jossa VRAM 1536 Mt.

---

## z) Alkutoimet
Koneen ja pääte-työkalun käynnistys.

---

Kaikki seuraavien osion tehtävänannot ovat peräisin Tero Karvisen - [Infra As a Code - Palvelinten hallinta 2024 kurssisivulta](https://terokarvinen.com/2024/configuration-management-2024-spring/#h3-toimiva-versio).

## a) Online - 11.04.2024 klo 13.30 - 13.43 EET.
Tee uusi varasto GitHubiin (tai Gitlabiin tai mihin vain vastaavaan palveluun). Varaston nimessä ja lyhyessä kuvauksessa tulee olla sana "summer". Aiemmin tehty varasto ei kelpaa. (Muista tehdä varastoon tiedostoja luomisvaiheessa, esim README.md ja GNU General Public License 3)

1. Omaan Githubiini kirjautuneena sivuston pääsivulta valitsin `new`
2. Avautuvasta ikkunasta annoin varastolle nimen *summer*. Jätin varaston näkyvyyden julkiseksi. Valitsin README-filen lisättäväksi sekä valitsin lisenssiksi GNU General Public Licensen. Viimeistelin luonnin `Create repository`.
3. Lopputuloksena Githubissa on uuso repo nimeltään *summer*
![h3-005]()

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_Toimiva_versio.md#h3-toimiva-versio)

---

## b) Dolly  11.04.2024 klo 13.45 - 14.06 EET
Kloonaa edellisessä kohdassa tehty uusi varasto itsellesi, tee muutoksia omalla koneella, puske ne palvelimelle, ja näytä, että ne ilmestyvät weppiliittymään.
Jatkoin tässä tehtävässä työskentelyä samalla virtuaalikoneella kuin kohdassa x.

1. Kopioin repon etusivulla `code-painikkeen` local- välilehdeltä löytyvän repon SSH-osoitteen jonka liitän myöhemmin  `git clone`-komentoon.
![h3-006]()
2. Siirryin kotihakemistossa sijaitsevaan code hakemistoon `cd ..`
3. Komennolla `git clone git@github.com:syjaka/summer.git` kopioin luodun repon paikalliseen virtuaalikoneeseeni.
![03-007]()
4. `cd summer` siirryin kopioituun repoon.
5. `micro vamos` loi vamos nimisen tiedoston
6. `git add . && git commit` tunkee tiedostosn ja commitin etärepoon.
7. Paitsi ei tunkenutkaan vaan vain "lavasti" ja teki commitin. Eli lisäsin myös `git push` komennon, ja homma toimi.
![h03-008]()
8. Aavistuksen erikoiselta tosin selaimessa näytti aikajanat jossa lisenssi ja README oli lisätty noin puoli tuntia sitten ja juuri lisäämäni vamos 14 tuntia sitten
9. Lokia tarkastellessa tämäkin selittyi. Virtuaalikoneeni on vielä eilisessä.
![h3-009]()
   
[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_Toimiva_versio.md#h3-toimiva-versio)

---

## c) Doh! 11.04.2024 klo 14.18 - 14.33 EET.
Tee tyhmä muutos gittiin, älä tee commit:tia. Tuhoa huonot muutokset ‘git reset --hard’. Huomaa, että tässä toiminnossa ei ole peruutusnappia.
En ollut ihan varma tehtävän lopullisesta tarkoituksesta kun tehty tyhmä muutoshan ei missään näy olman committia
1. Tein aluksi tyhmän muutoksen `micro vamos` + muutos sisältöön +  `git add .`
2. Muutoksen teko näkyi `git status`komennolla
3. Halusin nähdä myös muutoksen sisällön, jossa ChatGPT auttoi. `git diff --cached` toi esiin tehdyn muutoksen (ChatGpt 2024)
4. Lopuksi `git reset --hard` poisti tuon muutoksen.
![h3-010]()

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_Toimiva_versio.md#h3-toimiva-versio)

---

## d) Tukki - 11.04.2024 klo 14.45 - 15.05 EET.
Tarkastele ja selitä varastosi lokia. Tarkista, että nimesi ja sähköpostiosoitteesi näkyy haluamallasi tavalla ja korjaa tarvittaessa.

1. Varaston loki tulee esiin `git log --patch --color|less -R`
![h3-011]()
2. Analyysiä
    - *Commit* on tuo kyseisen commitin yksilöllinen tunniste - SHA-1 arvo.
    - *Author* näyttää nimeni ja meiliosoitteeni. Nämä säädin oikeaksi jo eilisellä tunnilla komennoilla `git config --global user.email "mun meili"` ja `git config --global user.name "mun nimi"`.
    - *Date* antaa commitin ajankohdan. Tässä ekan ja tokan välillä ristiriita, sillä virtuaalikoneeni ei ole ajan tasalla.
    - Seuraavaksi näkyy Commit message, tässä *initial commit* ja *add file vamos*
    - *diff --git a/vamos b/vamos* identifioi tiedoston ennen ja jälkeen muutoksen
    - *new file mode 100644* kertoo uudesta tiedostosta ja sen oikeuksista
    - *index 0000000..64cbbea* viittaa tiedoston index-tilaan
    - *+++ b/vamos* ja *+++ B/LICENSE* kertoo lisätyt tiedostot
    - *@@ -0,0 +1 @@* ja *@@ -0,0 +1,674 @@* kertoo lisättyjen rivien lukumäärän ja viimeiseksi vihreällä näkyy lisätyt rivit sisältöineen
    - 

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_Toimiva_versio.md#h3-toimiva-versio)

---

## e) Suolattu rakki - 11.04.2024 klo 15.10 - 17.40 EET.
Aja Salt-tiloja omasta varastostasi. (Salt tiedostot mistä vain hakemistosta "--file-root teronSaltHakemisto". Esimerkiksi 'sudo salt-call --local --file-root srv/salt/ state.apply', huomaa suhteellinen polku.)

Tähän tehtävään otin käyttöön viime tehtävässä h2 luodun virtuaalikoneen k002 jossa Salt oli valmiina.
1. Aloitin määrittämällä koneen:
   - Siirryin emokoneellani kansioon `cd twohost` ja otin päätteen eri välilehdille yhteydet `vagrant  ssh k002`
   - Aloitin asentamalla gitin ja muutamia muita ohjelmia:
     - `sudo apt-get update` ja `sudo apt-get -y install bash-completion pwgen micro git ssh tree`
   - Loin ssh avainparin `ssh-keygen`+ `3xreturn`
   - Kopioin julkisen avaimen `cat /home/vagrant/.ssh/id_rsa.pub`ja liitin sen githubin settings ja SSH and GPG keyes.
   - Loin githubissa uuden repon *suolaxkadi ja kopioin sieltä SSH-osoitteen jonka liitin ao komentoon.
   - Loin kotihakemistoon code kansion jonne laitan kaikki repot `mkdir code` ja siirryin sinne `cd code`
   - Annoin k001 komennon `git clone  git@github.com:syjaka/suolaxkadi.git` joka kloonasi githubiin luodun repon.
   - Siirryin kloonattuun repooin ja kaikki näyttää olevan kunnossa
     ![h03-12]()
   
2. Aloitin testaamalla Hello worldilla.
   - Loin suolaxkadi hakemistoon srv/salt halemiston `mkdir - p srv/salt` ja sinne loin `mkdir hello`.
   - `micro init.sls`luo tiedoston, jonne tallensin
         /tmp/GitSalt-greets:
           file.managed
   - Testasin `sudo salt-call --local --file-root srv/salt/ state.apply hello`joka palautti onnistuneesti yhden tehdyn muutoksen:
![h3-013]()
   - `git add . && git commit; git pull && git push` komento palautti virheen eli lisään aluksi nimen ja meilin.
   
       vagrant@k002:~/code/suolaxkadi$ git add . && git commit; git pull && git push
       Author identity unknown
    
       *** Please tell me who you are.
    
       Run
    
       git config --global user.email "you@example.com"
       git config --global user.name "Your Name"

       to set your account's default identity.
       Omit --global to set the identity only in this repository.
    
       fatal: empty ident name (for <vagrant@k002>) not allowed
   
   - `git config --global user.email "kadriye.syrja@myy.haaga-helia.fi"` ja `git config --global user.name "Kadi Syrjä @k001"` ja uudelleen kokeilen `git add . && git commit; git pull && git push` joka onnistuneesti päästi tallentamaan commitin.
     ![03-014]()
   - Lopputuloksena myös githubissa näkyy luotu moduuli. (väärä aikaleima harmitti. päivitin sen `sudo apt-get -y install ntp`ja `sudo systemctl enable --now ntp` tarkistin vielä `date`että kone on ajan tasalla.
`
3. Seuraavaksi tein lempparit moduulin joka ajaa kaikki suosikkiohjelmat uutta konetta käyttöönottaessa `mkdir lempparit`
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
    - Testasin `sudo salt-call --local -l info --file-root srv/salt/ state.apply lempparit`
    - Lopputuloksena onnistunut ajo:
     ![03-015]()
     ![03-016]()
    - `git add . && git commit; git pull && git push` tallensin muutokset ja tarkistin että ne siirtyivät Githubiin onnistuneesti.

4. Seuraavaksi loin makefilen joka ajaa `make` komennolla filessä olevat komennot. File luotiin repon päähakemistossa `micro Makefile` ja sinne tallensin lempparit moduulin ajokomennon.

        all:
             sudo salt-call --local -l info --file-root srv/salt/ state.apply lempparit
   - Komento `make`antoi palautteena että command not found ja google kertoi että se pitää asentaa komennolla `sudo apt-get install make` jonka jälkeen `make` toimi odotetusti. (Ramuglia 2024)
![h3-017]()

5. Tein vielä topfilen jolle voi antaa eri konetyyppejä joille voi asentaa eri moduuleja.
   - Poistin Makefilen ajettavasta komennosta ajettavan moduulin nimen, jolloin komennoksi jäi `sudo salt-call --local -l info --file-root srv/salt/ state.apply`
   - siirryin `srv/salt`hakemistoon ja siellä `micro top.sls`komennolla luon topfilen, jonne tallennan:

         base:
            '*':
               - hello
               - lempprit
      - Tämä sisältö ajaa Hello ja lempparit moduulit kaikille `'*'` koneille. `make`suolaxkadi-hakemistossa paljasti että homma toimii
       
6. Vielä viimeiseksi `git add . && git commit; git pull && git push`
   
Osion lähteinä käytetty 10.04.2024 luentomuistiinpanoja sekä Tero Karvisen suolax-repoa joka tehtiin luennolla. (Karvinen 2024)

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_Toimiva_versio.md#h3-toimiva-versio)

---

## f) Vapaaehtoinen ykkönen - Se toinen järjestelmä - 12.04.2024 klo 09.45 - 
Kokeile Gittiä eri käyttöjärjestelmällä kuin sillä, millä teit muut harjoitukset. Selitä niin, että kyseistä järjestelmää osaamatonkin onnistuu. Mahdollisuuksia on runsaasti: Debian, Fedora, Windows, OSX...

Kokeilin Gittiä oman koneeni käyttöjärjestelmällä. Minulla on jo brew asennettu, joten asensin sen avulla gitin käyttäen komentoa `brew install git`. Mikäli Brewtä ei olisi ollut olisi sen asennus onnistunut komennolla `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`
1. Koneen autentikointi Githubiin ja edellisen *summer* repon kloonaaminen paikallisesti koneeseen.
   - SSH-avainparin luonti onnistui komennolla `ssh-keygen -t rsa -b 4096` joka luo RSA-tyypin 4096 bittiä pitkän avaimen.
   - `cat /Users/kadriyesamaletdin/.ssh/id_rsa.pub` tulostaa julkisen avaimen terminaaliin, josta kopioin sen Githubini asetuksien SSH-avainten listaan.
   - `mkdir git` luo git-nimisen hakemiston jonnne kloonaan summer-repon SSH linkin komennolla `git clone git@github.com:syjaka/summer.git`
   - `cd summer` siellä `ls` tuo esiin saman hakemistorakenteen kuin a-tehtävässä tehty.
      ![h3-018]()
   - Luon vielä uuden kansion ja tiedoston ja synkkaan ne Githubiin.
   - Commit-ruutu aukeaa vimillä, sillä en ollut asentanut microa koneelle.

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
   -  Viestin kirjoittamisen jälkeen tallennan ja suljen editorin. `esc` palaa normaalitilaan ja `:wq`ja return tallentaa ja sulkee editorin.
      ![h3-019]()
   -  Sama muutos näkyy githubissa
      ![h3-020]()
      
   -  Asennan samalla micron ja asetan sen oletukseksi macilla, koska sitä on  mukavampi käyttää.
      - `brew install micro` asentaa micron
      - `echo "export EDITOR='micro'" >> ~/.zshrc` Tämä asettaa micron oletuseditoriksi määrittelemällä sen EDITOR-ympäritömuuttujaan. Koska käytössä on zsh-shell oikea tiedosto on kotihakemistostani öytyvä .zshrc.
   - Testaan vielä muokkaamalla macilla.uusi tiedostoa ja synkkaamalla sen Githubiin. Nyt aukeaa toivottu editori. 
     ![h3-021]()
   - Kirjoitin commit viestin ja `ctrl+s`ja `ctrl+q`tallentaa ja poistuu editorista. Synkkaus meni läpi ja Githubissa näkyy uusi commit-viesti
     ![h3-022]()

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_Toimiva_versio.md#h3-toimiva-versio)

---

## g) Vapaaehtoinen kakkonen - Yhteistyöbonus, eli ota kaveri mukaan
Anna kaverillesi (tai alter egollesi) oikeus kirjoittaa varastoosi (commit access). Tehkää molemmat muutoksia varastoon gitillä.

Kurssin tehtäväsivulle oli Anja lähettänyt oman reponsa [osoitteen](https://github.com/anha2/configdemo). Oletin että tätä tehtävää ajatellen. Annoin Anjalle oikeuden kirjoittaa minun summer repoon. 
1. Siirryin repon pääsivulle ja sieltä valitsin settings.
h3-023
2. Asetuksista klikkasin `Collaborators`.
h3-024
3. Täällä valitsin ensin add people ja avautuvaan ruutuun kirjoitin `anja2` ja `add anhs2to ...` jolloin repossa näkyi että yksi kutsu voimassa.
h3-025
h3-026
6. Jatkan tehtävää palautuksen jälkeen kun saan muokkausoikeudet jonkun toisen repoon.

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h3_Toimiva_versio.md#h3-toimiva-versio)

---

## Lähteet

Chacon and Straub 2014: Pro Git, 2ed: 1.3 Getting Started - What is Git? Luettavissa: https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F. Luettu 11.04.2024

ChatGPT 3,5 kysymyksellä, miten näen staged git muutoksen ennen committia.

Git documentation - a, git-add 2024. Luettavissa: https://git-scm.com/docs/git-add. Luettu 11.04.2024

Git documentation - b, git-commit 2024. Luettavissa: https://git-scm.com/docs/git-commit. Luettu 11.04.2024

Git documentation - c, git-pull 2024. Luettavissa: https://git-scm.com/docs/git-pull. Luettu 11.04.2024

Git documentation - d, git-push 2024. Luettavissa: https://git-scm.com/docs/git-pull. Luettu 11.04.2024

Karvinen T. Github Suolax 2024. mLuettavissa:https://github.com/terokarvinen/suolax/tree/main. Luettu 10.04.2024.

Ramuglia G, Intro to ‘make’ Linux Command: Installation and Usage 2024. Luettavissa: https://ioflood.com/blog/install-make-command-linux/. Luettu 11.04.2024.

Syjaka Palvelinten hallinta 2024/h2_Soitto kotiin 2024. Luettavissa: https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h2_Soitto_kotiin.md#f-hello-iac-08042024-klo-1505---1530-eet. Luettu 11.04.2024

Tero Karvinen, Infra as Code, 2024. Luettavissa: https://terokarvinen.com/2024/configuration-management-2024-spring/. Luettu 11.04.2024
