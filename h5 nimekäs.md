# h5 Nimekäs
## Tiivistelmä tehtävästä, tehtävänannot ja oman tietokoneen tiedot
Tähän tulee tiivistelmä 
### Tehtävänanto:
a) Kotisivu. Tee vähintään kolmen erillisen weppisivun kotisivu ja kopioi se näkymään palvelimellesi. Jos sinulla on oikea palvelin Internetissä, kannattaa käyttää sitä. Käytä name based virtual hosting tekniikkaa. Sivujen muokkaamisen pitää onnistua ilman pääkäyttäjän oikeuksia, niiden kopioiminen pääkäyttäjänä testisivun paikalle ei käy. Kotisivujen ei tarvitse olla hienoja, mutta niiden tulee olla validia HTML:ää ja linkittää toisiinsa.
b) Alidomain. Tee kaksi uutta alidomainia, jotka osoittava omaan koneeseesi. Esimerkiksi palvelu on example.com -> linuxkurssi.example.com. Tee toinen alidomain A-tietueella ja toinen CNAME-tietueella. Alidomainit ovat tyypillisesti ilmaisia, kun sinulla on päädomain (example.com).
c) Pubkey. Automatisoi kirjautuminen julkisella SSH-avaimella.
d) Tutki jonkin nimen DNS-tietoja 'host' ja 'dig' -komennoilla. Käytä kumpaakin komentoa kaikkiin nimiin ja vertaa tuloksia. Katso man-sivulta, miten komennot toimivat - esimerkiksi miten 'dig' näyttää kaikki kentät. Analysoi tulokset. Etsi tarvittaessa uusia lähteitä haastaviin kohtiin. Sähköpostin todentamiseen liittyvät SPF ja DMARC -tietojen yksityiskohdat on jätetty vapaaehtoiseksi lisätehtäväksi. Tutkittavat nimet:
    - Oma domain-nimesi. Vertaa tuloksia nimen vuokraajan (namecheap.com, name.com...) weppiliittymässä näkyviin asetuksiin.
    - Jonkin pikkuyrityksen, kerhon tai yksittäisen henkilön weppisivut. (Ei kuitenkaan kurssikaverin tällä viikolla vuokrattua nimeä).
    - Jonkin suuren ja kaikkien tunteman palvelun tiedot.
### Tietokoneen tiedot: 
- Näytönohjain: Asus GeForce RTX 3070 Ti ROG Strix - OC Edition
- Virtalähde: Corsair 750W SF Series SF750, modulaarinen SFX-virtalähde
- Emolevy: Asus ROG STRIX B550-I GAMING, Mini-ITX -emolevy
- Prosessori: AMD 5800x3D
- RAM: Corsair 32GB (2 x 16GB) Vengeance LPX, DDR4 3600MHz, CL18,
- SSD: Samsung 1TB 980 SSD-levy, M.2 2280, PCIe 3.0 x4, NVMe 1.4, sekä Kingston 1TB A2000 NVMe PCIe SSD-levy, M.2 2280, 2200/2000
- Käyttöjärjestelmä: Edition	Windows 10 Pro Version	22H2
## a) Kotisivu (Rannekello 1930 21.9.24)
Aloitin kotisivun tekemisen perehtymällä Apachen [dokumentaatioon](https://httpd.apache.org/docs/2.4/). Hyvää muistin virkistystä aiemmista. Yhdistin palvelinkoneeseeni komennolla `ssh kreatiini@ip-osoite` ja syötin salasanan. Tämän jälkeen päivitin koneen `sudo apt-get update` `sudo apt-get upgrade`. Tein uuden hakemiston etusivulleni jota saa muokattua tavallisena käyttäjänä: `mkdir -p /home/kreatiini/publicsites/kreatiini.org/` ja loin index.html sivun `nano index.html`. Loin conf tiedoston `sudoedit /etc/apache2/sites-available/kreatiini.org.conf` : ![image](https://github.com/user-attachments/assets/26fc844e-78fb-4db0-be39-9a058d4edbb6) ja otin defaultin pois, asetin oman päälle ja käynnistin a2 uudestaan: `sudo a2dissite 000-default.conf` `sudo a2ensite kreatiini.org.conf` `systemctl reload apache2`. Tämän jälkeen sain errorin avatessani sivua: ![image](https://github.com/user-attachments/assets/f8454e25-1df6-4621-a293-0e032a1de897) joten aloitin vianmäärityksen. Kääntäessäni edelliset komennot saadakseni takaisin aiemman default sivun se onnistuu hyvin ilman ongelmia. En ilmeisesti pysty korvaamaan default sivua kokonaan uudella tiedostolla onnistuneesti. Jostain syystä siis home puolelta tämä ei onnistu. 
Siirsin kansioni polkuun `/var/www/kreatiini.org/public_html` ja annoin kaikille käyttäjille oikeudet kansioon komennolla `chown -R $USER:$USER /var/www/kreatiini.org/public_html` ja käynnistelin kaiken uudestaan sekä muutin polut näihin. 
Nyt sain etusivuni näkymään: ![image](https://github.com/user-attachments/assets/300deaa3-dc99-4280-97c0-b8e1237f0caa)
Tein toisen sivun samaan `public_html` kansioon jonka nimesin `projektit.html`. Tämän jälkeen laitoin etusivun linkin viittaamaan tähän sivuun ja näin pääsin linkistä seuraavalle sivulle: ![image](https://github.com/user-attachments/assets/96cf8d7d-4763-42a7-8b65-a850b0a96b47)
Viimeisenä loin `testisivu.html` tiedoston ja kopioin projektisivun sisällön komennolla `cp projektit.html testisivu.html`.  Muokkasin taas hieman HTML-koodia ja laitoin linkin kotisivulle. Nyt kaikki toimii kuten pitääkin. En ole varma oliko tämä tehtävän idea. Todennäköisesti ei. 
## Alidomain (Rannekello 0700 22.9.2024)
Tähän tehtävään namecheapin sivuilta löytyi hyvät ohjeet joilla loin nämä subdomainit. 
![image](https://github.com/user-attachments/assets/57e514cd-8743-4b2e-a2f0-9aa1facd3b3c)
![image](https://github.com/user-attachments/assets/986ae7e7-8f1c-47bb-8a83-2a0c1f6377f7)
### Lähteet: https://www.namecheap.com/support/knowledgebase/article.aspx/9776/2237/how-to-create-a-subdomain-for-my-domain/
## Pubkey (Rannekello 0730 22.9.2024)


### Lähteet: Apache dokumentaatio: https://httpd.apache.org/docs/2.4/
https://www.digitalocean.com/community/tutorials/how-to-set-up-apache-virtual-hosts-on-ubuntu-20-04
https://www.w3schools.com/html/html_favicon.asp
