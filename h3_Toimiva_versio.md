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
### 1. [Chacon and Straub 2014: Pro Git, 2ed: 1.3 Getting Started - What is Git?](https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F)
   - Kirjan kappaleessa 1.3 opetetaan Gitin perusteita sen toiminnan logiikasta ja Gitin eroista muihin versionhallintajärjestelmiin. Tekstissä tuodaan esiin Gitin ainutlaatuisuutta tavassa käsitellä datan muutoksia enemmänkin tiedostojen tilannevedoksina, kuin aina uusina tiedostoina ja tiedostoina tehdyistä muutoksista.
   - Suuri osa Gitin muutoksista toimii paikallisesti, mikä nopeuttaa työskentelyä ja vapauttaa serveriyhteyden välttämättömyydestä.
   - Datan eheys varmistetaan käyttämällä SHA-1 hash tarkistussummaa.
   - Gitin tiedostot voivat olla kolmessa tilassa; muokattu, staged ja committed.
### 2. Gitin käyttö on lähinnä 'git add . && git commit; git pull && git push'. 
   - `git add` Kun projektin tehdään muutoksia, tulee ne "manuaalisti" sisällyttää seuraavaan committiin, eli lavastaa commitoitavaksi. Tämä tapahtuu `git add`-komennolla. Komennon seurauksena git on päivittänyt indeksinsä vastaamaan komennon suorittamisen aikaista tilaa. Kyseisen komennon voi suorittaa useita kertoja ennen varsinaista committia. (Git documentation -a 2024)
   - `git commit` On luontainen seuraus edelliselle komennolle, joka on lavastanut muutokset commitoitavaksi. Eli komento luo uuden commitin joka sisältää nykyisen indexin ja annetun lokiviestin commitista. Uusin kommit on yleensä nykyisen haaran kärki ja haara päivitetään automaattisesti osoittamaan siihen. (Git documentation - b 2024)
   - `git pull` - komento yhdistää muutokset etävarastosta paikalliseen varaston nykyiseen haaraan. Mikäli haarat ovat erkaantuneet tulee haarat sovittaa yhteen `rebase` tai `--no rebase` toiminnoilla (Git documentation - c 2024).
   - `git push` päivittää etävarastot käyttäen paikallisia varastoja. Komennon yhteydessä on annettava toivottuja konfiguraatioita tai komentorivin määrityksiä komennolla. Mikäli näitä ei anneta, työnnetään nykyinen haara vastaavaan ylähaaraan. Jos ylähaaran nimi ei vastaa paikallista keskeytetään komento (Git documentation - d 2024).
## 3. Varaston [terokarvinen/suolax/](https://github.com/terokarvinen/suolax/) historia - 11.4 klo 12.45 - 13.30 EET
   - eli loki ja muutokset (Karvinen 2024).
   1. Avasin ssh yhteyden aiemmin Vagrantilla luotuun virtuaalikoneeseen *Bookworm*, joka sijaitsi koneeni kotihakemistossa. Tein tämän komennolla `vagrant ssh`. Tälle koneelle oli Git asennettu jo tunnilla.
   2. Etäyhteyden avauduttua siirryin `cd code ` - hakemistoon (joka oli myös tunnilla luotu)
   3. Toin githubin opettajan repon tuonne hakemistoon kloonaamalla sen komennolla `git clone https://github.com/terokarvinen/suolax.git` ja siirryin komennot tuomaan suolax hakemistoon `cd suolax`.
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
Kaikki seuraavien osioiden tehtävänannot ovat peräisin Tero Karvisen - Infra As a Code - [Palvelinten hallinta 2024 kurssisivulta](https://terokarvinen.com/2024/configuration-management-2024-spring/#h3-toimiva-versio).
9. Lokia tarkastellessa tämä selittyi. Virtuaalikoneeni oli vielä eilisessä (korjasin tämän vasta myöhemmin tehtävässä).
1. Tein aluksi tyhmän muutoksen `micro vamos` + muutos sisältöön + `git add .`.
1. Varaston loki tuli esiin `git log --patch --color|less -R`.
2. Analyysiä tästä.
    - **Commit** on kyseisen commitin yksilöllinen tunniste - SHA-1 arvo.
    - **Author** näyttää nimeni ja meiliosoitteeni. Nämä säädin oikeaksi jo eilisellä tunnilla komennoilla `git config --global user.email "mun meili"` ja `git config --global user.name "mun nimi"`.
    - **Date** antoi commitin ajankohdan. Tässä ekan ja tokan välillä ristiriita, sillä virtuaalikoneeni ei ollut ajan tasalla.
    - Seuraavaksi näkyi Commit message, tässä kahden commitin **initial commit** ja **add file vamos**.
    - **diff --git a/vamos b/vamos** identifioi tiedoston ennen ja jälkeen muutoksen.
    - **new file mode 100644** kertoi uudesta tiedostosta ja sen oikeuksista.
    - **index 0000000..64cbbea** viittasi tiedoston index-tilaan.
    - **+++ b/vamos** ja **+++ B/LICENSE** kertoi lisätyt tiedostot.
    - **@@ -0,0 +1 @@** ja **@@ -0,0 +1,674 @@** kertoi lisättyjen rivien lukumäärän ja viimeiseksi vihreällä näkyi lisätyt rivit sisältöineen.
Tämän osion lähteinä on käytetty 10.04.2024 luentomuistiinpanoja, sekä Tero Karvisen suolax-repoa, joka tehtiin luennolla. Muut lähteet ovat merkitty tekstiviitteisiin. 
Tähän tehtävään otin käyttöön viime viikon tehtävässä h2 luodun virtuaalikoneen k002, jossa Salt oli valmiina.
   - Siirryin emokoneellani kansioon `cd twohost` ja otin yhteyden koneeseen `vagrant  ssh k002`
   - Kopioin julkisen avaimen `cat /home/vagrant/.ssh/id_rsa.pub` ja liitin sen Githubin settings sivun SSH and GPG keyes - osioon.
   - Loin Githubissa uuden repon **suolaxkadi** ja kopioin sieltä SSH-osoitteen. Tämän liitin ao. komentoon.
   - Loin kotihakemistoon code kansion, jonne laitan vastaisuudessakin kaikki repot `mkdir code` ja siirryin sinne `cd code`.
   - Annoin koneelle komennon `git clone  git@github.com:syjaka/suolaxkadi.git` joka kloonasi Githubiin luodun repon.
   - Loin suolaxkadi hakemistoon srv/salt hakemiston `mkdir - p srv/salt` ja sinne loin `mkdir hello`.
   - `git add . && git commit; git pull && git push` komento palautti ao. virheen eli minun piti lisäsätä aluksi nimeni ja meili.
   - Annoin komennot `git config --global user.email "kadriye.syrja@myy.haaga-helia.fi"` ja `git config --global user.name "Kadi Syrjä @k001"` ja kokeilin  uudelleen `git add . && git commit; git pull && git push`, joka onnistuneesti päästi tallentamaan commitin. Kuivassa lopputulos Githubissa.
   - Väärä aikaleima harmitti, joten päivitin sen `sudo apt-get -y install ntp`ja `sudo systemctl enable --now ntp`
3. Seuraavaksi tein **lempparit** moduulin, joka ajaa kaikki suosikkiohjelmat `mkdir lempparit`.
    - `git add . && git commit; git pull && git push` synkkasi muutokset Githubiin, josta vielä tuplatsekkasin, että ne siirtyivät onnistuneesti.
5. Tein vielä topfilen, jolle voi antaa eri konetyyppejä, joiden mukaan taas se osaa asentaa eri konetuyypeille määrätyt moduulit.
   - Poistin Makefilen ajettavasta komennosta, ajettavan moduulin nimen, jolloin komennoksi jäi `sudo salt-call --local -l info --file-root srv/salt/ state.apply`
6. Vielä viimeiseksi `git add . && git commit; git pull && git push`
Kokeilin Gittiä oman koneeni käyttöjärjestelmällä. Minulla on jo *brew* asennettu, joten asensin sen avulla, Gitin käyttäen komentoa `brew install git`. Mikäli Brewtä ei olisi ollut, olisi sen asennus onnistunut komennolla `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`
1. Koneen autentikointi Githubiin ja edellisen osion *summer* repon kloonaaminen paikallisesti koneeseen.
   - SSH-avainparin luonti onnistui komennolla `ssh-keygen -t rsa -b 4096`, joka loi RSA-tyypin 4096 bittiä pitkän avaimen.
   - `mkdir git` loi git-nimisen hakemiston jonne kloonasin summer-repon SSH linkin komennolla `git clone git@github.com:syjaka/summer.git`.
   - Loin vielä uuden kansion ja tiedoston ja synkkasin ne Githubiin kuten aiemminkin tehtävissä olin tehnyt.
      - `brew install micro` asensi micron.
   - Kirjoitin commit viestin ja `ctrl+s` ja `ctrl+q` tallensi ja poistui editorista. Synkkaus meni läpi ja Githubissa näkyi uusi commit-viesti.
Kurssin tehtäväsivulle oli Anja lähettänyt oman reponsa [osoitteen](https://github.com/anha2/configdemo). Oletin, että tätä tehtävää ajatellen. Annoin Anjalle oikeuden kirjoittaa minun summer repoon. 
![h3-023](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-023.png)
![h3-024](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-024.png)
![h3-025](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-025.png)
![h3-026](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-026.png)
Karvinen T. Infra as Code, 2024. Luettavissa: https://terokarvinen.com/2024/configuration-management-2024-spring/. Luettu 11.04.2024