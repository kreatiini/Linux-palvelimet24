# h6 Sovellettuna

## Tiivistelmä, tehtävänanto ja tietokoneen tietoja
### Tehtävänanto
Olen seuraavan viikon estynyt tekemään tehtäviä. Sain sovittua opettajan kanssa vaihtoehtoisesta tehtävästä. Suoritan Djangon kaksi erilaista asennusta, kehitys- ja tuotantoversiot. Noudatan Tero Karvisen tekemiä ohjeita näissä tehtävissä. Ohjeet ovat luettavissa täältä: https://terokarvinen.com/2022/deploy-django/ sekä toinen osio https://terokarvinen.com/2022/django-instant-crm-tutorial/ . 
### Tiivistelmä tehtävän kulusta
### Tietokoneen tiedot
- Näytönohjain: Asus GeForce RTX 3070 Ti ROG Strix - OC Edition
- Virtalähde: Corsair 750W SF Series SF750, modulaarinen SFX-virtalähde
- Emolevy: Asus ROG STRIX B550-I GAMING, Mini-ITX -emolevy
- Prosessori: AMD 5800x3D
- RAM: Corsair 32GB (2 x 16GB) Vengeance LPX, DDR4 3600MHz, CL18,
- SSD: Samsung 1TB 980 SSD-levy, M.2 2280, PCIe 3.0 x4, NVMe 1.4, sekä Kingston 1TB A2000 NVMe PCIe SSD-levy, M.2 2280, 2200/2000
- Käyttöjärjestelmä: Edition	Windows 10 Pro Version	22H2

## Djangon kehitysversion asennus (Rannekello 22.09 25.9.2024)
Asensin jokin aika sitten Djangon jo toiselle virtuaalikoneelleni. Jätin kuitenkin koulukäyttöön luomani ympäristön koskemattomaksi, joten pääsen aloittamaan puhtaalta pöydältä taas. Aloitin lukemalla hieman ohjeita läpi saadakseni kokonaiskuvan tehtävästä
Aloitin päivittämällä paketit `sudo apt-get update` ja `sudo apt-get upgrade`.
Apache2 minulla olikin jo asennettuna koneelle joten siirryin seuraavaan kohtaan. Siirryin kotihakemistoon ja tein uuden sivun: `cd` `mkdir -p /publicsites/kreatiininc/festari/` `echo "tämä ei ole kultti" | tee publicsites/kreatiininc/festari/index.html` 
![image](https://github.com/user-attachments/assets/90f2f929-2407-475e-90f4-d4f4ad9e1973)


Loin uuden virtualhostin tätä tehtävää varten `sudoedit /etc/apache2/sites-availaible/kreatiininc.conf` ja liitin sinne tarvittavat tiedot. 
![image](https://github.com/user-attachments/assets/5d7187e6-9d69-4109-9caf-4ded61361463)
Seuraavana otin kaikki muut sivuni pois käytöstä komennolla `sudo a2dissite '*'` ja asetin uuden sivustoni käyttöön komennolla `sudo a2ensite kreatiininc.conf`. Lopuksi käynnistin apache2 uudestaan `systemctl reload apache2`
![image](https://github.com/user-attachments/assets/2ba39c38-dab6-4c2e-823a-fc51792a04f1)
Testasin myös konfiguraatiotiedoston komennolla `/sbin/apache2ctl configtest` enkä saanut muutakuin hyväksytyn herjan domain nimestä. Toki olin jo käynnistänyt apachen uudestaan joten `curl` komento olisi riittänyt jo tässä vaiheessa. Nyt teen sen eli `curl http://localhost/festari/`. Nyt alan epäillä olisiko tässä tehtävässä ollut tärkeää nimetä tiedostot samannimisiksi joten taidan muokata tiedostoja hieman. 
![image](https://github.com/user-attachments/assets/33246cf6-d4e2-41ae-8d2d-0340e95dea6d)

Päädyin toistamaan saman vaihtamalla ohjeista poiketen "teroco" tilalle "kreatiininc". Jatketaan eteenpäin. 
Eli ensin asennushommat `sudo apt-get -y install virtualenv` ja tämän jälkeen uusi virtuaaliympäristö `publicwsgi` hakemistoon. `virtualenv -p python3 --system-site-packages env`.
Tämän jälkeen vuorossa Djangon asennus uuteen virtuaaliympäristöön. Ensin ympäristön käynnistys joka näkyy termninaalissa ennen käyttäjää:
`source env/bin/activate`  
![image](https://github.com/user-attachments/assets/f567fd1d-858a-470b-b1d0-3f40f4e257d1)

Requirements.txt joka yleensä on tiedosto täynnä erilaisia riippuvuuksia ohjelmaa varten, nyt vain yksi. `micro requirements.txt` ja sinne kirjoitan `django`. Tallennuksen jälkeen `cat requirements.txt` varmistuakseni oikeinkirjoituksesta. Sitten itse asennus: `pip install -r requirements.txt` ja varmistus `django-admin --version`. ![image](https://github.com/user-attachments/assets/d8e36f0d-4334-43b7-a641-45452680a2fa)
Seuraavassa kohdassa jossa pitäisi luoda projekti en pysty luomaan proejktia tähän hakemistoon sillä samanniminen hakemisto löytyy jo. Loin mielestäni ohjeiden mukaan hakemistot sekä tiedostot Apachelle. Tämän jälkeen käynnistin virtuaaliympäristön sinne. Loogisesti en kuitenkaan pysty aloittamaan samannimistä projektia kansioon jossa on jo hakemisto. Django luo `startproject` komennolla Djangon hakemiston annetulla nimellä. Ohjeissa ei ole mainintaa hakemiston vaihdosta tai olen liian väsynyt. Selaan ohjeita pidemmälle ja huomaan hakemistorakenteen olevan `home/tero/publicwsgi/teroco/teroco/wsgi.py`. Djangon luomaan hakemistoon verrattuna tämä projekti on siis luotu `teroco` hakemiston sisälle eikä `publicwsgi` hakemistoon. Päätän kuitenkin jättää asian hautumaan. Otan lyhyet yöunet ja koitan uudestaan. Eli lopetan nyt **rannekello 23.23 25.9.24** ja palaan asiaan aamulla. 


