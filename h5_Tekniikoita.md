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
z- kohdassa määritetyt virtuaalikoneet ovat Linux Bullseye 5.10.0-28-amd64.

  
##  a) Asenna Salt Windowsille tai Macille. Osoita 'salt-call --local' komentoa ajamalla, että asennus on onnistunut. 
(Jos olet asentanut jo aiemmin, tässä riittää pelkkä asennuksen testaaminen, eikä asennusta tarvitse tehdä uudelleen.)
- Olin suorittanut asennuksen jo luennon jälkeen joten en tee sitä uudelleen. Maciin asennettaessa asennus erosi siinä mnäärin, että SRV-hakemistoa ei Macin omien turvallisuusrajoitusten vuoksi voi sisällyttää juurihakemistoon. Sen vuoksi loin hakemistopolun `/Library/srv/salt` jonne tallennan vastaisuudessa saltin tilatiedostot.
- Jotta Salt löytää luodut tilatiedostot päivitin vielä masterfileen luodun polun.
  !h5-001
- 

b) Kerää Windows- tai Mac-koneesta tietoa grains.items -toiminnolla. Poimi 'grains.item' perään muutamia keskeisiä tietoja ja analysoi ne, eli selitä perusteellisesti mitä ne ovat. Kuvaile ja vertaile numeroita.

  
c) Kokeile Saltin file -toimintoa Windowsilla tai Macilla.

  
d) CSI Kerava. Näytä 'find' avulla viimeisimmäksi muokatut tiedostot /etc/-hakemistosta ja kotihakemistostasi. Selitä kaikki käyttämäsi parametrit ja format string 'man find' avulla.
  
e) Komennus. Tee Salt-tila, joka asentaa järjestelmään uuden komennon.
  
f) Vapaaehtoinen: Gui2fs. Muokkaa asetuksia jostain graafisen käyttöliittymän (GUI) ohjelmasta käyttäen ohjelman valikoita ja dialogeja. Etsi tämä asetus tiedostojärjestelmästä.


g) Vapaaehtoinen: Ämpärillinen. Tee Salt-tila, joka asentaa järjestelmään kansiollisen komentoja. Tee tila käytten recurse (tms) parametria niin, että et joudu luettelemaan jokaista asennettaa komentoa ja skriptiä eriksiin sls-tiedostossa.


## Lähteet:

Karvinen T.  Infra as Code - Palvelinten hallinta - Tekniikoita, 2024. Luettavissa: https://terokarvinen.com/2024/configuration-management-2024-spring/#h5-tekniikoita. Luettu 29.04.2024.

Lindell J. Palvelinten Hallinta - Harjoitus 6 - Windows - 10.05.2021. Luettavissa: https://johanlindell.fi/palvelintenhallinta#h4. mLuettu 29.04.2024
