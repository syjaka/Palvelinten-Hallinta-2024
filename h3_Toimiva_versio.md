Selitä tuon komennon jokainen osa. Käytä apuna itse valitsemiasi lähteitä ja viittaa niihin.
### 3. Varaston [terokarvinen/suolax/](https://github.com/terokarvinen/suolax/) historia - 11.4 klo 12.45 - 13.30 EET
eli loki ja muutokset (Karvinen 2024).
   - Tein tehtävän komentorivin kautta.
         ![h3-003](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-003.png)
7. Paitsi ei tunkenutkaan, vaan vain "lavasti" ja teki commitin. Eli lisäsin myös `git push` komennon, ja homma toimi.
2. Analyysiä 
    - **Commit** on kyseisen commitin yksilöllinen tunniste eli SHA-1 arvo.
    - **Author** näytti nimeni ja meiliosoitteeni. Nämä säädin oikeaksi jo eilisellä tunnilla käyttäen komentoja `git config --global user.email "mun meili"` ja `git config --global user.name "mun nimi"`.
    - **Date** kertoi commitin ajankohdan. Tässä ekan ja tokan välillä ristiriita, sillä virtuaalikoneeni ei ollut ajan tasalla.
    - Seuraavaksi näkyi Commit messaget, tässä kahden commitin **initial commit** ja **add file vamos**.
    - Kuvassa jää **Initial commit** vajaaksi sillä lisenssin 1 674 rivin jälkeen siellä näkyy vielä commitin README-filen lisäysosuus.
1. Aloitin asentamalla Gitin ja muuta, sekä Määrittämällä Githubin repon koneen käyttöön:
   - Loin ssh avainparin `ssh-keygen`+ 3  x `return`.
   - Kopioin julkisen avaimen `cat /home/vagrant/.ssh/id_rsa.pub` ja liitin sen Githubin settings sivun SSH and GPG keyes - osioon. Tämä autentikoin k002 muokkaamaan **syjaka*-tilin Githubia.
   - Annoin komennot `git config --global user.email "kadriye.syrja@myy.haaga-helia.fi"` ja `git config --global user.name "Kadi Syrjä @k001"` ja kokeilin  uudelleen `git add . && git commit; git pull && git push`, joka onnistuneesti päästi tallentamaan commitin. Kuvassa lopputulos Githubissa.
5. Tein vielä topfilen, jolle voi antaa eri konetyyppejä, joiden mukaan taas se osaa asentaa eri konetyypeille määrätyt moduulit.
6. Vielä viimeiseksi `git add . && git commit; git pull && git push`.
Kokeilin Gittiä oman emokoneeni käyttöjärjestelmällä. Minulla on jo *brew* asennettu, joten asensin sen avulla Gitin käyttäen komentoa `brew install git`. Mikäli **brewtä** ei olisi ollut, olisi sen asennus onnistunut komennolla `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`
   - Commit-ruutu aukesi **vimillä**, sillä en ollut asentanut microa koneelle.
   - Testasin vielä muokkaamalla **makilla.uusi** tiedostoa ja synkkaamalla sen Githubiin. Nyt aukesi toivottu editori. 
### jatkoa - 16.04.2024 klo 13.00 -  14.10

7. Alkuun käynnistin virtuaalikoneeni jolla olin tehtävän tehnyt ja otin siihen SSH-yhteyden.

       kadriyesamaletdin@Kadriye-MacBook ~ % cd twohost 
       kadriyesamaletdin@Kadriye-MacBook twohost % vagrant up
       kadriyesamaletdin@Kadriye-MacBook twohost % vagrant ssh k002 # lopputuloksena:
       vagrant@k002:~$
   
9. Toveri NicklasHH samalta kurssilta, salli minulle mahdollisuuden muokata repoaan. Ilmoitus tuli kutsuna mun Github tilille:
   ![h3-027](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-027.png)
11. Painettuani  `accept invitation` siirtyi selain Nicklaksen kyseisen repon sivulle. Yläpalkkiin tuli ilmoitus, että minulla on nyt oikeus lisätä tähän repoon muokkauksia (NicklasHH 2024).
12. Siirryin virtuaalikoneellani `cd code` hakemistoon jossa minulla oli jo aiemmin luomani gitin repo.
13. Selaimessa `code` napin alta kopioin Nicklaksen repon HTTPS - urlin. Annoin tämän virtuaalikoneelleni muodossa `git clone https://github.com/NicklasHH/summer-task.git`.
   ![h3-028](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-028.png)
14. Siirryin kopioituun hakemistoon ja `ls` näytti, että sisältö tuli kloonatuksi.
   ![h3-029](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-029.png)
15. Loin repoon uuden tiedoston **kadinTiedosto*.
   ![h3-030](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-030.png)
16. `git add . && git commit; git pull && git push` Teki muutoksesta commitin, mutta Nicklaksen Githubiin ajettaessa tuli virhe.
   ![h3-031](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-031.png)
17. Virheen ehdottamasta URLista löytyi lisätietoa asiaan. Salasanatunnistautuminen ei ole enää mahdollinen, vaan täytyy luoda token (Github Docs 2024). Tokenin luonti onnistuu oman sivuni asetusten ja sieltä löytyvien **developer settings** kautta.
   ![h3-032](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-032.png)
18. Täällä Github suosittelee käytettäväksi Beta-kehitysvaiheessa olevaa **Fine-grained tokenia**, jota klikkaamalla aukesi tokenin luontia varten sivu. (Github Docs/Tokens 2024)
19. Sivulla loin uuden tokenin. Tämän specseissä en ollut ihan varma, mitä kaikkia oikeuksia tulisi antaa. Klikkailin tarpeellisiksi katsomani ja kopioin valmiin tokenin salasanani tilalle CLIn kysellessä salasanaa. Tämäkään ei auttanut.
   ![h3-033](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-033.png)
21. Tässä vaiheessa testasin selaimella, että minulla oli riittävät oikeudet repoon luomalla selaimen kautta **KadinTiedosto**n. Tämä onnistui.
22. Päivitin tämän paikalliseen gitiin komentorivilläni `git pull`.
21. Testasin yksinkertaisempaa Classic-tokenia jonka määritykset olivat selkeämmät. Luonti onnistui samaa kautta kuin edellisen luonti eli `generate new token`. Sitä ennen olin muokannut tiedostoa jotta oli jotain päivitettävää.
   ![h3-034](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-034.png)
22. `git add . && git commit; git pull && git push` ja salasanan tilalle luotu classic token toi toivotun lopputuloksen
   ![h3-035](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-035.png)
23. Selaimella tarkistus paljasti saman.
   ![h3-036](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/images/h3-036.png)

Github Docs, About remote repositories 2024. Luettavissa: https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories#cloning-with-https-urls. Luettu 16.04.2024

Github Docs, Tokens 2024. Luettavissa: https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens.mLuettu 16.04.2024

Karvinen T. Github Suolax 2024. Luettavissa: https://github.com/terokarvinen/suolax/tree/main. Luettu 10.04.2024

Åkerman N. Github summer-task 2024. Luettavissa: https://github.com/NicklasHH/summer-task. Luettu 16.04.2024