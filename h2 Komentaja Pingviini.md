# Tiivistelmä tehtävästä h2 Komentaja Pingviini ja sen kulusta sekä laitetiedot
### Tiivistelmä: Tehtävä oli moniosainen. Tehtävässä tutustuttiin yleisiin komentoihin sekä hakemistoihin Linux ympäristössä. Tämän lisäksi harjoiteltiin asentamaan uusia ohjelmia komentokehotteesta, kokeiltiin grep komentoa ja putkia. Lopuksi tarkasteltiin oman laitteen raudan tietoja.
Tehtävä ei alkanut omalta osaltani suunnitellusti. Ensimmäisen kolmen ohjelman asennus epäonnistui. En ymmärtänyt niihin tarvittavia laajennuksia tai niiden asentamista. Toki kaksi kolmesta olisi mahdollista asentaa `sudo apt-get install` komennolla. Tätä tapaa ei kuitenkaan mainittu Github sivuilla. Yritin siis asentaa ohjelmat Github sivujen suosittelemalla tavalla tässä onnistumatta. Valitsin siis uudet kolme ohjelmaa jotka asensin sujuvasti. 
Hakemistot ja yleisimmät komennot olivat minulle jo jossain määrin tuttuja. Ne eivät aiheuttaneet suurempaa päänvaivaa. Pipes `|` oli hieman tuoreempi tuttavuus. Olin toki törmännyt siihen aiemmin. En kuitenkaan ollut käyttänyt tätä tapaa. 
Raudan analysointi osoittautui haasteelliseksi. Se osio jäi hieman tyngäksi. 
### Laitetiedot: 
- Näytönohjain: Asus GeForce RTX 3070 Ti ROG Strix - OC Edition
- Virtalähde: Corsair 750W SF Series SF750, modulaarinen SFX-virtalähde
- Emolevy: Asus ROG STRIX B550-I GAMING, Mini-ITX -emolevy
- Prosessori: AMD 5800x3D
- RAM: Corsair 32GB (2 x 16GB) Vengeance LPX, DDR4 3600MHz, CL18,
- SSD: Samsung 1TB 980 SSD-levy, M.2 2280, PCIe 3.0 x4, NVMe 1.4, sekä Kingston 1TB A2000 NVMe PCIe SSD-levy, M.2 2280, 2200/2000
- Käyttöjärjestelmä: Edition	Windows 10 Pro Version	22H2
- Hypervisor: Virtualbox Version 7.0.14 r161095 (Qt5.15.2)
- Käyttöärjestelmä virtuaalikoneella: Debian Version 6.1.0-23-amd64
## x) Tiivistelmä Tero Karvisen sivusta [Command line basics revisited](https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited) sekä omat huomiot
Linuxissa on hyödyllistä ja käytännössä välttämätöntä osata käyttää komentokehotteita. Osaa komennoista joutuu käyttämään jatkuvasti, toisia ei niin useasti. 
- Tärkeimpiä ja omalla kohdallani käytetyimpiä ovat hakemistoissa siirtymiseen sekä niiden tarkasteluun tarkoitetut kehotteet kuten `cd` `ls` `pwd`
- Help komennot auttavat usein alkuun komentojen muodostamisessa, esimerkiksi `man ls` tai `wget -h` 
- Linuxin tärkeimmät hakemistot on hyvä osata ulkoa ja ymmärtää hieman hakemistorakennetta. Näitä käsitellään tämän tehtävän kohdassa **C)**. 
- Pakettienhallinta on hyödyllinen työkalu ja yksinkertainen käyttää. Esimerkiksi `sudo apt-get install nethack-console`
- Ongelmia saattaa tulla eri Linuxien välillä. Toiset ohjelmat eivät ole saatavilla suoraan joidenkin Linuxin versioiden paketinhallinnasta.
- Komentojen oppimiseen auttaa ainoastaan niiden käyttäminen
## a) Micro editorin asennus kello 15.43 29.8.2024
### 1. Yritys
Aloitin tehtävän päivittämällä listan saatavilla olevista paketeista komennolla `sudo apt-get update` . Haettuani päivitetyn listan saatavilla olevista paketeista etsin Micro editoria komennolla `apt-cache search Micro` ja näin sen olevan listalla: ![Pasted image 20240829155527](https://github.com/user-attachments/assets/fa8bb36f-b3e4-4aa9-9f42-02f080acbfe7)

Tämän jälkeen katsoin Micro editorin Github repositoriosta asennustavat varmistuakseni siitä että onnistun asennuksessa. Github repositoriossa mainitaan `apt install micro` joten päätin käyttää sitä. (https://github.com/zyedidia/micro).  Suoritettuani komennon `sudo` alkuisena onnistuin asentamaan Micro editorin. Githubissa olevassa ReadMe tiedostossa sanotaan että tämä tapa ei välttämättä asenna uusinta mahdollista versiota. Tarkistin siis version komennolla `micro -version` . Asentamani versio on 2.0.11 mutta Githubin mukaan uusin versio on 2.0.14. Käsittääkseni en siis pysty päivittämään sitä uudempaan sillä 2.0.11 on uusin versio Debianin paketti repositoriossa.
### 2. Yritys kello 16.15
Koska en halua asentaa itselleni vanhentunutta versiota Microsta, päätin käydä Micron Github repositoriossa perehtymässä muihin asennustapoihin. Micron repositoriosta löytyi skripti uusimman version asentamiseen. 
Selailin skriptin läpi jonka jälkeen suoritin sen komennolla `curl https://getmic.ro | bash` . Tämä komento asensi Micron onnistuneesti läpi. Skripti löytyy osoitteesta https://getmic.ro/ ja ohjeet https://github.com/zyedidia/micro/wiki/Installing-Micro . Onnistuneen asennuksen jälkeen tarkistin taas version komennolla `micro -version` . Versio oli sama edelleen sillä unohdin poistaa Micron ennen uutta asennusyritystä. 
Poistin asennuksen komennolla `sudo apt purge micro` . Sain Micron poistettua ja varmistin sen komennolla `apt list --installed` . Suorittaessani skriptiä uudestaan sain seuraavanlaisen virheilmoituksen: 
![Pasted image 20240829164718](https://github.com/user-attachments/assets/2a415cd4-d6bc-4b3f-b4d7-74050e05fba8)

Löysin kuitenkin Micron skriptitiedostosta toisen komennon jota käyttää asennuksessa: `curl https://getmic.ro/r | sudo sh` ja tällä komennolla onnistuin asentamaan version 2.0.14.![Pasted image 20240829165229](https://github.com/user-attachments/assets/cd2308b4-6ba9-44f5-af70-7a47b6d69580)

### Editorin testaus
Asennuksen onnistuttua pääsin vihdoin kokeilemaan itse Microa. Käynnistin Micron komennolla `./micro` ja pääsin seuraavaan näkymään: 
![Pasted image 20240829165506](https://github.com/user-attachments/assets/8d8b8d47-74c3-4167-b572-cfb67717d88c)

Painamalla `CTRL+E` pääsin Micron komentokehoitteeseen ja komennolla `help colors` sain lisätietoa eri värien asettamisesta. Kokeilin erilaisia teemoja Micro editorissa komennolla `set colorscheme ...` :
Ensin twilight:![Pasted image 20240829170028](https://github.com/user-attachments/assets/20fd38a8-ba5c-4f85-a366-3b71310e88bc)

Sen jälkeen bubblegum:
![Pasted image 20240829170050](https://github.com/user-attachments/assets/928fc36f-af0d-46d8-82de-7db13a5b9701)

ja viimeisenä suosikkini railscast:![Pasted image 20240829170207](https://github.com/user-attachments/assets/9223e9a7-63ba-4d6b-b9fe-ffa44087e7e6)

Kuvankaappauksista näkee myös ääkkösten toiminnan. Asennus tehty ja vaikeuksien kautta voittoon kello 17.00.
### Lähteet:
https://github.com/zyedidia/micro/blob/master/runtime/help/help.md
https://github.com/zyedidia/micro/wiki/Installing-Micro
https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited
https://opensource.com/article/18/8/how-install-software-linux-command-line
## b1) Kolme uutta komentoriviohjelmaa sekä niiden testaus(Epäonnistunut yritys, yritän näitä myöhemmin uudestaan kun ehdin perehtyä aiheeseen paremmin.)
### Komentoriviohjelmien valinta kello 17.05
Seuraavana piti valita kolme uutta komentoriviohjelmaa sekä testata niitä. Aloitin siis tiedonhaun millaisia ohjelmia haluaisin kokeilla. Googlasin "Linux CLI tools" ja törmäsin Github repositorioon nimeltä [awesome-cli-apps](https://github.com/agarrharr/awesome-cli-apps) jonka on tehnyt vitaly-zdanevich. Selailtuani listaa läpi päädyin seuraaviin kolmeen:
- [Timetrap](https://github.com/samg/timetrap): Timetrap is a simple command line time tracker written in ruby. It provides an easy to use command line interface for tracking what you spend your time on.
- [Speedtest-cli](https://www.speedtest.net/apps/cli): Measure internet connection performance metrics like download, upload, latency and packet loss natively without relying on a web browser
- [Glances](https://github.com/nicolargo/glances/blob/master/README.rst): **Glances** is an open-source system cross-platform monitoring tool.
### 1. Timetrap kello 17.30
#### 1. Vaihe: Valmistelut
Päätin aloittaa ensin asentamalla Timetrapin koneelleni. Aloitin lukemalla Githubin readme tiedoston. Ensin piti asentaa RubyGems koneelleni. Löysin [GeeksForGeeksin](https://www.geeksforgeeks.org/how-to-install-rubygems-on-linux/) sivulta siihen hyvät ohjeet. Ensimmäisenä piti asentaa Ruby komennolla `sudo apt-install ruby`. Tämän jälkeen piti ladata zip tiedosto [RubyGemsin](https://www.geeksforgeeks.org/how-to-install-rubygems-on-linux/) sivulta ja purkaa se. Suuntasin terminaalin avulla Downloads kansioon mistä kyseinen tiedosto löytyy. Käyttäen seuraavia komentoja: `cd Downloads` , `ls` varmistaakseni tiedoston nimen ja lopuksi `unzip rubygems-3.5.18.zip` jolla purin zip tiedoston. Siirryin purettuun kansioon `cd` komennolla ja asensin komennolla `sudo ruby setup.rb` .
#### 2. Vaihe: Timetrapin asennus
Seuraavan itse Timetrapin asennus komennolla `gem install timetrap`. Komennon ajettuani sain seuraavanlaisen virheen: ![Pasted image 20240829174435](https://github.com/user-attachments/assets/7ae0d793-4dda-4627-880e-a3bb1044a64d)

Virhettä selvitellessä törmäsin seuraavaan keskusteluun Githubissa: https://github.com/samg/timetrap/issues/174 jossa annettiin vinkki ajaa ensin `sudo apt install ruby-dev && sudo apt install libsqlite3-dev` jonka jälkeen asennus onnistui. Silti timetrap ei toiminut. Asennuksen kuvat: ![Pasted image 20240829180155](https://github.com/user-attachments/assets/55d009cd-9322-4503-b29c-581cf754aea9)

#### 3. Vaihe: Testaus
### 2. Glances kello 18.25
#### 1. Vaihe: Valmistelut 
Glances sovelluksen asennukseen tarvitaan pip joten ensin piti asentaa se komennolla `sudo apt-get install python3-pip` . Toivon että tämä toimii sillä haasteita on ollut edellisen kohdan kanssa joten pidin pienen tauon siitä. https://pip.pypa.io/en/stable/installation/
https://docs.python-guide.org/starting/install3/linux/
#### 2. Vaihe: Glances asennus
Aloitin asennuksen `pip install --user glances` komennolla. Sain seuraavan virheilmoituksen: ![Pasted image 20240829183742](https://github.com/user-attachments/assets/01bad2a3-3887-4202-9484-c5062460dd36)

Etsittyäni verkosta tietoa tästä ilmoituksesta vastaani tuli Stack Overflow keskustelu: https://stackoverflow.com/questions/75602063/pip-install-r-requirements-txt-is-failing-this-environment-is-externally-mana. Keskustelussa Julien Palard kertoo tämän olevan varoitus kahden eri paketinhallintasovelluksen tiedostojen sekoittamisesta. Suositeltiin käyttämään venv toimintoa joka on tietynlaisella rakenteella oleva kansio tai virtuaalinen ympäristö. Luin siitä täältä:https://docs.python.org/3/library/venv.html.  Päätin kokeilla tätä reittiä. Yritin luoda tämän mutta sain seuraavanlaisen virheen: ![Pasted image 20240829185310](https://github.com/user-attachments/assets/5aed6c23-0477-4414-9b80-094cba69b5ae)

Joten suoritin ohjeistetun `apt install python3.11-venv` komennon sudona. Tämä ei korjannut ongelmaani ja netistä löydetyt ohjeet eivät auttaneet asiaa. Oli aika luovuttaa jo toista kertaa saman harjoituksen aikana. 
## b2) Kolme uutta komentoriviohjelmaa sekä niiden testaus(2. yritys)
### Komentoriviohjelmien valinta
Edellisen epäonnistuneen yrityksen pohjalta päädyin valitsemaan uudet ohjelmat jotka yritän asentaa laitteelleni. Pienen etsiskelyn päätteeksi päädyin seuraaviin ohjelmiin: 
### 1: Neovim: A work in progress attempt to improve Vim.
#### Asennus kello 21.54:
Neovim löytyy Githubin tietojen mukaan suoraan Debianin paketinhallinnasta. Aloitan siis sudo `apt-get install neovim komennolla.
Tämä onnistuu vaivattomasti ja terminaali ilmoittaa asennuksen onnistuneen. Seuraavaksi kokeilen käynnistää ohjelman komennolla `nvim` ja ohjelma käynnistyy:![Pasted image 20240902215802](https://github.com/user-attachments/assets/ea644616-1071-4eb8-b110-66b20244eca0)

Tämän jälkeen luon tekstitiedoston johon kirjoitan tekstiä. Käytän seuraavia komentoja: `touch nvimt1.txt` luodakseni tiedoston ja `nvim nvimt1.txt ` avatakseni sen Neovim sovelluksessa. ![Pasted image 20240902220211](https://github.com/user-attachments/assets/ee13f9f8-ee53-4e98-8f00-a1e7139b22ed)

Onnistun kirjoittamaan tekstiä ja tämän jälkeen tallentamaan tekstin. Ohjelma siis toimii.
https://github.com/neovim/neovim/blob/master/INSTALL.md
### 2. ncdu: NCurses disk usage, sovellus listaa tiedostot ja niiden koon (22.08)

Ncdu löytyy myös Debianin paketinhallinnasta. Sen avulla pystyy tarkastelemaan levytilaa sekä kuinka paljon tilaa mikäkin vie. Aloitan asennustyön antamalla komennon `sudo apt-get install ncdu` aloittaakseni asennuksen. Asentaminen näyttää terminaalin mukaan päättyneen. Kokeilen käynnistää ohjelman komennolla `ncdu` . Käynnistys onnistuu ja ohjelma listaa kansiot hakemistossa kokojärjestyksessä:![Pasted image 20240902221036](https://github.com/user-attachments/assets/2942cdf5-7d20-4f25-a006-abca254b24b4)

Tiedostolistausta pystyy selaamaan nuolinäppäimillä ja painamalla Enter pääsee valittuun hakemistoon:![Pasted image 20240902221125](https://github.com/user-attachments/assets/d77d3f16-1906-40ab-9ec2-0f36daa75142)

Asennus on onnistunut ja ohjelma toimii kuten kuuluu.
https://www.networkworld.com/article/972132/using-the-linux-ncdu-command-to-view-your-disk-usage.html
### 3. Steam Locomotive: get train in shell (22.14)
Viimeisenä on hupiohjelma joka näyttää terminaalissa liikkuvan junan mikäli kirjoitat vahingossa `sl` komennon `ls` sijaan. Se vaikuttaa hauskalta, ja tiedän tekeväni välillä kyseisen kirjoitusvirheen. Aloitan asennuksen komennolla `sudo apt-get install sl`. Terminaalissa asennus näyttää päättyneen nopeasti joten pääsen heti kokeilemaan ohjelmaa. Ohjelma näyttää toimivan mallikkaasti. Terminaalin läpi matkaa höyryveturi oikealta vasemmalle:![Pasted image 20240902221641](https://github.com/user-attachments/assets/054def4c-3a0d-4a34-82b4-1d2358f42f14)

Kolme ohjelmaa asennettu ongelmitta. Palaan epäonnistuneisiin ohjelmiin myöhemmin. Ne vaativat kuitenkin lisää perehtymistä. 
## c) File System Hierarchy harjoitus (22.20)
Tässä harjoituksessa tarkoituksena on etsiä [Command Line Basics Revisited](https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited) kappaleen "important directories" hakemistot ja näyttää kuvaavat esimerkit tärkeistä kansioista tai tiedostoista. Mikäli kyseessä on tiedosto, on siitä näytettävä esimerkkirivi. Tehtävä tehdään komentokehotetta käyttäen.
#### Root 
Aloitan juurihakemistosta. Siirryn sinne komennolla `cd /`![Pasted image 20240902222239](https://github.com/user-attachments/assets/11d3046a-de6c-49b7-9f65-8f003648a6fb)

Komennolla `ls` listaan tiedostot ja kansiot joita juurihakemistosta löytyy. Juurihakemistossa on paljon tärkeitä kansioita. `/boot` hakemisto esimerkiksi sisältää bootloaderin, kernelin ja siihen liittyvät tiedostot. Siirryn sinne komennolla `/boot` . En kuitenkaan avaa sieltä mitään.![Pasted image 20240902222739](https://github.com/user-attachments/assets/325dac4d-0145-423f-81de-545cc936aa3f)

#### /home/ 
Seuraavana siirryn kotihakemistoon komennolla `cd /home/` . Sieltä löytyy kaikki käyttäjien hakemistot. ![Pasted image 20240902222904](https://github.com/user-attachments/assets/2d8e8280-02f7-4aaf-a66c-5efa46a7f52d)

#### /home/kreatiini
Omaan kotihakemistooni pääsen joko suoraan komennolla `cd /home/kreatiini` tai komennolla `cd kreatiini` sillä olen jo kotihakemistossa joka sisältää oman hakemistoni: ![Pasted image 20240902223105](https://github.com/user-attachments/assets/9a70de93-e3f7-4841-bea0-531d1053dcaa)

Hakemistosta löytyy omat tiedostoni ja kansioni. Näistä mikään ei vaikuta erityisen tärkeältä. 
#### /etc/
Tästä hakemistosta löytyy asetuksia esimerkiksi verkkoasetuksia. Siirryn hakemistoon komennolla `cd /etc/` . Valitsen tästä kansiosta nyt tiedoston "passwd" sillä sieltä löytyy esimerkiksi käyttäjä ID:t, kotihakemistot ja paljon muuta. ![Pasted image 20240902224114](https://github.com/user-attachments/assets/88dd86b5-074a-45bd-b440-ed61d86d7118)

Avaan tiedoston käyttäen Nano-tekstieditoria komennolla `nano passwd` 
![Pasted image 20240902224331](https://github.com/user-attachments/assets/85690be2-c9f1-4483-a15e-b00b7f2ee8ff)

Tiedostosta löytyy paljon muutakin. Tässä kuitenkin pari esimerkkiriviä.
#### /media/
Media hakemisto sisältää ulkoiset mediat kuten USB tai CD mediat. Siirryn sinne komennolla `cd /media/` . ![Pasted image 20240902232527](https://github.com/user-attachments/assets/44892832-38a5-4751-b80f-3db44b7525fd)

Hakemisto on tyhjä kuten listauksesta näkee. Laitteessani ei ole yhdistettynä ulkoisia medioita tällä hetkellä.
#### /var/log/
Viimeisenä var/log/ joka sisältää lokitietoja. Siirryn sinne komennolla `cd /var/log/` . ![Pasted image 20240902232701](https://github.com/user-attachments/assets/19db215b-eb07-4925-a5b7-7d8a7f864eef)

Lokitiedot ovat tärkeitä, etenkin jonkinlaisen virheen selvittämisessä. Tärkeintä on kuitenkin aina lukea README tiedostot mikäli sellainen löytyy: ![Pasted image 20240902232926](https://github.com/user-attachments/assets/feab631e-d381-4897-8c9a-544d031c597f)

Avaan myös dpkg.log tiedoston komennolla `nano dpkg.log` josta näen minkälaisia paketteja on asennettu `dpkg` komennolla. ![Pasted image 20240902233200](https://github.com/user-attachments/assets/3fa6da35-bf9b-49a5-a356-dd4b043282b3)

https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited
## d) The Friendly M: grep-komento (22.45)
Tehtävänä on näyttää 2-3 kuvaavaa esimerkkiä grep-komennon käytöstä. En oikein tiedä mitä etsiä joten luon ensin muutaman tekstitiedoston eri hakemistoihin.
Loin tiedoston omaan kotihakemistooni. Tämän jälkeen siirryin juurihakemistoon. Juurihakemistossa käytin komentoa `grep -r "Tama"` . Näin pystyin hakemaan grepillä merkkijonoa kaikista hakemistoista. Nyt grep näyttää koko reitin kyseiseen tiedostoon ja rivin jossa hakusana on.
![Pasted image 20240902225852](https://github.com/user-attachments/assets/1dc1fbd3-4159-49cc-8204-92dc81ed557c)

Seuraavana kokeilen hakea samaa tiedostoa. Nyt haen kuitenkin `grep -i "tama" greippi.txt` . Ilman `-i` osaa komento ei löytäisi tiedostoani. Tällä lipulla grep ei välitä kirjainten koosta: 
![Pasted image 20240902230304](https://github.com/user-attachments/assets/d51fd6f0-1ac5-4e92-b3ae-b6db0464acd2)


## e) Pipe: esimerkkejä putkien käytöstä (22.54)
Pipes eli `|` avulla eri komentoja pystytään ketjuttamaan. Tästä hyvänä esimerkkinä `ls -l | more` . Näin pystytään listaamaan hakemiston tiedostot rivi kerrallaan ja näyttämään enemmän tietoa kyseisistä tiedostoista. 
![Pasted image 20240902230950](https://github.com/user-attachments/assets/2dc5f703-6263-4a18-b11f-bef60dbf2fdf)

## f) Raudan listaus ja analysointi lshw:n avulla(23.08)
Aloitan asentamalla lshw:n komennolla `sudo apt-get install lshw` jonka jälkeen ajan komennon `sudo lshw -short sanitize` : ![Pasted image 20240902231227](https://github.com/user-attachments/assets/06509194-5a41-49cc-8c5e-087424aa7e49) ![Pasted image 20240902231243](https://github.com/user-attachments/assets/ce8bcf9e-579e-4a5c-a892-014058cf9c4c)


- **bus** luokka: Tämän luokan tehtävänä on toimia prosessorin ja jonkin laitteen välillä. Esimerkiksi tästä listauksesta löytyy VirtualBoxin, USB ja PCI porttien bus ohjaimet.
- Seuraavana **memory** luokka. Memory tarkoittaa muistia joka toimii nopeana tapana tallentaa tietoa prosessorin käsittelyn apuna. Listauksessa näkyy käytettävissä oleva muistin määrä.
- **Processor** tarkoittaa yksinkertaisesti prosessoria. Prosessori käsittelee tietoa nopeasti tekemällä erilaisia loogisia toimia. Omasta koneestani löytyy 8-ytiminen AMD Ryzen.
- **Input** luokasta löytyy eri syöttölaitteet. Esimerkiksi näppäimistö, virtanäppäin tai hiiren integraatio VirtualBoxiin.
- **Disk** kertoo paljonko massamuistia on käytössä ja minkä nimisiä muistilaitteita on yhdistettynä. Omassa laitteessani näyttää olevan 53gb kokonaisuudessaan muistia käytössä.
- **Volume** kohdasta näkee miten massamuisti on jaettu. Tässä tapauksessa 37gb on tavallisessa tiedostokäytössä ja 12gb on swap muistin käytössä. Swap muisti toimii keskusmuistin laajennuksena. 

## Lähteet:
- Tehtävät perustuvat Tero Karvisen Linux Palvelimet kurssin tehtäviin. https://terokarvinen.com/linux-palvelimet/#h2-komentaja-pingviini
- Tero Karvinen, Command Line Basics Revisited: https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited
- [awesome-cli-apps](https://github.com/agarrharr/awesome-cli-apps) 
- [Timetrap](https://github.com/samg/timetrap)
- [Speedtest-cli](https://www.speedtest.net/apps/cli)
- [Glances](https://github.com/nicolargo/glances/blob/master/README.rst)
- https://stackoverflow.com/questions/75602063/pip-install-r-requirements-txt-is-failing-this-environment-is-externally-mana
- https://pip.pypa.io/en/stable/installation/
- https://docs.python-guide.org/starting/install3/linux/
- https://www.networkworld.com/article/972132/using-the-linux-ncdu-command-to-view-your-disk-usage.html
- https://docs.python.org/3/library/venv.html
- https://github.com/neovim/neovim/blob/master/INSTALL.md
- https://www.networkworld.com/article/972132/using-the-linux-ncdu-command-to-view-your-disk-usage.html
- “Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. http://www.gnu.org/licenses/gpl.html”
