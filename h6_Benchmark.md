
# h6 Benchmark


a) [Paketti Windowsia](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h6_Benchmark.md#a-paketti-windowsia)

b) [Benchmark](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h6_Benchmark.md#b-benchmark)

c) [Testbench](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h6_Benchmark.md#c-testbench)

d) [Viisi ideaa](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h6_Benchmark.md#d-viisi-ideaa)

x) [Lue ja tiivistä](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h6_Benchmark.md#x-lue-ja-tiivist%C3%A4)

y) [Käyttöympäristö](https://github.com/syjaka/Palvelinten-Hallinta-2024/edit/main/h6_Benchmark.md#y-k%C3%A4ytt%C3%B6ymp%C3%A4rist%C3%B6)

---

## x) Lue ja tiivistä

Windows Package Manager: 
- Introduction
  - Salt tarjoaa Windowsille paketinhallintatyökalun jota voi soveltaa etä-ympäristöjen hallinnassa (vastaava kuin Linuxin `apt`).
  - Tätä toteutetaan paketinmääritystiedoston avulla joka sisältää mm. ohjelmistopaketin nimen, sekä sen lataussijainnin. Näitä tiedostoja voi hostata Git-repoissa.
  - Pakettien asentamiseen käytetyt sls-tiedostot tulee kloonata olestusvarastosta **salt-winrepo-ng**.
  - `pkg.install`asentaa paketin ja `pkg.installed`tarkistaa paketin asennuksen tilan.
- Install libraries
  - `git python` tai `git pygit` asentaminen mahdollistaa sujuvan Git-varastojen käsittelyn mikäli käytät Saltin Git-varaston hostaamia paketinmääritystiedostoja.
- Populate the local Git repository
  - `salt-run winrepo.update_git_repos` kloonaa **salt-winrepo-ng** repon Salt-masterille **winrepo_dir_ng**:n määrittelemään sijaintiin. 
  - `salt-call --local winrepo.update_git_repos` komennolla "itsenäinen" minion voi suorittaa saman.
- Update minion database
  - `pkg.refresh_db` päivittää minionien tietokannan pakettimäärittelytiedostoja varten. Komento voidaan suorittaa masterilta kaikille minioneille muododssa `salt -G 'os:windows' pkg.refresh_db`tai itsenäisellä minionilla muodossa `salt-call --local pkg.refresh_db`.
- Install software package - Alla luetelluissa komennoissa on sama syntaksi masterille tai itsenäisellä minionilla, kuin yllä esitellyt.
  - Kun oletusvarastot ovat kloonattu ja tietokannat päivitetty, voidaan softaa asentaa masterilta `salt * pkg.install 'firefox_x64'` tai itsenäisellä minionilla `salt-call --local pkg.install "firefox_x64"`.
- Usage
  - `pkg.list_pkgs` listaa kaikki järjestelmään asennetut paketit. Komennon tulosteesta voi päätellä, onko asennettu ohjelma Saltin kautta hallittavissa vai ei, eli löytyyko paketin vastaavuus winrepo-tietokannasta.
  - `pkg.list_available` listaa saatavilla olevista versiot tietylle paketille. Haluttu paketin nimi lisätään komennon loppuun.
  - `pkg.install` Aaentaa komennossa nimetyn paketin/paketit. Paketin nimeen voi lisätä vielä halutun versiotiedon.
  - `pkg.remove` Poistaa komennossa nimetyn paketin asennuksen.
  (Salt 2024)

## y) Käyttöympäristö

Tehtävä toteutettiin MacBook Retina 12-inch, koneella jossa, host OS on Ventura 13.6.1 käyttöjärjestelmä Suomen maa-asetuksilla ja suomen kielellä. Koneessa on 1,3GHz kaksiytiminen Intel Core i5 prosessori ja 8Gt 1867 MHz LPDDR3 muistia. Näytönohjain on Intel HD Graphics 615 jossa VRAM 1536 Mt.

Koneeseen asennettu Vagrant versio on 2.4.1.

c - kohdassa käytetyt virtuaalikoneet ovat Linux Bullseye 5.10.0-28-amd64.


## a) Paketti Windowsia
Asenna Windowsiin tai Macciin ohjelmia Saltin pkg.installed -funktiolla (Karvinen 2024).

Tehtävän suoritus 02.05.2024 klo 11.35 - 12.15 EET.

1. Aloitin tmuxin asennuksella, sillä koen sen olevat hyödyllinen lisä CLI-työskentelyyn.
   -  `brew install tmux` kännisti asennuksen. Sen valmistuttua sain palautteen:
      ![h6-001](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h6-001.png)
   -  `tmux` käynnistyi ja uusia istuntoja sai joko `ctrl+b ja "`=vaaka ja `ctrl+b ja %`= pysty. `ctrl+b ja nuoli` vaihtaa paneelia ja `ctrl+b ja  x` sulkee paneelin. `ctrl+b ja s` luetteloi istunnon paneelit ja `exit` lopettaa istunnon  (Choi 2028).
   -  Hyvin toimi ja vaikutti hyödylliseltä.
2. Seuraavaksi asensin vielä `brew install cowsay speedtest-cli`
Kaikki näytti toimivan mainiosti.
![h6-002](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h6-002.png)

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h6_Benchmark.md#h6-benchmark)
___ 

## b) Benchmark

Etsi 3-7 keskitetyn hallinnan projektia, esimerkiksi tämän kurssin "Oma moduli" lopputyötä. Työn tulee olla modernia keskitettyä hallintaa (idempotentti, infra koodina, yksi totuus). Esimerkiksi pelkkä shell script ei kelpaa. Työ saa käyttää mitä vain työkalua, esim Salt, Puppet, Ansible, Chef, Conftero, CFEngine (Karvinen 2024).

Tässä tehtävässä en kirjannut aikaa, sillä merkittävän suuri osa tehtävän suoritusta kului sopivien projektien etsimiseen.

#### 1. Projekti -  [samikul - ph-moduuli Githubissa](https://github.com/samikul/ph-moduuli)

1. Tarkoitus
   - Tämän moduulin tarkoitus on konfiguroida palvelin valmiiksi Flask web-applikaatioiden testikehitykseen ja tuotantoon.
2. Lisenssi
   - Lisenssi löytyy heti repon tiedostoissa, sekä README tiedoston infosta. Työhön on valittu GNU - General Public License (GPL) joka on vapaiden ohjelmistojen lisenssi. Se antaa käyttäjille oikeuden käyttää, jakaa ja muokata ohjelmistoa. Lisenssi myös velvoittaa käyttäjäänsä säilyttämään alkuperäisen tekijän tietoa, sekä jakamaan muokatut versiot samaa lisenssiä käyttäen. Pääasiallinen juridinen vaikutus on se, että mikäli hyödynnät lisenssin vaikutuksen alaista materiaalia, sitoudut samalla noudattamaan sen ehtoja. 
3. Moduulin tekijä on Sami Kulonpää ja vuosi 2021
4. Riippuvuudet:
   - Moduuli on toteutettu Linux-käyttöjärjestelmällä. Varsinaista distroa en kyennyt vahvistamaan, sillä varsinainen työn raportointi ei annetusta linkistä, eikä Samin verkkosivuilta löytynyt. Lisäksi moduuli vaati Salt-Stackin asennuksen ja käyttöönoton. Kohdekoneella tulee olla salt minion asennettuna ja se tulee olla conffattuna masterin saavutettavissa.
5. Kiinnostavaa:
   - Työssä kiinnostavaa oli sen aihe, sillä se on juuri samaa, mitä olemme kurssilla harjoitelleet. Tässä työssä on tiivistettynä kaikki tämän ja Linux-palvelinkurssien opit kauniiseen pakettiin, joka tekee työstä myös opiskelijan näkökulmasta hyödyllisen. Lisäksi työn tarkoitus vastaa palttiarallaa sisällöltään sitä, mitä itse olin pyöritellyt oman moduulin aiheeksi. Tämä tietenkin ymmärrettävää, sillä kuten sanottu, työ tiivistää ja tarjoilee koko opitun sisällön. 
6. Avoimet kysymykset:
    - Ei jäänyt.
(Kulonpää 2021)

#### 2. Projekti -  [Janne Mustonen - Oma moduuli h7](https://jannelinux.design.blog/2020/05/19/oma-moduuli-h7/)
1. Tarkoitus
   - Moduulin tarkoitus on asentaa valitut ohjelmat valmiiksi conffattuna mille tahansa Linuxin distron minionille.
2. Lisenssi
   - Lisenssimainitaa en työstä löytänyt.
3. Tekijä ja vuosi
   - Janne Mustonen, 2020
4. Riippuvuudet: 
   - Moduuli on rakennettu toimimaan Linuxin distroilla. Kohdekoneella tulee olla Salt minion asennettuna ja se tulee olla conffattuna masterin saavutettavissa.
5. Kiinnostavaa,
   - Valittu myös ohjelmia jotka tarvitsevat repositoryn. 
6. Avoimet kysymykset ja muut huomiot
   - `state.hightsate`n ja topfilen käyttö. Mietin olisiko tämän voinut ajaa suoraan ilman topfilen määrityksiä?

#### 3. Projekti -  [Riku Mannonen - Oma Moduuli](https://rikumannonen935063021.wordpress.com/)
1. Tarkoitus
   - Rikun moduulin tarkoitus oli asentaa Visual studio code, pip ja flask. Lisäksi haluttiin vscodeen python lisäosa, valita se komentotulkiksi sekä muuttaa vscoden teemaa.
3. Lisenssi
   - Sama lisenssi löytyy sekä tehtävää esittelevän weppisivun teksteistä, kuin githubin moduulin reposta.
5. Tekijä ja vuosi
   - Riku Mannonen 2021
7. Riippuvuudet:
   Asennettu toimiva Salt joka pyörii Linux käyttöjärjestelmän päällä. Distrovaatimuksia en varmaksi osaa sanoa. Testit tehty **Ubuntu 20.04 LTS** ja **Xubuntu 18.04.5 LTS**.
9. Kiinnostavaa
    - Testit oli toteutettu paikallisesti. Minua jäi kiinnostamaan onnistuuko sama etähallintaan. Sen vuoksi valitsin tämän.
11. Avoimet kysymykset ja muut huomiot
    - Millä edellytyksillä olisi voinut muuttaa VSCoden oletusmäärityksiä. Olisiko Flaskin näyttämän sivun voinut myös automatisoida Saltilla?
    
[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h6_Benchmark.md#h6-benchmark)
___ 

## c) Testbench

Tehtävän suoritus 02.05.5024 klo 14.30 - 15.20 ja 20.20 - 23.35 EET.

Tehtävässä tuli tarkistaa ajaa ja analysoida jokin yllä esitellyistä (Karvinen 2024). Valitsin Viimeiseksi esitellyn, sillä halusin testata sitä etähallintaan. Lisäksi halusin tarkastella löytyisikö syitä, miksi VSCoden määritykset eivät onnistuneet tilan avulla.

#### 1. Moduulin sisältö.
   - Aloitin tutkimalla sisältöä Git-hubista. Repoon sisältyi srv/salt hakesmisto, lisenssi, README-tiedosto, sekä high.sh-tiedosto jossa oli kirjattuna highstate-komento.
     ![h6-003](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h6-003.png)
   - **srv/salt**-hakemistossa oli **flask** ja **vscode** moduulit sekä **top.sls** tiedosto.
     - vs-code tilassa oli init.sls, Microsoftin GPG-avaintiedosto, microsoftin pakettilähdelista (nämä tarvitaan sillä VSCode ei sisälly Linuxin-jakeluiden oletuspakettivarastoihin), sekä oletusasetustiedosto jolla vscode määritellään käyttäjän mukaiseksi.
     - flask tilassa oli vain flaskin init.sls.
  
#### 2. Sisällön tarkistamisen jälkeen latasin kyseisen repon virtuaalikoneelleni doh001.
   - Otin yhteyden virtuaalikoneeseen, jossa master asennettu, siirtymällä hakemistoon jossa vagrantfile on `cd VagrantVMs/h4_demonit`. Siellä käynnistin virtuaalikoneet `vagrant up`. Koneiden käynnistyttyä otin yhteyden `vahrant ssh doh002`.

#### 3. Repon tuominen koneelle.
   - Loin **doh002**koneelle hakemiston gitin repoille antamalla käyttäjän kotihakemistossa `sudo mkdir code` komennon ja siirryin sinne `cd code`.
   - Kopioin repon etusivulla `code`-painikkeen local- välilehdeltä löytyvän repon HTTPS - urlin.
     ![h6-004](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h6-004.png)
   - `git clone https://github.com/riku-mannonen/moduuli.git` kloonasi rikun repon code - hakemistooni... Tai ei kloonannut kun git oli asentamatta. Korjasin tämän `sudo apt-get install git`. Tämän jälkeen kloonaus onnistui, tosin **srv/salt** repo typistyi nimeen **srv**.
     
     ![h6-005](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h6-005.png)
    - Siirryin `cd /srv/` hakemistoon, jossa ensin uudelleennimesin olemassaolevan salt-hakemiston `sudo mv -n salt salt_v1.0`, jotta sen sisältö ei suoritu Rikun moduulia testatessa.
     ![h6-006](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h6-006.png)
   - Kopioin tuodun repon **srv** hakemiston code hakemistosta srv hakemistoon `sudo cp -r /home/vagrant/code/moduuli/srv salt`.

#### 4. Omien virtuaalikoneiden valmistelu testaamista varten.
   - Jotta pystyin testaamaan VSCoden asennuksen onnistumista, tarvitsin koneen jota voi käyttää GUIn työpöytäympäristön kautta. Löytämässäni [ohjeessa](https://shanemcd.org/2018/12/16/adding-a-gui-to-a-debian-vagrant-box/) (Shane 2018) määriteltiin ensin vagrantfilessä virtuaalikone käynnistymään GUIn kautta tämän jälkeen virtuaalikoneelle oli asennettu XFCE. Itse halusin kokeilla myös tämän automatisointia suoraan Vagrantfilen kautta, joten lisäsin aiemmin kurssilla muokkaamaani vagrantfileen toisen skriptin doh002 koneelle. Skriptissä asennettiin samat ohjelmat kuin doh001-koneelle, mutta myös tasksel sekä XFCE (GCore 2023).
      <details>
        <summary>Avaa muokattu vagrantfile tästä</summary>
          
          # -*- mode: ruby -*-
          # vi: set ft=ruby :
          
          $tscript_doh002 = <<TSCRIPT
          set -o verbose
          apt-get update
          apt-get -y install ufw curl netcat micro bash-completion tasksel
            # Asenna XFCE työpöytäympäristö vain doh002 koneelle
          sudo tasksel install xfce-desktop
          echo "XFCE asennettu doh002"
          TSCRIPT
          
          $tscript_doh001 = <<TSCRIPT
          set -o verbose
          apt-get update
          apt-get -y install ufw curl netcat micro bash-completion
          echo "valmista doh001"
          TSCRIPT
          
          Vagrant.configure("2") do |config|
          	      config.vm.synced_folder ".", "/vagrant", disabled: true
          	      config.vm.synced_folder "shared/", "/home/vagrant/shared", create: true
          	      config.vm.box = "debian/bullseye64"
          
          	      config.vm.define "doh001" do |doh001|
          		            doh001.vm.hostname = "doh001"
          		            doh001.vm.network "private_network", ip: "192.168.88.101"
          		            doh001.vm.provision "shell", inline: $tscript_doh001
          	      end
          
              	config.vm.define "doh002", primary: true do |doh002|
                    		doh002.vm.hostname = "doh002"
                    		doh002.vm.network "private_network", ip: "192.168.88.102"
                    		doh002.vm.provision "shell", inline: $tscript_doh002
                    		doh002.vm.provider "virtualbox" do |vb|
                    			vb.gui = true
                    			vb.memory = "2048" 
                    		end
          	    end
           end
  
      </details>
   - Klo 22.30 päivitin koneet `vagrant reload` joka käynnisti myös virtualboxin graafisen ikkunan sekä työpöytäympäristön kirjautumisikkunan klo 22.38. Käyttis ja salasanan **vagrant** eivät toimineet, joten testasin nollata salasanan CLIn kautta komennolla `sudo passwd vagrant`. Tämä auttoi ja työpöytäympäristö aukesi.
     ![h6-008](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h6-008.png)
   
#### 5. Rikun moduulin testaaminen

- Siirryin **doh001** koneella `cd /srv/salt`ja annoin Rikun komennon `sudo salt-call --local state.highstate --file-root srv/salt`. Tämä ei tuottanut toivomaani tulosta.
  ![h6-010](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h6-010.png)
- Tarkistin komennon, hakemistojen sijainnit sekä topfilen syntaksin, jotka kaikki näyttivät toimivan. Ennen täsmällisempää vianetsintää kokeilin suorittaa `sudo salt '*' state.apply` josta sain onnistuneen palautteen.
 ![h6-009](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h6-009.png)
- Onnistuneen suorituksen jälkeen tarkistin vielä asennukset. Ensiksi Flask.
  ![h6-011](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h6-011.png)
- Sitten siirryin minionin työpöytäympäristöön josta avasin asennetun VSCoden, mutta kuten Riku totesi hänen luomat conffit eivät olleet asentuneet.
  ![h6-012](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h6-012.png)
  - Tarkastelin alkuun VSCoden init.sls tiedostoa, jossa mielestäni vscode/settings.json tiedosto oli oikein määritelty ja tila oli oikein kirjattu. En kuitenkaan osannut vahvistaa, onko kohdepolku asetuksille oikea. Muokkasin asennetun VSCoden määrityksiä valitsemalla teemaksi vaalean. Sitten etsin findin avulla vscoden asetustiedoston. Viime tehtävässäni harjoiteltu komento `sudo find -type f -printf '%T+ %p\n'|sort |tail -10 |nl` ei suoraan näyttänyt vscoden asetustiedostoa, mutta antoi vinkin oikeaan suuntaan.
    ![h6-013](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h6-013.png)
  - Pienen selailun jälkeen löysin settings-tiedoston jossa oli vaalea teema tallennettuna.
    ![h6-014](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h6-014.png)
    ![h6-015](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h6-015.png)
  - Korjasin tämän polun vscoden init.sls-tiedostoon eli tiedostopolun `/etc/skel/` tilalle tuli `/home/vagrant/.config/Code/User`:
    ![h6-016](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h6-016.png)
  - Tallensin ja suoritin moduulin uudelleen `sudo salt '*' state.apply`.
  - Palautteen mukaan asetustiedostoa muutettiin. Avasin VSCoden ja tarkistin.
    ![h6-017](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h6-017.png)
  - Tumma tila oli määrittynyt oikein, myös python löytyi vaikka Code ehdotti toista suositeltua versiota.
  - ![h6-018](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h6-018.png)
  - Sitä oliko python oletustulkki en osannut päätellä mistään, joten jos tämän tehtävän vertaisarvioijalla on siihen vinkkiä, kuulen hyvin mielelläni.
  
[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h6_Benchmark.md#h6-benchmark)
___ 

## d) Viisi ideaa

Listaa viisi ideaa omalle modulille, kurssin lopputehtävälle. Modulilla tulee olla tarkoistus. Sen ei tarvitse silti ratkaista mitään oikeaa liiketoiminnan ongelmaa, vaan tarkoitus voi olla keksitty (Karvinen 2024).


1. Ajatus mahdollisesti määrittää pien verkko jossa Master toimii adminina, mahdollisesti weppiserveri ja muutamia käyttäjiä joista yhdellä muokkausoikeus weppiserveriin.
2. Lähtötilanteessa tullee olla valmiina kaikki minionit määriteltyinä. Jos näin voiko luoda ja conffata valmiiksi vagrantfilen avulla?
3. Tuleeko työpöytä määrittää vagrantfilessä, vai voisiko sen tehdä jotenkin etähallinnan kautta?
4. Ilmeisesti suositeltavaa olisi kuitenkin mahdollisimman laajasti hoitaa asennukset etähallinan kautta?
5. Jos haluaa testata eri käyttöjärjestelmiä minioneille toimiiko alkumääritysten jälkeen nämä samoilla saltin komennoilla? Linuxin distroilla tämä ainakin lienee näin?




[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h6_Benchmark.md#h6-benchmark)
___ 

## Lähteet

Alpine Linux D-Bus, 2023. Luettavissa: https://wiki.alpinelinux.org/wiki/D-Bus. Luettu 02.05.2024.

Choi J. Install tmux on OSX and Basics Commands for Beginners, 2018. Luettavissa: Install tmux on OSX and Basics Commands for Beginners. Luettu 02.05.2024.

GCore, How to Install XFCE on Debian, 2023. Luettavissa: https://gcore.com/learning/how-to-install-xfce-on-debian/. Luettu 02.05.2024.

Karvinen T. Infra as Code - Palvelinten hallinta 2024. Luettavissa: https://terokarvinen.com/2024/configuration-management-2024-spring/#h6-benchmark. Luettu 02.05.2024.

Kulonpää S. ph-moduuli 2021. Luettavissa: https://github.com/samikul/ph-moduuli. Luettu 02.05.2024.

Mustonen J. Oma moduuli h7 2020. Luettavissa: https://jannelinux.design.blog/2020/05/19/oma-moduuli-h7/. Luettu 29.04.2024.

Salt Project - Windows package manager 2024. Luettavissa: https://github.com/therealhalonen/PhishSticks/blob/master/notes/ollikainen/windows.md. Luettu 02.05.2024

Shane Adding a GUI to a Debian Vagrant box, 2018. Luettavissa: Adding a GUI to a Debian Vagrant box. Luettu 02.05.2024.
