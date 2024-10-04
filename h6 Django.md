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

**Rannekello 7.00 26.9.24** Tein herättyäni toisen koulutehtävän alta pois ja jatkoin Djangon parissa. Luin iltasaduksi dokumentaatiota Djangosta. En löytänyt muuta ratkaisua kuin pakottaa projekti lisäämällä komentoon `django-admin startproject kreatiini .` pisteen. 
Seuraavana muokkaan kreatiininc.conf tiedostoa: `sudoedit /etc/apache2/sites-available/kreatiniinc.conf`. Kun sain projektin luotua ja aloin valmistelemaan conf tiedostoa, havaitsin olleeni oikeassa. Muista luoda uusi projekti aiemmin luodun samannimisen hakemiston sisälle vaikka sitä ei erikseen mainita. Minä en luonut mutta tämä toimii ehkä tälläkin rakenteella. ![image](https://github.com/user-attachments/assets/a8cbff22-6526-4f95-9e6f-5f205442c583)

## Django Instant Customer Database Tutorial (Rannekello 0736 26.9.2024)
Edellinen tehtävä ei lähtenyt toimimaan enkä löytänyt verkosta apuja. Aloitan sen alusta tämän tehtävän jälkeen. Loin ensin hakemiston `mkdir -p o/home/kreatiini/crm/` johon teen projektin ja virtuaaliympäristöt. ![image](https://github.com/user-attachments/assets/9737fc84-e4cc-4e77-bd70-3ac0ad425253)

Loin tarvittavat env paketit:
![image](https://github.com/user-attachments/assets/ff3b18bb-823c-4793-ae82-d9ed9d7edcd6)

Aktivoin sen ja varmistin oikean sijainnin: 
![image](https://github.com/user-attachments/assets/3621703a-e8ac-4271-b017-532b369b89a2)

Loin requirements.txt tiedoston ja asensin djangon siitä. VArmistuin Djangon versiosta: 
![image](https://github.com/user-attachments/assets/2e937f55-bcbc-4861-b71c-2d8a9c909a74)

Loin uuden projektin ja käynnistin Djangon testipalvelimen: 
![image](https://github.com/user-attachments/assets/7b572406-5d29-449f-9e17-1d22e0d041fd)

Ja se toimii:
![image](https://github.com/user-attachments/assets/8f565e2d-6fca-4ed7-83b3-c4f6d9099fda)

### Admin interfacen luominen
Päivitin tietokannat `./manage.py makemigrations` ja `./manage.py migrate`. Tämän jälkeen latasin salasanageneraattorin sekä tein käyttäjän itselleni. Suljin vahingossa terminaalin joten jouduin avaamaan uuden tässä kohtaa. Sain kuitenkin käyttäjän luotua ja admin näkymä toimii: 
![image](https://github.com/user-attachments/assets/859e9a46-8be4-4d62-be3c-9b9f6313e3f3)

Tein uuden käyttäjän ja lisäsin ryhmiin staff sekä superuser: ![image](https://github.com/user-attachments/assets/0a39ef46-a56e-441f-8355-14fdcd6b38c9)

Pystyin esimerkiksi lisäämään ryhmiä tällä käyttäjällä: ![image](https://github.com/user-attachments/assets/b90c98e4-2827-40b4-b1c8-fd8fa8eae6fd) 
Suljin taas serverin ja tein uuden kansion: ![image](https://github.com/user-attachments/assets/62e0b50e-8b23-4cef-87c9-512e66d498ed)
Lisäsin crm sovelluksen settings.py tiedoston sovelluksiin: ![image](https://github.com/user-attachments/assets/fca415f6-793c-4bfe-8da4-ac4dc4799b4f)
Tein malleihin uuden asiakasluokan: ![image](https://github.com/user-attachments/assets/a6fa01ef-b1c9-4909-b4b7-8cec5b989ed5)
Ja loin ne:
![image](https://github.com/user-attachments/assets/31be2302-d49b-4a7e-8047-8f3060d49082)

Rekisteröin tietokannan: ![image](https://github.com/user-attachments/assets/6122670e-8c1a-4b0e-8bf3-08f84d41eb09)

Ja se näkyy siellä: ![image](https://github.com/user-attachments/assets/65845e73-d7f4-4dd7-adc8-80eae21d1fbb)

![image](https://github.com/user-attachments/assets/ef1d2268-cddf-4a19-a92e-65232bbc7070)

Muutetaan nimet näkyviin muutamalla crm/models.py tiedostoa: ![image](https://github.com/user-attachments/assets/a7560559-3f4d-472d-8716-8c6e746c0c9e)

![image](https://github.com/user-attachments/assets/0a77c16c-2f44-48ed-a905-631d7faafaa2)

Ja nimet näkyvät ![image](https://github.com/user-attachments/assets/00105f69-73a2-41a0-8477-dc8b5bb629e3)

Tehtävä tehty onnistuneesti **rannekello 0814 26.9.24** . Voin palata edelliseen tehtävään.

## Django yritys 2 (Rannekello 0818 26.9.2024)
Eilisen sekoilun jälkeen uusi yritys. Toivottavasti ehdin tehdä tämän ennen lähtöä. Apache2 on asennettuna, poistan eilen luomani kansiot ja aloitan puhtaalta pöydältä. Luon uudet tiedostot: `mkdir -p publicwsgi/kreatiininc/static` . Asetan uuden tekstin `echo "Tämä ei ole kultti" | tee publicwsgi/kreatiininc/static/index.html` Poistan apache sivut käytöstä `sudo a2dissite '*'`. Muokkaan aiemmin tekemääni kreatiininc.conf tiedostoa: `sudoedit /etc/apache2/sites-available/kreatiininc.conf`.
![image](https://github.com/user-attachments/assets/f8901aee-6bce-45e6-8cb3-cd970b5b0d8f)
![image](https://github.com/user-attachments/assets/671c1936-0635-46ce-b75c-90cb1c60605a)
Uuden sivun käyttöönotto `sudo a2ensite kreatiininc.conf` ja käynnistys uudestaan `sudo systemctl reload apache2`. Ja homma toimii curlilla: 
![image](https://github.com/user-attachments/assets/797c8ea5-e793-44ae-91c5-5ffaeea78768)

Siirryn `publicwsgi/` hakemistoon ja luon uuden hakemiston virtualenviä varten: 
![image](https://github.com/user-attachments/assets/ee4e7c83-e7a3-4278-a656-c0412318817c)
Käynnistän virtuaaliympäristön ja varmistan että pip on oikeassa paikassa ` source env/bin/activate` sekä ` which pip`:
![image](https://github.com/user-attachments/assets/8a4ec18b-2ee9-4e9e-9de7-94ee3387c6ee)
Tämän jälkeen requirements.txt tiedoston luominen, laitan sinne sanan "django" ja varmistan catilla ennen asennusta: 
![image](https://github.com/user-attachments/assets/0f64d3c7-e11b-4b33-9f2f-8eff3dae3c20)

Seuraavana asennus `pip install -r requirements.txt` ja testi `django-admin --version` .
![image](https://github.com/user-attachments/assets/d8984b31-5e53-4fe0-aecf-b5f306b04d78)

Tällä kertaa koitan luoda projektini kreatiininc kansion sisään sillä pakottamalla sen vanhaan kansioon en onnistunut tehtävässä. 

Nyt muokkaan kreatiinin.conf tiedostoa `sudoedit /etc/apache2/sites-available/kreatiininc.conf`. Mielestäni polut ovat oikein, käyn ne kuitenkin vielä kerran läpi. 
![image](https://github.com/user-attachments/assets/98a541b0-a8b0-4ba4-b41e-8bf8972643df)
Eli tein ehkä kuitenkin ensimmäisellä kerralla oikein, toki se ei toiminut suoraan joten epäilen sitäkin. Nyt kokeilen kuitenkin muuttaa polkua .conf tiedostossa jos se toimisi silti tällä kertaa. Pystyn kuitenkin siirtämään  `static` hakemistoa tarvittaessa, muistan vain muuttaa sen .conf tiedostoon myös. Kokeilin nyt muuttaa polut: 
![image](https://github.com/user-attachments/assets/bb5b5cd1-8acf-4147-9221-a6a6fb4da92b)

WSGI moduulin asensin jo eilen joten nyt tarkistan .conf tiedoston ja käynnistän apachen uudestaan: 
![image](https://github.com/user-attachments/assets/fd7daf86-5462-48fb-82c0-3d4e32ce8a89)

Totuuden hetki curl komennolla, jos ei toimi joudun tekemään tehtävän palattuani. 

... Ja ei tapahdu mitään. `curl` palauttaa vain Default joten joudun perehtymään asiaan paremmin matkani aikana puhelimella. ![image](https://github.com/user-attachments/assets/cd47596d-86a7-4da5-8d4c-f8b20dd22a7e)
Huomasin myös että en ollut vaihtanut python kansion versiota. Se ei kuitenkaan muuttanut mitään. En tiedä vaikuttaako apachen antama DocumentRoot jotenkin asiaan :![image](https://github.com/user-attachments/assets/912c16d6-e710-43e4-8787-5f982ed52199)
Jotenkin luulen että polut ovat väärin/tiedostot ovat väärissä paikoissa. En nyt keksi mikä on syynä. 

Lueskeltuani hetken conf tiedostoa `static` tulee polusta `TDIR` ja sieltä pitäisi löytyä `/static` joten siirrän sen manage.py tiedoston kanssa samaan. Nyt hakemisto näyttää tältä: 
![image](https://github.com/user-attachments/assets/f56aa1e2-3d04-4532-84a0-4cb0f7f8de5d)
Apachen uudelleenkäynnistys ja ei siltikään toimi. 
Muutin myös hakemistorakennettani toisenlaiseksi, ei auttanut. Jokin on säädöissä pielessä en kyllä keksi mitä. Nykyinen hakemistorakenne: ![image](https://github.com/user-attachments/assets/fec33242-3a5e-43d3-a7a0-83ce2f3a4a04) 
![image](https://github.com/user-attachments/assets/516e380b-56b0-4c70-82c7-8d401755e330) ja .conf tiedosto: 

![image](https://github.com/user-attachments/assets/671b0883-34f0-45b5-9ba6-674298dd64d0)´
Tarkastin hakemistojen reitit, conf tiedostot yms monta kertaa. Ainoastaan kreatiininc.conf on päällä. Silt localhost sivu on vain sivu jossa lukee "Default" kuten olen asettanut aiemmin. Ehkä asennukset menneet pieleen ei hajua.

Palaan tehtävään palattuani maanantaina yöllä :) Lopetan nyt **rannekello 1000 25.9.2024** .

## Yritys nro3 Django Production install- **rannekello 0026 1.10.24**
Suoraan lentokentältä kone tulille ja uutta yritystä. Mikäli en onnistu tälläkään kertaa palautan tehtävän ja teen keskiviikkona töiden jälkeen loppuun toisella virtuaalikoneella.
Aloitin nopeilla `apt-get update` ja `apt-get upgrade` komennoilla. Tämän jälkeenm
Localhostissa näkyi Default sivu eli Apache toimii kuten aiemmin. 
Tämän jälkeen tein uuden hakemiston `/julkinen` ja loin sinne hakemistot `/kreatiininc/static/`.
![image](https://github.com/user-attachments/assets/2a92134a-6b67-4420-8372-93fc16acf69f)

Muokkasin kreatiininc conf tiedostoa sudoeditillä:
![image](https://github.com/user-attachments/assets/9ed9943e-c944-497d-89cb-390cb543ad61)

![image](https://github.com/user-attachments/assets/51fd966e-e374-4ef0-b6fc-235943a8bcd6)

Sen jälkeen apachen muut sivut pois, kreatiininc päälle, configtest ja apache uudelleen käyntiin:
![image](https://github.com/user-attachments/assets/993bedb6-b3d9-42ca-b441-57c842773bb4)
![image](https://github.com/user-attachments/assets/ceaf63d2-a0ca-4bff-84e2-4d9a209865f9)
![image](https://github.com/user-attachments/assets/9fe1af65-8fca-47cb-8063-4f855e8528f2)
Ja selaimella localhost/static auki: ![image](https://github.com/user-attachments/assets/ace9364d-4df4-4ca1-9c1b-951f487a4893)

Tämän jälkeen lisäsin virtualenvin `/julkinen` hakemistoon:
![image](https://github.com/user-attachments/assets/ca64f912-eda9-4b51-b07e-2e75d68a6132)
Sitten käynnistin sen, tarkistin tietty oikean pip paikan: ![image](https://github.com/user-attachments/assets/26641ee6-1e5c-4a41-8b18-45f7628f25c4)
Asensin djangon ja tarkistin version:
![image](https://github.com/user-attachments/assets/3bd24726-1642-4391-ad5a-1f9b7995deb8)

Aloitin uuden projektin djangolla: 
![image](https://github.com/user-attachments/assets/b8d8919f-7a6a-41fe-b502-1bec19df410f)
Muokkasin conf tiedostoa [Karvisen](https://terokarvinen.com/2022/deploy-django/) ohjeiden mukaan:
![image](https://github.com/user-attachments/assets/28831608-efec-4869-94cd-fa0878a85fe0)

Ja varmistin että wsgi on asennettuna, tarkistin syntaksin ja käynnistin apachen uudestaan:
![image](https://github.com/user-attachments/assets/9c011d65-c2f8-4a3a-a076-68a26fd78e58)

Ja en taaskaan onnistunut joten päädyin vielä siirtämään kreatiiniproj kansion kreatiininc kansion sisälle. Uusi hakemistorakenne ei auttanut vaikka muutin conf tiedostoani: 
![image](https://github.com/user-attachments/assets/132bbd5f-6a0e-4821-aaab-d0507840fd2b)
Käyn vielä läpi pyydetyt hakemistot ja vertaan niitä omiini:
Ensin Djangon manage.py polku: 
![image](https://github.com/user-attachments/assets/17d02bf6-7346-49b8-a998-c294423e974b)
Seuraavaksi polku wsgi.py:
![image](https://github.com/user-attachments/assets/5ae54be0-80f9-41e2-a146-30e6eac1af18)
Viimeisenä site-packages:
![image](https://github.com/user-attachments/assets/78972c65-3438-4434-bd17-967a8f5345cc)

Mielestäni hakemistot täsmäävät: 
![image](https://github.com/user-attachments/assets/cb92ba62-d576-4e36-9e7a-45db12011377)

Poistin kaikki sivut käytöstä a2dissite, käynnistin uudestaan apachen, laitoin kreatiininc.conf käyttöön ja käynnistin uudestaan. Edelleen localhost sivuna aukeaa default. 

Totean että tehtävä ei onnistunut, yritän ehtiä töissä läppärillä toisella virtuaalikoneella suorittamaan tehtävän kokonaan maaliin huomenna. Herätys kello 6 ja 24h töitä tiedossa. Aika luovuttaa tältä erää. **Rannekello 0122 1.10.2024** 

En ehtinyt tarkastella tehtävää ennen töitä. Katsotaan ennen luentoa huomenna onnistuuko tehtävän tekeminen.¨

[**EDIT klo 1912 2.10.24** Vika oli conf tiedostossa jossa oli virheellistä tekstiä. ]
[**EDIT 4.10.24 Lisätty lähdeluettelo**]
