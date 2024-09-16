# h4 Maailma kuulee
## Tiivistelmä tehtävästä ja oman tietokoneen tiedot
Tehtävä oli kohtuu suoraviivainen ja siinä hyödynnettiin aiemmin opittuja taitoja. Tällä kerralla tehtävä tuntui paljon helpommalta kuin aiemmin. Siinä oli myös kääntöpuoli sillä tällä kertaa palvelin oli kaikille saatavilla. Oli siis oltava tarkkana, muuten palvelin voi olla haavoittuva. 
### Tietokoneen tiedot: 
- Näytönohjain: Asus GeForce RTX 3070 Ti ROG Strix - OC Edition
- Virtalähde: Corsair 750W SF Series SF750, modulaarinen SFX-virtalähde
- Emolevy: Asus ROG STRIX B550-I GAMING, Mini-ITX -emolevy
- Prosessori: AMD 5800x3D
- RAM: Corsair 32GB (2 x 16GB) Vengeance LPX, DDR4 3600MHz, CL18,
- SSD: Samsung 1TB 980 SSD-levy, M.2 2280, PCIe 3.0 x4, NVMe 1.4, sekä Kingston 1TB A2000 NVMe PCIe SSD-levy, M.2 2280, 2200/2000
- Käyttöjärjestelmä: Edition	Windows 10 Pro Version	22H2
## x) Lue ja tiivistä:
### a)Pilvipalvelimen vuokraus ja asennus(Lehto 2022)
 - Vuokrauksessa esim. kurssia varten on hyvä muistaa laittaa maksuilmoitukset päälle säästyäkseen turhilta maksuilta.
 - Paketin valinta kannattaa aloittaa pienimmästä sillä sitä voi kasvattaa mikäli tarve kasvaa myöhemmin.
 - Datakeskus kannattaa valita läheltä käyttäjiä
### d) Palvelin suojaan palomuurilla(Lehto 2022)
 - Ensimmäisen yhdistämisen yhteydessä kannattaa päivittää palvelut.
 - Palomuuri asennetaan komennolla `sudo apt-get install ufw`
 - Palomuuriin on tehtävä reiät tarvittaville palveluille esim. ssh ja se on lopuksi käynnistettävä. Esimerkiksi `sudo ufw allow 22/tpc` ja `sudo ufw enable`
### e) Kotisivut palvelimelle(Lehto 2022)
 - Ennen sivujen julkaisua lukitaan juurikäyttäjä
 - Apache2 täytyy asentaa ensin komennolla `sudo apt-get install apache2`
 - Testisivu on helppo korvata putkittamalla komennot echo ja tee
 - Sivulle on mahdollista luoda julkisia hakemistoja
### f) Palvelimen ohjelmien päivitys(Lehto 2022)
 - Hae saatavilla olevat päivitykset `sudo apt-get update`
 - päivitä `sudo apt-get upgrade`
 - Tietoturvapäivitykset `sudo apt-get dist-upgrade`
### Karvinen 2017
 - AINA VAHVAT SALASANAT
 - Yhdistämisen jälkeen käytät ainoan kerran root käyttäjää
 - Tee reikä ssh yhteyttä varten palomuuriin ja kytke se päälle
 - Tee oma käyttäjä ja lisää sudo sekä adm ryhmiin
 - Muista sulkea Root käyttäjä
 - Haavoittuvuuksien hyväksikäyttö työkalujen avulla on helppoa joten muista päivittää järjestelmä
 - Avaa portti myös julkista palvelinta varten esim 80/tcp porttiin
 - Nimipalvelua käyttäessä tee uusi A-tietue ja yhdistä se omaan palvelimeesi
### Lähteet: 
- [Karvinen 2017: First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS](https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/)
- [Susanna Lehto 2022: Teoriasta käytäntöön pilvipalvelimen avulla](https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/) 
## a) Vuokraa oma pilvipalvelin haluamaltasi palveluntarjoajalta (Rannekello 12.21 16.9.2024: 
Tässä tehtävässä tulee vuokrata ensin haluamastasi palvelusta oma virtuaalipalvelin. Olen jo aiemmin aktivoinut Github Education- paketin. Paketin mukana saa myös ilmaisia krediittejä Digital Ocean palveluun joten käytän sitä. Aloitan kirjautumalla Digital Oceaniin tietokoneellani. Seuraavana valitsen kohdan Spin up a Droplet: KUVA1 DROPLET
Pääsen kohtaan "Create Droplets jossa määritän virtuaalipalvelimen sijainnin, resurssit sekä käyttöjärjestelmän. Valitsin seuraavat asetukset: 
- Region: Amsterdam
- Datacenter: Amsterdam, Datacenter 3, AMS3
- OS: Debian 12 x64
- Droplet type: Basic
- Disk type: SSD
- Ram: 1GB /1CPU
- SSD: 25GB
- Transfer: 1000GB
- Backups: No automatic backups
- Authentication Method: Password
- Hostname: jokuvaa
- Kokonaishinta: 6.00$/Month
  ![image](https://github.com/user-attachments/assets/0cb3a667-14b1-4c78-a280-f89055ab6848) ![image](https://github.com/user-attachments/assets/213061f7-8fe2-449f-9e0e-cc724abf45dd) ![K3-Määritykset3](https://github.com/user-attachments/assets/6febc511-186d-4300-b5ce-e27b0caecd30)



Tehtyäni nämä määritykset valitsin alhaalta kohdan "Create Droplet". Virtuaalipalvelimeni käynnistyi rannekellon mukaan kello 12.39 16.9.2024
https://www.digitalocean.com/
## b) Tee alkutoimet omalla virtuaalipalvelimellasi: tulimuuri päälle, root-tunnus kiinni, ohjelmien päivitys(Rannekello 12.44 16.9.2024)
1. Saadakseni yhteyden omaan palvelimeeni tarvitsen sen ip-osoitteen Digital Oceanista. Otan yhteyden palvelimeeni root-käyttäjänä komennolla `ssh root@OMAIP` .
Tässä kohdassa tuli ensimmäinen ongelma: Yhdistäessä sain ilmoituksen "ssh command not found". Tarkoittanee sitä että minun täytyy ensin asentaa ssh itselleni. Ensin päivitän kaiken komennoilla `sudo apt-get update` ja `sudo apt-get upgrade`. Tämän jälkeen etsin oikean paketin komennolla `sudo apt-cache search ssh`. Löydän paketin `openssh-client` joka on haluamani paketti. Asennan sen komennolla `sudo apt-get install openssh-client`. Asennuksen jälkeen yritän yhdistää virtuaalipalvelimeeni uudestaan. Se kysyy haluanko varmasti yhdistää ja tämän jälkeen syötän salasanani. Nyt yhteys on muodostettu ja komentokenttä muuttuu muotoon `root@jokuvaa`: ![image](https://github.com/user-attachments/assets/ecd733b6-22b1-4d2e-9af3-b94d31d0c268) 
 
2. Ensimmäisenä täytyy tehdä palomuuriin reikä SSH yhteyttä varten. SSH käyttää oletuksena porttia 22 joten sallin sen pääsyn palomuurin läpi `ufw allow 22/tcp` ja laitan palomuurin päälle komennolla `ufw enable` . En tarvitse `sudo` etuliitettä sillä olen root-shellissä. Taas kerran kohtaan ongelman "ufw: command not found". Aloitan tarkastelemalla asennettujen ohjelmien listaa komennolla `apt --installed list` . Listalta ei löydy ufw sovellusta joten asennan sen. Etsin ensin oikean paketin `apt-cache search ufw` . Tämän jälkeen asennan sen komennolla `apt-get install ufw`.
    ![image](https://github.com/user-attachments/assets/aab41d32-6276-4199-9cbc-0d63a6075019) ![image](https://github.com/user-attachments/assets/3b53a9d3-f3af-4519-bac7-3761308c27fa). Nyt ufw on asennettuna ja voin aiemmin mainituilla komennoilla sallia portin 22 ja käynnistää palomuurin.
    ![image](https://github.com/user-attachments/assets/25fb1b4c-8c26-40f0-8f04-e272f5454bfe) ja lopuksi komennolla `ufw status` varmistan palomuurin toiminnan ja asettamani säännön:
    ![image](https://github.com/user-attachments/assets/b5f3d9ca-f67b-4fb5-95fc-5f390d1a7989) Hyvältä näyttää joten jatketaan eteenpäin.
3. Sulkeakseni Root-käyttäjän minun täytyy ensin luoda itselleni tavallinen käyttäjä. Aloitan sen komennolla `adduser kreatiini`:![image](https://github.com/user-attachments/assets/78b7b19c-16e2-4126-afba-95f2ed0ed854)
   Lisään käyttäjäni "sudo" ryhmään komennolla `adduser kreatiini sudo`:![image](https://github.com/user-attachments/assets/ca4f4d98-fc3c-4e88-9078-c2af89282b0c) Saan taas jonkinlaisen Locale asetusherjan johon perehdyn tärkeimpien asetusten jälkeen. 
Seuraavana kokeilen toisella terminaalilla **kreatiini** onnistunko yhdistämään uuteen käyttäjääni. Samalla päivitän paketit jotta voin varmistaa sudo komennon toiminnan. ![image](https://github.com/user-attachments/assets/ed6ade65-2e99-4027-ae43-3ec31b76a9f9) Komento näyttää toimivan toivotulla tavalla.
4. Lukitsen Root käyttäjän salasanan komennolla `sudo usermod --lock root` ja poistan root loginin SSH:n kautta `sudoedit /etc/ssh/sshd_config`: ![image](https://github.com/user-attachments/assets/466e0173-772e-42aa-9da1-9cab46540ced)
 ![image](https://github.com/user-attachments/assets/17244da5-1f1d-4471-8976-52e7eedee79b) Muutettuani ssh_config tiedostoa tallennan sen `ctrl+o`, vahvistan painamalla `Enter` ja poistun `ctrl+x`. Käynnistän SSH palvelun uudestaan komennolla `sudo systemctl restart ssh` ja kokeilin myös varmuuden vuoksi `sudo service ssh restart`.
### Lähteet: 
- Karvinen 2017: https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/
- Lehto 2022: https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/
## C) Asenna weppipalvelin omalle virtuaalipalvelimellesi. Korvaa testisivu. Kokeile, että se näkyy julkisesti. Kokeile myös eri koneelta, esim kännykältä(rannekello 13.57 16.9.2024). 
1. Asennan Apache2 ohjelman virtuaalipalvelimelleni komennolla `sudo apt-get -y install apache2`. Onnistuneen asennuksen jälkeen teen palomuuriin reiän palvelimelle komennolla `sudo ufw allow 80/tcp` . Tämän jälkeen käynnistin apachen komennolla `sudo service apache2 start ` ja katsoin sen tilan komennolla `sudo systemctl status apache2`. ![image](https://github.com/user-attachments/assets/ea0a0d20-c57a-4888-abfb-b0538462fac2) Apachen testisivu näkyy myös windows selaimella hakemalla virtuaalipalvelimeni osoitetta,  joten se toimii. Seuraavana korvaan testisivun omalla sivulla.
2. Aloitin korvaamalla testisivun komennolla `echo "Toimiiko tää?" | sudo tee /var/www/html/index.html` ja käynnistin apachen uudestaan komennolla `sudo service apache2 restart`. Muutaman kirjoitusvirheen jälkeen sain komennon ajettua onnistuneesti ja testisivu vaihtui mutta ääkköset eivät toimineet toivotusti: ![image](https://github.com/user-attachments/assets/c79c7e86-6014-4b6d-b149-b3a5694d4871) Sivu kuitenkin toimii ja sain yhteyden siihen myös puhelimellani.
3. Lopuksi katkaisin yhteyden komennolla exit
### Lähteet: 
- Karvinen 2017: https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/
- Lehto 2022: https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/
## Locale error
Aloin hakemaan netistä tietoa Locale erroriin jonka sain käynnistäessäni palvelinta. Debianin dokumentaation mukaan ssh yhteyttä käytettäessä suositellaan "None" oletukseksi. Ensin mietin mikä on järkevintä ylipäätään palvelinta pyöritettäessä muualla? Onko järkevää pakottaa palvelimen aika omaan sijaintiin vai laitteen sijaintiin. Yritin hakea erilaisilla hakusanoilla tietoa siitä mutta en löytänyt järkevää vastausta. `locale -a` komennolla näin käytettävissä olevat locale paketit: ![image](https://github.com/user-attachments/assets/1d7a5250-9734-499d-b4b1-73c8f46e9dd6) 
Listasta ei löytynyt suomenkielen pakettia joten ryhdyin asennustöihin.

Yritin ensin ohjeiden mukaan `sudo dpkg-reconfigure locales` komentoa mutta valitessani uutta ohjelma sulkeutui ja sama error ilmestyi näytölle. ![image](https://github.com/user-attachments/assets/0fd1260c-e58c-4d35-86c6-f6c42da9c7ae)
Järjestelmään asennetut localet olivat : ![image](https://github.com/user-attachments/assets/d45d6403-f638-4fa2-87c4-8a9a0bd6d46c)
Komennolla `locale` saan kuitenkin suomen ajat ja asetukset. Näitä ei kuitenkaan löydy palvelinkoneestani vaikka oma koneeni yrittää niitä tarjota. 
Löysin artikkelin jonka ratkaisuun olin jo törmännyt aiemmin. Päätin kokeilla tiedoston `/etc/locale.gen` tiedoston muokkaamista. Poistamalla risuaidan oikean locale asetuksen edestä pystyin luomaan locale paketin. Risuaidalla merkatut kohdat ovat siis kommentteja joita ei suoriteta. Sen jälkeen suoritin komennon `sudo locale-gen` luodakseni oikean localen. 
![image](https://github.com/user-attachments/assets/7901203c-97d0-4585-9a12-4e9c5cc4a201) 
Seuraavaksi kokeilen uudestaan komennolla `locale` onko virhe poistunut: 
![image](https://github.com/user-attachments/assets/9cd2fbd1-d38e-4b03-a506-9d11e07afc8d)
Virhe on poistunut joten seuraavana katsotaan vielä kerran `locale -a` : ![image](https://github.com/user-attachments/assets/ad6b62fb-7e57-4980-884d-cb21100430aa)
Oikea locale on asennettuna. 
Kellonaika asian annan vielä olla. 
 - Merkataanko palvelimen aika sen fyysisen sijainnin vai oman sijainnin mukaan?
 - Voinko vaihtaa järjestelmän ajan omaan aikaani ja jättää RTC ajan utc-0 aikaan? 
![image](https://github.com/user-attachments/assets/9ce88794-8baa-4233-a76a-459893a4802d) 
### Lähteet: 
- Debian org: https://wiki.debian.org/Locale
- Kili 2023: [How to Change or Set System Locales in Linux](https://www.tecmint.com/set-system-locales-in-linux/)
- Xiao 2021: [3 Ways to Fix SSH Locale Environment Variable Error](https://www.linuxbabe.com/linux-server/fix-ssh-locale-environment-variable-error)




 
   



