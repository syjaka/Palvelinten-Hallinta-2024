# Keskeneräinen

# h5 Tekniikoita

a) Asenna Salt Macille.

b) Kerää Windows- tai Mac-koneesta tietoa grains.items -toiminnolla.

c) Kokeile Saltin file -toimintoa Windowsilla tai Macilla.

d) CSI Kerava.

e) Komennus.

f) Vapaaehtoinen: Gui2fs.

g) Vapaaehtoinen: Ämpärillinen.

x) Lue ja tiivistä 

y) Käyttöympäristö

z) Alkutoimet



##  x) Lue ja tiivistä. 

Tehtävänä oli lukea ja tiivistää jokin aiempi kotitehtäväraportti Saltin käytöstä Windowsilla muutamaan riviin. Valitsin Johan Lindellin raportin vuodelta 2021.

- Alkuun johan kokeili asentaa Windowsiin VSCODEN, jotta hän varmistui sen toimivuudesta koneessaan. Onnistuneen asennuksen jälkeen VSCODE poistettiin ja varsinainen tehtävä alkoi.
- Johan asensi Salt Minionin ohjeiden mukaan ja asennuksen yhteydessä hän määritti masterin IP-osoitteen sekä minionin nimen asennusohjelmassa.
- Minionin asennuttua Johan asensi masterin sekä tallensi avaimet ja tarkisti `sudo salt '*' cmd.run 'whoami'`-komennollka että minion vastaa.
- Ennen vscoden asennusta windowsille piti asentaa git ja windows repot saltin srv hakemistoon. Lisäksi niiden oikeudet piti muuttaa siten että Saltilla on kirjoitusoikeus.
- `sudo mkdir -p /srv/salt/vscode` ja `sudoedit /srv/salt/vscode/init.sls` johan loi vscode-moduulin tavoitteena asentaa masterilla vscode minionille.
- `sudo salt '*' state.apply vscode` komento suoritti onnistuneen VSCODE-asennuksen.
  (Lindell 2021)

Saltin asennus tässä raportissa oli suoritettu GUI:n kautta. Jäin pohtimaan tämän tavan etuja ja haittoja suhteessa komentorivin kautta tapahtuneeseen asewnnukseen. Ainakin minionin conf-tiedoston päivittäminen näytti sujuneen helposti..

## y) Käyttöympäristö

Tehtävä toteutettiin MacBook Retina 12-inch, koneella jossa, host OS on Ventura 13.6.1 käyttöjärjestelmä Suomen maa-asetuksilla ja suomen kielellä. Koneessa on 1,3GHz kaksiytiminen Intel Core i5 prosessori ja 8Gt 1867 MHz LPDDR3 muistia. Näytönohjain on Intel HD Graphics 615 jossa VRAM 1536 Mt.

Koneeseen asennettu Vagrant versio on 2.4.1.
d, e ja - kohdassa virtuaalikoneet ovat Linux Bullseye 5.10.0-28-amd64.
f - kohdassa Virtualbox Version 7.0.12 ja Debian GNU/Linux 12 (bookworm).

  
##  a) Asenna Salt Windowsille tai Macille. Osoita 'salt-call --local' komentoa ajamalla, että asennus on onnistunut. 
(Jos olet asentanut jo aiemmin, tässä riittää pelkkä asennuksen testaaminen, eikä asennusta tarvitse tehdä uudelleen.)
- Olin suorittanut asennuksen jo luennon jälkeen joten en tee sitä uudelleen. Maciin asennettaessa asennus erosi siinä mnäärin, että SRV-hakemistoa ei Macin omien turvallisuusrajoitusten vuoksi voi sisällyttää juurihakemistoon. Sen vuoksi loin hakemistopolun `/Library/srv/salt` jonne tallennan vastaisuudessa saltin tilatiedostot.
- Jotta Salt löytää luodut tilatiedostot päivitin vielä masterfileen luodun polun.
  !h5-001
- Olin myös luonut **hello**-tilan jonka toteuttamaa tiedostonimeä muokkasin vähän ja testasin onnistuneesti komennolla `sudo salt-call --local state.apply hello`
  !h5-002

b) Kerää Windows- tai Mac-koneesta tietoa grains.items -toiminnolla. 
Poimi 'grains.item' perään muutamia keskeisiä tietoja ja analysoi ne, eli selitä perusteellisesti mitä ne ovat. Kuvaile ja vertaile numeroita(Karvinen 2024).

- Komento `sudo salt-call --local grains.items` näyttää kaikki saatavilla olevat tiedot järjestelmästä avain-arvo pareina.
- Annoin komennon `sudo salt-call --local grains.item saltversioninfo saltpath virtual` jolla valtisin näytettävät seikat. Komento näytti:
  !h5-003
  1. **saltversioninfo**
     Saltin versiotiedot jossa 3007 edustaa pääversiota ja ,0 aliversiota.
  3. **saltpath**
     Kesroo saltin asennuskansion polun.
  5. **virtual**
     Kertoo järjestelmän virtualisoinnin tilan joka on tällä hetkellä physical eli ei virtualisointia.

## c) Kokeile Saltin file -toimintoa Windowsilla tai Macilla.
- Tästä osan olin jo tehnyt kohdassa a), kun käytin hello tilaa.
- Saman voisi toteuttaa suoralla komennolla `sudo salt-call --local  state.single file.managed /Library/salt/srv/tmp/testi.md`, joka palautti onnistuneen tiedoston luonnin
  !h5-004
- Tarkistus vielä tmp hakemistosta näytti tiedoston olevan paikallaan.
  !h5-005
- Tiedoston poisto tapahtui komennolla `sudo salt-call --local -l info state.single file.absent /Library/salt/srv/tmp/testi.md`.
- !h5-006
(Karvinen 2021)
  
## d) CSI Kerava. 
Tehtävän suoritus 29.04.2024 klo 15.32 - 16.11 EET.

Näytä 'find' avulla viimeisimmäksi muokatut tiedostot /etc/-hakemistosta ja kotihakemistostasi. Selitä kaikki käyttämäsi parametrit ja format string 'man find' avulla (Karvinen 2024).

Tehtävää suorittaessa piti palata Karvisen 17.04 luentomuistiinpanoihin joissa CSI-Kerava oli hyvin selitetty. Sieltä löysin avun Find-komennon jäsentämisen alkuun, siten että tulostetta olisi mahdollista jatkojalostaa.

1. Aloitin tehtävän siirtymällä viime viikon tehtävässä luotuun doh001 virtuaalikoneeseen. Tätä varten siirryin ensin kansioon jossa koneiden vagrantfile on eli `cd /Users/kadriyesamaletdin/VagrantVMs/h4Demonit` ja siellä komento `vagrant up` käynnisti koneet.
2. `vagrant ssh doh001` otti yhteyden doh001 koneeseeni.
3. Yhteyden saatuani siirryin `cd /etc` hakemistoon ja kokeilin ensin `find|nl`-komentoa joka tulosti kaikki kaikki tiedostot ja hakemistot työhakemistossa omille riveilleen numeroituina. Näitä oli 1316 joten sorttaamista tarvittiin.
4. Avasin komentoriviltä findin manuaalin `man find`. Helpin kautta löytyi ohje hakusanahakuun, eli /hakusana ja `n` tai `Shift + n` selasi tuloksia eteen ja taakse.
6. Teron 17.04 luennolta olin poiminut talteen komennon `find -printf '%T+ %p\n'|sort `, jonka toimia selvittelin ** man find** avulla:
   - `-printf` on printformat eli tulostaa hakutulokset omien pyydettyjen parametrien mukaisesti.
   - `'%T+ %p\n'` jossa `%T` esittää tiedoston muokkauksen viimeisen ajankohdan, `+` määrittää tämän ajankohdan päivämääräformaatin ISO806 formaattiin, `%p` tulostaa tiedostonimen ja  `/n` eli new line määrittää tulosteen tiedostot omille rivilleen.
   - Lisäsin komennon loppuun vielä seuraavat `|tail -10 |nl`, jossa`|sort` lajittelee päivämääräjärjestyksessä `|näyttää 10 viimeistä` sekä `|nl` numeroi rivit.
   Tämä komento tulostaa siis ym. parametreillä työhakemiston tiedostot kuten alla:
   !h5-007
7. Tehtävänannossa pyydettiin etc-hakemiston sekä kotihakemiston **tiedostot** joten komentoon tuli lisätä `/etc /home`ja rajaus vain tiedostoihin `-type f`. Lisäksi edellinen hakutulos antoi yhteen tiedostoon *permission denied* joten lisäsin sudon komennon alkuun. Näin ollen komento `sudo find /etc /home -type f -printf '%T+ %p\n'|sort |tail -10 |nl`näytti
   !h5-008
Osion lähteet Karvisen 17.04.2024 luentomuistiinpanot sekä Find manuaali.

e) Komennus. Tee Salt-tila, joka asentaa järjestelmään uuden komennon.

Tehtävän suoritus 29.04. klo 16.15 - 17.51 EET.

Jatkoin tehtävää edellisen tehtävän doh001-virtuaalikoneella. 

1. Aloitin luomalla uuden komennon
   - Siirryin kotihakemistooni `cd` ja loin sinne oman hakemiston komennoille `mkdir komennot`.
   - Siirryin luotuun hakemistoon `mkdir komennot`ja loin sinne uuden tiedoston `micro tervehdi`.
   - Tallensin tiedostoon scriptin joka tervehtii käyttäjää ja ketoo ajankohdan:

         #!/usr/bin/bash

         echo "Hauska tavata $1!" #poimii komennon perään annetun syötteen esim bash tervehdi Kadi
         echo "Tervetuloa $USER!"
          
         PAIVA=$(date +"%Y-%m-%d")
         AIKA=$(date +"%H:%M")
          
         echo "Tänään on $PAIVA ja kello on $AIKA +3UCT."
   - Komento `bash tervehdi Kadi`testasi ja osoitti komennon toimivuuden
     !h5-009
   - Seuraavaksi muutin komennon käyttöoikeiuksia site että kaikilla käyttäjillä on oikeudet ajaa komento `chmod ugo+rx tervehdi`.
    !h5-010
   - `sudo cp tervehdi /usr/local/bin/` kopioi komennon sijaintiin jossa sen suorittaminen on mahdollista käyttäjästä riippumatta.
   - Testasin vielä luomalla uuden käyttäjän "tavis" `sudo adduser tavis`, vaihtamalla käyttäjäksi tavis `su tavis` ja ajamalla komennon `bash tervehdi Maailman kuningas`. 
     !h5-011
     (nyt huomasin että koneeni kello on UCT ajassa joten komennon tulosteen aikavyöhykeleiman voisi korjata pois)
1. Seuraavaksi Salt-tilan luonti.
   - Siirryin Saltin srv hakemistoon `cd /srv/salt/` ja loin sinne uuden hakemiston `sudo mkdir -p komennot/temp`.
   - Kopioin **tervehdi**-komennon komennot/temp hakemistoon `sudo cp /home/vagrant/komennot/tervehdi /srv/salt/komennot/temp`
   - Hakemistoon tallensin `sudo micro init.sls`-tiedoston tervehdi tilaa varten. Sinne tallensin:

         /usr/local/bin/tervehdi: # Lisättävän tiedoston polku
             file.managed: # suoritettava toimi eli lisätään tiedosto
               - source: "/srv/salt/komennot/temp/tervehdi" # lisättävän tiedoston lähde
   - Ennen testaamista poistin aiemmin kopioidun **tervehdi** tiedoston tilan kohdekansiosta `sudo rm -r /usr/local/bin/tervehdi` sekä omasta kotikansiosta `sudo rm -r /home/vagrant/komennot/tervehdi`
     !h5-012
   - Testasin paikallisesti `sudo salt-call --local state.apply komennot`, sekä `bash tervehdi` ja sain onnistuneen palautteen.
     !h5-013
   - Ennen minionille testausta avasin toisen komentorivi-ikkunan jossa otin yhteyden minioniin `vagrant ssh doh002`.
   - Testasin minionille `sudo salt '*' state.apply komennot`, joka palautti virheen, että lähdetiedostoa ei löydy annetusta polusta.
     !h5-014
   - Palasin tarkastelemaan edellisen viikon repoani ja lähdetiedoston viitettä ja huomasin eroavaisuuden suoran tiedostopolun suhteen. Muokkasin lähdetiedoston polun muotoon `- source: "salt://komennot/temp/tervehdi"` ja testasin `sudo salt '*' state.apply komennot`, sekä onnistuneen suorituksen jälkeen minionilla `bash tervehdi` (syjaka 2024).
   - !h5-015
   
  
f) Vapaaehtoinen: Gui2fs. 
Tehtävän suoritus 29.04 klo 18.05 - 19.02 EET.
Muokkaa asetuksia jostain graafisen käyttöliittymän (GUI) ohjelmasta käyttäen ohjelman valikoita ja dialogeja. Etsi tämä asetus tiedostojärjestelmästä (Karvinen 2024).

Tätä tehtävää varten käynnistin ensin virtualboxin ja sieltä viime periodilla asennetun debianin **KadinDeb**. 
- Debianin guin auettua valitsin vasemman yläreunan applications valikosta settings ja desktop jossa muutin työpöydän ikonien kokoa sekä työpöydän taustakuvaa.
  !h5-016
- Siirryin komentoriville ja komennolla `sudo find  -type f -printf '%T+ %p\n'|sort |nl` hain muokatut tiedostot lajiteltuna uusin muokkaus ensin.
  !h5-017
- Hakutulos paljasti siis tiedostot joissa työpöytäasetuksien muutokset ovat.
- Tarkastelin ensimmäisen sisältöä `cat .config/xfce4/desktop/icons.screen0-1204x957.rc`. Tähän oli tallentunut muutoksia joiota tein työpöydän ikonien kokoon.
  !h5-018
- Toisen tiedoston sisältö näytti taustakuvan määritykset ´cat ./.config/xfce4/xfconf/xfce-perchannel-xml/xfce4-desktop.xml` Tiedoston backgroung kohdasta löysin taustakuvan asetuksen
  !h5-019

g) Vapaaehtoinen: Ämpärillinen. 

Tehtävän suoritus 29.04 klo 19.05 - 
Tee Salt-tila, joka asentaa järjestelmään kansiollisen komentoja. Tee tila käytten recurse (tms) parametria niin, että et joudu luettelemaan jokaista asennettaa komentoa ja skriptiä eriksiin sls-tiedostossa (Karvinen 2024).

1. Jatkoin tehtävää koneella **doh002** jonne alkuun loin kansion `sudo mkdir -r amparillinen/temp`.
   !h5-020
2. Temp kansioon loin komennot `backup`, `koneinfo`, `tervehdi` ja `update`. Jokaisen komennon luonnin jälkeen testasin myös niiden toiminnan.
   !h5-021
3. Annoin riittävät oikeudet tiedostoihin komennolla `sudo chmod u=rwx,g=rx,o=rx backup  koneinfo  tervehdi  update` ja tarkistin että luoduolla kansioilla on riittävät oikeudet.
   !h5-022
4.  Seuraavaksi loin **init.sls**-tiedoston **amparillinen**-hakemistoon komennolla `micro init.sls`.

        kopioi komennot:
          file.recurse: 
            - name: /usr/local/bin
            - source: salt://amparillinen/temp 
5.  Testasin paikallisesti `sudo salt-call --local state.apply amparillinen` ja vastoi kaikkia todennäköisyyksiä testi onnistui.
    !h5-023
6.  Testasin minionille `sudo salt '*' state.apply amparillinen` onnistuneesti.
7.  !h5-024
8.  Vielä viimeiseksi testit minionilla että komennot toimii. Suoritin testin tavallisena käyttäjänä jonka loin doh002 koneessa `sudo adduser tavis`ja vaihdoin luotuun käyttäjään `su tavis`.
    - Komento `bash backup` toimi kyllä odotetusti, mutta ongelmia tuli itse skriptin kanssa, sehän ei normikäyttäjänä ja minionissa toimi. Korjaan skroptin mahdollisesti myöhemmin.
    - Komennot `bash koneinfo` ja `bash tervehdi` toimivat odotetusti.
    - Komentoa `bash update` varten tajusin vaihtaa rootiksi ja sekin toimi mutkitta.
    !h5-025

## Lähteet:

Karvinen T.  Infra as Code - Palvelinten hallinta - Tekniikoita, 2024. Luettavissa: https://terokarvinen.com/2024/configuration-management-2024-spring/#h5-tekniikoita. Luettu 29.04.2024.

Karvinen T. Run Salt Command Locally, 2021. Luettavissa: https://terokarvinen.com/2021/salt-run-command-locally/. Luettu 29.04.2024.

Lindell J. Palvelinten Hallinta - Harjoitus 6 - Windows - 10.05.2021. Luettavissa: https://johanlindell.fi/palvelintenhallinta#h4. Luettu 29.04.2024

Kadi Syrjä/syjaka, Palvelinten-hallinta, h4 Demoni 2024. Luettavissa : https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h4_Demoni.md#e-vapaaehtoinen-apache. Luettu 29.04.2024

Kadi Syrjä h7-maalisuora, 2024. Luettavissa: https://github.com/syjaka/Linux-Palvelimet-2024/blob/main/h7_maalisuora.md#b-seuraavaksi-tein-uuden-skriptin-ja-asetin-sen-kaikkien-saataville. Luettu 29.04.2024.


<details>
<summary>Näytä lisää tekstiä</summary>

Tässä on lisää tekstiä, joka piilotetaan, kun alasvetonuolta ei ole avattu.
Voit kirjoittaa tänne mitä haluat!

</details>

