# h7 Oma miniprojekti

Miniprojektini tarkoitus on saltia hyödyntäen luoda yksityinen verkko jossa on verkkosivuja hostaava webserver, verkkosivuja hallinnoiva muutoin tavallisia oikeuksia omaava käyttäjä webadmin. Lisäksi luon admin ja tavallisen käyttäjän jotta ylläpitotoimia voi suorittaa muutoin kuin roottina, sekä testata tavallisena käyttäjänä.

Tässä raportissa käyn askeleitain läpi miten loin oman miniprojektini. Varsinaiset tilat olin luonut jo valmiiksi,tätä raporttia kirjoitettaessa mutta  tiloja testatessani  "puhtaalla pöydälla" selostan samalla stepit, mitä tein. Pääsääntöisinä lähteinä olen käyttänyt tämän kurssin - Palvelinten hallinta - raporttejani. Niiltä osin kun muita lähteitä on käytetty, on ne merkitty tekstiviitteisiin ja lähdeluetteloon.

a) Alkutoimet

d) Varsinainen moduulin luonti

z) Käyttöympäristö



---
##  a) Alkutoimet

#### 1) Vagrant ja saltin käyttöönotto

Koska aavistelin projektin luonnin ja testaamisen vaativan useamman vagrantkoneen luontia, conffasin Vagrantfilen joka luo kolme konetta.
1. Salt masterin jossa tarvitut ohjelmat asennettu.
2. Kaksi salt minionia, webadmin ja webserver joissa salt-minion asennettu ja masterin IP-osoite, sekä minionID määritetty. Lisäksi webadmin koneelle työpöytäympäristö. Tarkoituksena on luoda webadmin käyttäjä joka koneeltaan voi ottaa etäyhteyden webserveriin ja ylläpitää siellä hostattuja verkkosivuja.

<details>
<summary>Avaa vagrantfile kokonaisuudessaan tästä</summary>

          
  
</details>

Loin kotihakemistoni vagrantVMs hakemistoon miniprojektihakemiston jonne kopioin luodun vagrantfilen ja loin suunnitellut virtuaalikoneet "vagrant up".
Koneiden käynnistyttyä otin ssh yhteydet kaikkiin koneisiin kolmeen eri terminaali-ikkunaan:
1. `vagrant ssh saltmaster`
2. `vagrant ssh webadmin`
3. `vagrant ssh webserver`

Yhteyksien auettua testasin että asiat toimi:
- `sudo salt-key` tulosti hyväksymistä odottavat avaimet, eli vagrantfilen määritykset olivat onnistuneet.
  !h7-001
- Testasin että masterille oli asentunut haluamani ohjelmat.
- Webserverin gui kirjautuminen ei onnistunut esitetyn salasanavirheen takia. Nollasin salasanan webserverin terminaalista `sudo passwd vagrant`. Tämän jälkeen kirjautuminen onnistui.
  Lisäksi työpöytä ei käynnistynyt automaattisesti, mutta `startxfce4` auttoi.

Koska salt oli valmiiksi asennettu ja määritelty, käyttöönotto ja yhteys minioneihin avautui `sudo salt-key -A`ja `y`.
!h7-002

#### 2) Gitin käyttöönotto

1. Salt masterilla loin ssh avainparin `ssh-keygen` joka loi ssh avaimet oletushakemistoon - /home/vagrant/.ssh/id_rsa. Tulostin sieltä terminaaliin julkisen avaimen `cat /home/vagrant/.ssh/id_rsa.pub`, jonka taas liitin omaan githubiini asetussivun SSH and GPG keys, SSH keys -osioon.
2. Siirryin koneellani kotihakemistooni luotuun /home/vagrant/code hakemistoon jonne kloonasin githubin repon `git clone git@github.com:syjaka/h7_Oma_miniprojekti.git`.  

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h7_Oma_miniprojekti.md#h7-oma-miniprojekti)

---

## d) Varsinainen moduulin luonti

1. Hello world testaa että kaikki toimii
    - Siirryin `cd srv` hakemistoon jonne luoin `sudo mkdir salt`-hakemiston.
    - Loin tuonne helloworld tilan `mkdir helloworld` jonne loin `sudo micro init.sls` tiedoston
      <details>
      <summary>helloworld init.sls tästä</summary>
        
          /tmp/helloworld.txt:
            file.managed
      </details>
    - `sudo salt '*' state.apply helloworld` palautti onnistuneen ajon molemmille koneille
      !h7-003
    - Tarkistus molemmilla koneilla osoitti että helloworld.txt tiedosto löytyi.

2. Palomuurin asentavan tilan luonti.
    - Masterille oli asennettu ja conffattu palomuuri jo vagrantfilen määrityksissä. Molemmille orjille tuli asettaa tämä toimintaan. Myös SSH, HTTP, ja saltin käyttämät portit tuli jättää auki.
    - Loin salt hakemistoon ufw hakemiston jonne tallensin init.sls tiedoston
      <details>
      <summary> ufw init.sls tästä</summary>
      
          ufw:
            pkg.installed
          
          ufw.service:
            service.running:
              - name: ufw
              - enable: True
              - watch:
                  - cmd: 'ufw enable'
                  - cmd: 'ufw allow 22/tcp'
                  - cmd: 'ufw allow 80/tcp'
                  - cmd: 'ufw allow 4505/tcp'
                  - cmd: 'ufw allow 4506/tcp'
          
          'ufw enable':
            cmd.run:
              - unless: "ufw status verbose |grep 'Status: active'"
          
          'ufw allow 22/tcp':
            cmd.run:
              - unless: "ufw status verbose |grep '^22/tcp' "
          
          'ufw allow 80/tcp':
            cmd.run:
              - unless: "ufw status verbose |grep '^80/tcp' "
              
          'ufw allow 4505/tcp':
            cmd.run:
              - unless: "ufw status verbose |grep '^4505/tcp' "
          
          'ufw allow 4506/tcp':
            cmd.run:
              - unless: "ufw status verbose |grep '^4506/tcp' "

      </details>
    - `sudo salt '*' state.apply ufw` suoritti tilan onnistuneesti. Tässä kohtaa tosin jäi ongelma, sillä palomuurin asennus katkaisi yhteyden minioneihin. Yhteyden onnistui palauttaa uudelleenkäynnistämällä minion paikallisesti, joka ei tietenkään ole tarkoituksenmukaista. Vaihtoehdoksi jäi joko jättää palomuuri pois tai hyväksyä tämä kunnes keksin miten asian voi korjata. Jotta moduulia voisi muuten testata kokonaisuudessaan jätän palomuurin kokonaan asentamatta mikäli en löydä ratkaisua tähän.

      
3. Seuraavaksi loin käyttäjät luovan moduulin
    - Loin salt hakemistoon user hakemiston jonne tallensin init.sls tiedoston. Tavoitteena oli luoda tila, joka lukee tiedostosta luotavat käyttäjät. Tähän en löytänyt keinoa, joten listasin käyttäjät suoraan tilaan.
      <details>
      <summary> user init.sls tästä</summary>
        
          create_groups:
            group.present:
              - names:
                - webserver
          
          admin:
            user.present:
              - name: admin
              - fullname: Admin
              - shell: /bin/bash
              - uid: 1001
              - groups:
                - users
                - sudo
                - webserver
              - home: /home/admin
              - password: $1$bTZqB.KC$M1Silm8xtymp4nhSyRa0x0   # Admin
          
          webadmin:
            user.present:
              - name: webadmin
              - fullname: User One
              - shell: /bin/bash
              - uid: 2001
              - groups:
                - users
                - webserver
              - home: /home/webadmin
              - password: $1$m61LQpa5$KICoJcAk7O.XWzu3/YcYB1    # User One
          
          basic:
            user.present:
              - name: basic
              - fullname: User Two
              - shell: /bin/bash
              - uid: 3001
              - groups:
                - users
              - home: /home/basic
              - password: $1$z6y5IghC$sgtr0efVyO1aF9MP443On/    # User Two
      <details>
    - `sudo salt '*' state.apply user` loi onnistuneesti määritellyt kolme käyttäjää sekä webserver käyttäjäryhmän johon webadmin liitettiin.
4. Loin webadmin ja web servereille molemmille omat apps-tilatsalt hakemistoon, jotka asentavat koneille niiden tarvitsemia perus ohjelmia.
       <details>
          <summary> usrApps init.sls tästä</summary>esh
    
            usrApps:
              pkg.installed:
                - pkgs:
                  - git
                  - bash-completion
                  - pwgen
                  - micro
                  - ssh
                  - tree
                  - wget
                  - curl
        <details>
    - `sudo salt webadmin state.apply usrApps`asensi webadminille halutut ohjelmat
5. Viimeisenä nginx asensi webserverille nginxin vastaamaan sivusta testi.com ja localhost
    - Loin salt hakemistoon nginx hakemiston jonne tallensin:
      <details>
      <summary> nginx init.sls tiedoston</summary>

          nginx:
            pkg.installed
          
          /etc/nginx/sites-available/testi.com:
            file.managed:
              - source: "salt://nginx/tmp/testi.com"
           
          /etc/nginx/sites-enabled/default:
             file.absent
          
          /etc/nginx/sites-enabled/testi.com:
            file.symlink:
              - target: "../sites-available/testi.com"
           
          /home/vagrant/nginx:
             file.directory:
               - name: /home/vagrant/nginx/
               - group: webserver
               - dir_mode: 775
          
          /home/vagrant/nginx/public_html:
             file.directory:
               - name: /home/vagrant/nginx/public_html/
               - group: webserver
               - dir_mode: 775
          
          /home/vagrant/nginx/public_html/index.html:
             file.managed:
               - source: "salt://nginx/tmp/index.html"
               - group: webserver
               - mode: 664
          
          /etc/hosts:
                 file.managed:
                   - source: "salt://nginx/tmp/hosts"
          
          nginx.service:
            service.running:
              - name: nginx
              - enable: True
              - restart: True
              - watch:
                - file: /etc/nginx/sites-available/testi.com
                - file: /etc/nginx/sites-enabled/testi.com
                - file: /home/vagrant/nginx/public_html/index.html
      <details>



   - Sekä tmp hakemiston jossa oli lähdetiedostot joihin init.sls tiedostossa viitataan
     <details>
      <summary> tmp hakemiston tiedostot </summary>
     hosts:
                    
                              127.0.0.1	localhost testi.com
                              127.0.0.2	bullseye
                              ff02::1		ip6-allnodes
                              ff02::2		ip6-allrouters
                              
                              127.0.1.1 webserver webserver
                    
     index.html:
                    
          
                  <!DOCTYPE html>
                  <html lang="en">
                  <head>
                      <meta charset="UTF-8">
                      <meta name="viewport" content="width=device-width, initial-scale=1.0">
                      <title>Salt-installed NGINX Test Page</title>
                      <style>
                          body {
                              font-family: Arial, sans-serif;
                              margin: 0;
                              padding: 0;
                              background-color: #f4f4f4;
                              color: #333;
                              text-align: center;
                              padding-top: 50px;
                          }
                          h1 {
                              font-size: 36px;
                              margin-bottom: 20px;
                          }
                          p {
                              font-size: 18px;
                              margin-bottom: 20px;
                          }
                      </style>
                  </head>
                  <body>
                      <h1>Welcome to the Salt-installed NGINX Test Page!</h1>
                      <p>This page confirms that NGINX has been successfully installed using Salt.</p>
                  </body>
                  </html>
          
     testi.com ngnx-conf tiedosto:
              
                      server {
                          listen 80;  
                          server_name localhost testi.com;
                      
                          root /home/vagrant/nginx/public_html;  
                          index index.html;  
                      
                          location / {
                              try_files $uri $uri/ =404;  
                          }
                      }
                  
          <details>

            
   - `sudo salt webserver state.apply nginx`  asensi nginxän. Testasin kirjautua webadmin koneen työpöydälle webadmin/ User One tunnuksin ja selaimella kohteeseen localhost sekä testi.com
   - !h7-004
   - Tämän jälkeen ongekmat sitten alkoivatkin. webadmin kyllä pystyi muokkaamaan html sivun lähdekoodia, mutta se ei päivittynyt työpöydän selaimelle. `curl localhost`palautti muokatun sivun, mutta selaimen päivitykseen en löytänyt keinoa.
   
8. 

## z) Käyttöympäristö
Tehtävä toteutettiin MacBook Retina 12-inch, koneella jossa, host OS on Ventura 13.6.1 käyttöjärjestelmä Suomen maa-asetuksilla ja suomen kielellä. Koneessa on 1,3GHz kaksiytiminen Intel Core i5 prosessori ja 8Gt 1867 MHz LPDDR3 muistia. Näytönohjain on Intel HD Graphics 615 jossa VRAM 1536 Mt.

Koneeseen asennettu Vagrant versio on 2.4.1.

c - kohdassa käytetyt virtuaalikoneet ovat Linux Bullseye 5.10.0-28-amd64.

[Takaisin ylös](https://github.com/syjaka/Palvelinten-Hallinta-2024/blob/main/h7_Oma_miniprojekti.md#h7-oma-miniprojekti)

---
