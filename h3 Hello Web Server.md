# Laitetiedot ja tiivistelmä tehtävästä
## Laitetiedot: 
- Näytönohjain: Asus GeForce RTX 3070 Ti ROG Strix - OC Edition
- Virtalähde: Corsair 750W SF Series SF750, modulaarinen SFX-virtalähde
- Emolevy: Asus ROG STRIX B550-I GAMING, Mini-ITX -emolevy
- Prosessori: AMD 5800x3D
- RAM: Corsair 32GB (2 x 16GB) Vengeance LPX, DDR4 3600MHz, CL18,
- SSD: Samsung 1TB 980 SSD-levy, M.2 2280, PCIe 3.0 x4, NVMe 1.4, sekä Kingston 1TB A2000 NVMe PCIe SSD-levy, M.2 2280, 2200/2000
- Käyttöjärjestelmä: Edition	Windows 10 Pro Version	22H2
- Hypervisor: Virtualbox Version 7.0.14 r161095 (Qt5.15.2)
- Käyttöärjestelmä virtuaalikoneella: Debian Version 6.1.0-23-amd64
## Tehtävän kulku
Sekoilin koko alkutehtävän ja minulle tuli kiire saada tätä tehtävää maaliin halutussa ajassa. Olisi pitänyt keskittyä enemmän alusta asti. Sain kaiken tehtyä silti. 
# x) Tiivistelmä kahdesta weppipalvelimista kertovasta artikkelista
- IP-based hosts käyttää ip osoitetta oikean sivun määrittämiseen
- Tässä versiossa tarvitaan useita ip osoitteita
- Name-Based hosts käyttää hostnamea halutun sivun tunnistamiseen ja näin yhdestä ip osoitteesta voidaan tarjota useita eri sivuja
- Pyynnön saapuessa palvelin valitsee parhaimman osuman mukaisen sivuston ja tarjoaa sen
- Asentamisessa on tärkeää määrittää oikea portti ja ServerName jotta yhteys voidaan muodostaa
## Lähteet:
- The Apache Software Foundation 2023: Apache HTTP Server Version 2.4 Documentation: [Name-based Virtual Host Support](https://httpd.apache.org/docs/2.4/vhosts/name-based.html)
- Karvinen 2018: [Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address](https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/)
# a) Localhost testi (10.9.2024 klo 09.46)
Ensimmäisessä tehtävässä testataan vastaako oma palvelin localhost-osoitetta. Apache oli asennettu jo oppitunnilla joten tämän pitäisi olla suoraviivainen tehtävä. Aloitin tehtävän kokeilemalla selaimella siirtymistä sivulle *localhost*. Vastaan tuli Apachen testisivu: ![Pasted image 20240910094953](https://github.com/user-attachments/assets/7bf347fb-94b8-403f-b20a-04e0624dc3cc)

Tästä voin siis päätellä palvelimeni toimivan.
# b) Lokitietojen etsiminen ja tulkinta (10.9.24 klo 09.51)
Seuraavaksi etsin oman palvelimen lokitiedot ja käyn läpi mitä sieltä löytyy.
Löysin [Codeasite](https://blog.codeasite.com/how-do-i-find-apache-http-server-log-files/) blogista ohjeet lokitietojen hakemiseen. Tiedostot löytyvät `/var/log/apache2` sijainnista. Yrittäessäni siirtyä kansioon sain "Permission denied" vastauksen. ![Pasted image 20240910100013](https://github.com/user-attachments/assets/e2dcc0ba-4247-4a94-8264-02bae6fefc17)

Netistä haettuani löysin [askubuntu](https://askubuntu.com/questions/421684/cant-access-apache-error-logs) kesksutelusta ohjeet oman käyttäjän lisäämisestä adm ryhmään. Ajoin komennon `sudo usermod -aG adm kreatiini`. Tämä ei kuitenkaan poistanut ongelmaa. Päädyin siis nyt avaamaan root-terminaalin. Sen avulla pystyin avaamaan hakemiston: ![Pasted image 20240910100339](https://github.com/user-attachments/assets/29c9eb97-33f9-4b8e-9dca-b7477b0c3880)

Palaan tähän ongelmaan tehtävän jälkeen. Seuraavana kuitenkin listaan tiedoston access.log komennolla `cat access.log` jotta näen tiedostosisällön:![Pasted image 20240910102040](https://github.com/user-attachments/assets/647aa038-416e-4fdd-9a95-99c037875512)

Tässä koko näkymä. Ensimmäiset 4 ovat curl komentoja:
![Pasted image 20240910102040](https://github.com/user-attachments/assets/acbf0fcf-0cd3-4d09-8cd9-e282f886bb56)

Ensimmäinen numerosarja **127.0.0.1** on ip osoite joka tekee yhdistämispyynnön sivulleni.
Toisen viivan kohdalla ilmeisesti lukisi käyttäjänimi mikäli sellainen on. Tässä kuitenkin sen tilalla on vain pelkkä viiva. 
Kolmantena **10/Sep/2024:09:47:21 +0300** kertoo ajan jolloin tämä pyyntö on tehty. 
Neljäs kohta **"GET / HTTP/1.1"** kertoo minkälainen pyyntö on lähetetty, esimerkiksi tässä tapauksessa **GET** pyyntö käyttäen  **HTTP/1.1** protokollaa. **GET** pyynnöllä tehdään tietopyyntöjä tietyistä kohteesta. 
Numero **200** tarkoittaa HTTP vastauksen tilakoodia. Koodi **200** tarkoittaa pyynnön onnistuneen. 
**10956** tarkoittaa minkäkokoinen objekti on palautettu pyynnön lähettäjälle. 
Viimeisenä oleva **"curl/7.88.1"** kertoo millä pyyntö on tehty. Tässä tapauksessa curl työkalulla jonka versio on 7.88.1. Google kertoo uusimman version olevan 8.9.1 joten minun täytyy tehtävän päätteeksi päivittää se. 
![Pasted image 20240910103351](https://github.com/user-attachments/assets/06c90685-79c4-4de1-8607-733759452807)

Viimeiset pyynnöt noudattavat samaa kaavaa kuin edelliset. Nämä pyynnöt on kuitenkin tehty Mozilla Firefox selaimen kautta. Näissä näkyy myös pyyntö kuvaan ja logoon. Ikonin pyynnössä on käynyt joka virhe ja siksi koodi on **404**. 
## Lähteet 
- https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/200
- https://www.sumologic.com/blog/apache-access-log/
# ~~C) Etusivu uusiksi (10.9.24 klo 10.35) epäonnistunut yritys~~
Tässä tehtävässä täytyy luoda uusi name based virtual host joka näkyy suoraan etusivulla. Sitä pitää pystyä muokkaamaan normaalina käyttäjänä. Aloitan seuraamalla Tero Karvisen tekemiä [ohjeita](https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/) . Eli ensin korvaan oletussivun komennolla `echo "Default"|sudo tee /var/www/html/index.html`. ![Pasted image 20240910104408](https://github.com/user-attachments/assets/6e754c95-6074-4de6-be0a-07e64205ad67)

Avaan oman ip-osoitteeni selaimella ja saan seuraavanlaisen näkymän: ![Pasted image 20240910105100](https://github.com/user-attachments/assets/dc99d4c1-1db8-4c4a-9c00-1c45bf464767)

Voin siis todeta että komento toimi. 
## Uusi name based virtual host (klo 10.44) 
Seuraavan teen uuden name based virtual hostin. Syötettyäni komennon `sudoedit /etc/apache2/sites-available/hattu.example.com.conf` Aukeaa seuraava näkymä: ![Pasted image 20240910111005](https://github.com/user-attachments/assets/2d09d4cb-dcc2-4f39-b97e-aac1ec8df330)

Jonne tallennan sivun conf tiedot:![Pasted image 20240910111117](https://github.com/user-attachments/assets/fbcd972a-f2a4-482f-b137-38b17220a6ca)


Tämän jälkeen poistun komennolla **ctrl+q** . Laitan uuden sivun päälle komennolla `sudo a2ensite hattu.example.com` ja käynnistän apachen uudestaan komennolla `sudo systemctl restart apache2`. ![Pasted image 20240910111334](https://github.com/user-attachments/assets/41b479e7-9179-474e-b5da-2ddb54bcedf7)

Huomasin kuitenkin hakemalla **localhost** selaimella saan edelleen Apachen Default sivun. Default tiedoston **/var/www/html/index.html** sisältö on kuitenkin muuttunut onnistuneeksi tekstiin "Default" ja ip-osoitteellani hakemalla saan sivun jossa lukee vain "Default".
![Pasted image 20240910111703](https://github.com/user-attachments/assets/20bb58e6-bb8b-4c4c-9fc1-eb3a9a8a6d8f)

Koitin myös ottaa Apachen 000-Default confin pois päältä. Tämä kuitenkin aiheutti vain forbidden page errorin sekä localhostille että omalle ip osoitteelleni. Muistin kuitenkin sivun päivittämisen, sivu latautui kokoajan välimuistista mutta **CTRL+päivitys** päivitti myös Localhost osoitteen näyttämään oikeaa sivua: ![Pasted image 20240910112509](https://github.com/user-attachments/assets/648f73e4-e7cf-427d-8d41-4bfc392c4e3f)

Edellisessä kohdassa en myöskään lukenut ajatuksella syöttämiäni tietoja kokonaan joten joudun muokkaamaan määritystiedostoa. Muokkasin tiedoston osoittamaan oikeaan paikkaan eli omaan kotihakemistooni: ![Pasted image 20240910113115](https://github.com/user-attachments/assets/390e6928-e8d5-44ec-aced-685b3b45ff62)

## Uuden sivun luominen tavallisena käyttäjänä: 
Nyt luon kotihakemistooni tämän määritellyn sivun: `mkdir -p /home/kreatiini/publicsites/hattu.example.com/` sekä teen uuden index tiedoston: `echo hattu > /home/kreatiini/publicsites/hattu.example.com/index.html` ![Pasted image 20240910113405](https://github.com/user-attachments/assets/6cb83108-9f9f-489e-ab6f-ac1b2c29d979)

#  C) Etusivu uusiksi (10.9.24 klo 12.45) Toinen yritys
Aloitin lukemalla uudestaan materiaalit ajatuksella ja poistamalla kaiken ennen aloitusta. 
Nyt aloitin menemällä nano editoriin ja loin uuden hostin komennolla `EDITOR=nano sudoedit /etc/apache2/sites-available/hattu.example.com.conf` ja tallensin sinne seuraavat tiedot: ![Pasted image 20240910124713](https://github.com/user-attachments/assets/7f0f4e26-f993-44cf-95a9-29400d55dbe7)

Tämän jälkeen käynnistin sivun komennoilla `sudo a2ensite hattu.example.com` sekä ` sudo systemctl restart apache2` 
Jatkoin tästä luomalla uuden hakemiston html sivua varten: `mkdir -p /home/kreatiini/publicsites/hattu.example.com/` ja menin tekemään uuden sivun: ![Pasted image 20240910125026](https://github.com/user-attachments/assets/ee80e83d-c2c1-4572-8595-34072fbb2fe1)

Sivuni ei kuitenkaan toiminut vaan edelleen päädyn samalle Default sivulle kuin aiemmin joten  poistin default conf tiedoston. `sudo rm 000-default.conf` ja käynnistän apachen taas uudestaan. Edelleen päädyn sivulle jossa lukee "Default". Lisäämällä hattu.example.com osoitteen hosts listaan sain vihdoin homman toimimaan: ![Pasted image 20240910130549](https://github.com/user-attachments/assets/2c5e08bf-a144-4fe4-aa80-613113368d70)

Nyt siirryn tekemään sivulle otsikkoa lyhyellä pätkällä HTML koodia jonka otin W3Schoolsin sivulta: ![Pasted image 20240910131036](https://github.com/user-attachments/assets/bd6b7fbb-63f4-466f-a878-64ec8308016f)

# D) HTML sivu 13.15
Saatuani vihdoin sivun toimimaan otin HTML koodinpätkän ja syötin sen validiointia varten [validator](https://validator.w3.org/#validate_by_input) sivulle:![Pasted image 20240910131649](https://github.com/user-attachments/assets/a7e1b683-1d03-44a7-9594-e8495bdf669f)

Tämän perusteella muokkasin koodini näyttämään tältä: ![Pasted image 20240910131912](https://github.com/user-attachments/assets/7fa52ea9-c794-428c-988f-9dce40a44f56)

# f) Curl komento:
Curl komentoa käytetään tiedonahkuun eri protokollilla. Esimerkiksi normaalista URL sivusta kuten tehtävän aikana on tehty. Se näyttää sivun sisällön esim: ![Pasted image 20240910132201](https://github.com/user-attachments/assets/bb419877-7e97-4dee-ae72-08f69b77de8a)

`curl -I` Komennolla saadaan myös HTTP otsakkeet mukaan curl komentoon. esimerkiksi: ![Pasted image 20240910132541](https://github.com/user-attachments/assets/f027aefe-39b6-4343-b0a2-2a28fb3dd8fc)

Tästä käy ilmi käytössä olevan HTTP/1.1 versio protokolla. Koodi 200 tarkoittaa että tietopyyntö on onnistunut. Tässä näkyy myös miltä palvelimelta ne tulevat, milloin sivua on viimeksi muokattu. Accept-Ranges: bytes tarkoittaa että ainoastaan osa tiedosta on saatavilla, ei koko tiedostoa. Content-Length otsake tarkoittaa kuinka iso on lähetettävä osa tiedostoa. Content-Type tarkoittaa minkä muotoista tietoa lähetetään, tässä tapaauksessa HTML tekstiä. 

# Lähteet:
- https://terokarvinen.com/linux-palvelimet/#h3-hello-web-server
- https://validator.w3.org/#validate_by_input
- https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/
- https://httpd.apache.org/docs/2.4/vhosts/name-based.html
- https://www.sumologic.com/blog/apache-access-log/
- https://httpd.apache.org/docs/current/logs.html
- https://blog.codeasite.com/how-do-i-find-apache-http-server-log-files/
- https://superuser.com/questions/646820/apache2-virtual-hosts-not-working
- https://www.w3schools.com/html/html_basic.asp
- 
