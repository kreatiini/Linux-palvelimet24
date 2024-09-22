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
Aloitin kotisivun tekemisen perehtymällä Apachen[dokumentaatioon](https://httpd.apache.org/docs/2.4/). Hyvää muistin virkistystä aiemmista. Yhdistin palvelinkoneeseeni komennolla `ssh kreatiini@ip-osoite` ja syötin salasanan. Tämän jälkeen päivitin koneen `sudo apt-get update` `sudo apt-get upgrade`. Tein uuden hakemiston etusivulleni jota saa muokattua tavallisena käyttäjänä: `mkdir -p /home/kreatiini/publicsites/kreatiini.org/` ja loin index.html sivun `nano index.html`. Loin conf tiedoston `sudoedit /etc/apache2/sites-available/kreatiini.org.conf` : 
![image](https://github.com/user-attachments/assets/26fc844e-78fb-4db0-be39-9a058d4edbb6) 
Käytin koodina aiemman tehtävän HTML-koodia jota hieman muokkasin.
ja otin defaultin pois, asetin oman päälle ja käynnistin a2 uudestaan: `sudo a2dissite 000-default.conf` `sudo a2ensite kreatiini.org.conf` `systemctl reload apache2`. Tämän jälkeen sain errorin avatessani sivua:
![image](https://github.com/user-attachments/assets/f8454e25-1df6-4621-a293-0e032a1de897) 
joten aloitin vianmäärityksen. Kääntäessäni edelliset komennot saadakseni takaisin aiemman default sivun se onnistuu hyvin ilman ongelmia. En ilmeisesti pysty korvaamaan default sivua kokonaan uudella tiedostolla onnistuneesti. Jostain syystä siis home puolelta tämä ei onnistu. 
Siirsin kansioni polkuun `/var/www/kreatiini.org/public_html` ja annoin kaikille käyttäjille oikeudet kansioon komennolla `chown -R $USER:$USER /var/www/kreatiini.org/public_html` ja käynnistelin kaiken uudestaan sekä muutin polut näihin. 
Nyt sain etusivuni näkymään: 
![image](https://github.com/user-attachments/assets/300deaa3-dc99-4280-97c0-b8e1237f0caa)

Tein toisen sivun samaan `public_html` kansioon jonka nimesin `projektit.html`. Tämän jälkeen laitoin etusivun linkin viittaamaan tähän sivuun ja näin pääsin linkistä seuraavalle sivulle:
![image](https://github.com/user-attachments/assets/96cf8d7d-4763-42a7-8b65-a850b0a96b47)

Viimeisenä loin `testisivu.html` tiedoston ja kopioin projektisivun sisällön komennolla `cp projektit.html testisivu.html`.  Muokkasin taas hieman HTML-koodia ja laitoin linkin kotisivulle. Nyt kaikki toimii kuten pitääkin. En ole varma oliko tämä tehtävän idea. Todennäköisesti ei. 
Lopuksi validoin sivuni HTML validaattorilla joka sanoo koodini olevan validia: 
![image](https://github.com/user-attachments/assets/a460b653-08f8-4b2f-94b2-4fd74e7f8502)

## b) Alidomain (Rannekello 0700 22.9.2024)
Tähän tehtävään namecheapin sivuilta löytyi hyvät ohjeet joilla loin nämä subdomainit. 
![image](https://github.com/user-attachments/assets/57e514cd-8743-4b2e-a2f0-9aa1facd3b3c)
![image](https://github.com/user-attachments/assets/986ae7e7-8f1c-47bb-8a83-2a0c1f6377f7) ja testasin ne:
![image](https://github.com/user-attachments/assets/4c4e9aea-1eef-48d0-b88a-b7d8c9266c4d)
![image](https://github.com/user-attachments/assets/5915aae2-2c2d-4ac9-a2e9-6697ee51547a)

### Lähteet: https://www.namecheap.com/support/knowledgebase/article.aspx/9776/2237/how-to-create-a-subdomain-for-my-domain/
## c) Pubkey (Rannekello 1900 22.9.2024)
Aloitin perehtymällä teoriaan SSH-asioista. Yksinkertaisuudessaan täytyy siis luoda SSH-avainpari, kopioida julkinen avain palvelinkoneelle ja näin omalta koneelta löytyvällä yksityisellä avaimella saadaan yhteys heti. SSH on tuttu jo ennestään joten uskon tämän luonnistuvan helposti. Koneellani on auki kaksi terminaalia, toinen on ssh-yhteydellä yhdistettynä palvelimeeni ja toinen on paikallisen koneen. Aloitan luomalla avainparin **paikallisella** laitteella komennolla `ssh-keygen` . Tallensin avainpari oletussijaintiin `/home/kreatiini/.ssh/` . Tämän jälkeen kopioin julkisen avaimeni palvelimelleni komennolla `ssh-copy-id kreatiini@64.225.64.211`. Tässä kesti hetki ja sain seuraavan herjan: 
![image](https://github.com/user-attachments/assets/643720bd-7c0a-4f69-8998-a2419ee58cf6) 
Huomasin kirjoitusvirheeni ja nyt onnistuin: 
![image](https://github.com/user-attachments/assets/35e99e34-00f9-468c-9ee9-50ca62070b39)
Seuraavana kirjaudun laitteelle ja tarkastan avaimet. Kirjautuminen onnistui ainakin suoraan. Siirryin siitä hakemistoon `~/.ssh` ja komennolla `cat authorized_keys` näin että listalla on ainoastaan julkinen avaimenin. Tehtävä onnistui siis. Nyt pystyn yhdistämään laitteelle. En vielä poista salasanakirjautumista kokonaan pois käytöstä. Haluan yhdistää myös toisella laitteella palvelimelleni joten täytyy ensin lisätä sen avain listaan.   

### Lähteet:
https://www.ssh.com/academy/ssh/keygen
https://docs.digitalocean.com/products/droplets/how-to/connect-with-ssh/
https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server

## d) DNS-tiedot `host` ja `dig` komennoilla. 
Aloitin taas tehtävän perehtymällä näihin komentoihin. Ensin piti asentaa dnsutils komennolla `sudo apt-get install dnsutils`. `dig` komennolla tehdään A-tietue hakuja. `host` komennolla nähdään haettavan domainin ip-osoite. Avaan eri kohtia näistä komennoista tarkemmin kun käyn läpi eri sivujen hakuja. 
  ### a) `host kreatiini.org` ja `dig kreatiini.org`
 ![image](https://github.com/user-attachments/assets/bbad6353-0ad5-48ca-b6d7-fd44587c3cd6)
 Tästä kuvasta näkee tulokset jotka tulee kun haen omaa domainiani näillä komennoilla. Aloitaan `dig` komennosta: Kohdassa **QUESTION SECTION** nähdään      mihin domainiin haku kohdistuu ja minkälainen haku. Tässä tapauksessa kyseessä on kreatiini.org ja A-tietue kysely. **ANSWER SECTION** kohdasta nähdään    että vastauksena tuli kreatiini.org A-tietue IP-osoitteelle 64.225.64.211. Numero 300 tarkoittaa TTL aikaa jonka jälkeen tietue päivittyy. Viimeinen osio kertoo yleistä tietoa kyselystä. Tässä tapauksessa aika oli 16msec, DNS palvelin joka vastasi tähän kyselyyn, milloin komento suoritettiin ja minkäkokoinen vastaus DNS palvelimelta tuli. `any` liitteellä saadaan kaikki kentät näkyviin. Omalla palvelimellani tulos näyttää kuitenkin vain tältä: 
 ![image](https://github.com/user-attachments/assets/717ea5af-7a83-4c12-b455-929e1a8d39ab)
 Ilmeisesti HINFO tarkoittaa hardware infoa ja koodi on RFC8482 eli palvelin ei halua vastata tähän kyselyyn sillä ne rasittavat järjestelmiä. 

 `host` komennon vastaus on yksinkertainen, vastauksena tulee domainin ip-osoite sekä muut tietueet mikäli näitä on. Nämä vastaavat namecheapin mail recordia. `dig` komento näytti ip-osoitteen joka on omalla laitteellani sekä TTL ajan 5min kuten kuuluu. 
 ### b) `dig espoonjudokerho.com any` ja `host espoonjudokerho.com`
 ![image](https://github.com/user-attachments/assets/0db79b56-79f8-4618-b9a7-e8ef312d871d)
 Tästä näemme että espoon judokerhon nimipalvelimet ovat  `ns1.webhotelli.fi` sekä `ns2.webhotelli.fi`. Sivuston IP-osoite on `84.239.152.195`. Omalta sivultani en löytänyt vastaavia nimipalvelin listausta. 
 Host haulla taas espoonjudokerhon posti on ohjattu myös 0 espoonjudokerho.fi sivulle.
 ![image](https://github.com/user-attachments/assets/e30f1e1d-6415-419b-9b3b-40269ee23c96)
 ### c) `dig instagram.com any` ja `host instagram.com`
 ![image](https://github.com/user-attachments/assets/c6bd1bb6-a92f-4da2-b746-2bc5d0394890)
Tästä vastauslistasta näemme instagramin A, A ja AAAA tietueet. Eli A-tietue näyttää ipv4 osoitteen, AAAA-tietue taas IPV6 osoitteen koska sellainen on määritetty. SOA-tietue eli state of authority record. Se sisältää tietoa hallinnollisista asioista joita liittyy tähän alueeseen, etenkin zone transfer - toimintoon liittyen. Sen avulla pystytään siirtämään kyselyitä eri palvelimille joista saa saman vastauksen. 
![image](https://github.com/user-attachments/assets/51b83d6f-618c-48cf-82d4-75acbd17ccfb)
Host kyselyllä saatiin näkyviin IPV4 osoite, IPV6 osoite sekä mitkä palvelimet toimivat MX-tietueina eli huolehtivat sähköpostista tällä tunnuksella. 
 


        

### Lähteet:
https://www.cloudflare.com/learning/dns/dns-records/dns-soa-record/
https://blog.cloudflare.com/rfc8482-saying-goodbye-to-any/
https://datatracker.ietf.org/doc/html/rfc8482
https://www.geeksforgeeks.org/dig-command-in-linux-with-examples/
https://www.geeksforgeeks.org/host-command-in-linux-with-examples/
https://www.digitalocean.com/community/tutorials/how-to-retrieve-dns-information-using-dig
https://phoenixnap.com/kb/linux-dig-command-examples
https://phoenixnap.com/kb/linux-host
## Lähteet: 
Apache dokumentaatio: https://httpd.apache.org/docs/2.4/
https://www.digitalocean.com/community/tutorials/how-to-set-up-apache-virtual-hosts-on-ubuntu-20-04
https://www.w3schools.com/html/html_favicon.asp
https://www.ssh.com/academy/ssh/keygen
https://www.cloudflare.com/learning/dns/dns-records/dns-soa-record/
https://blog.cloudflare.com/rfc8482-saying-goodbye-to-any/
https://datatracker.ietf.org/doc/html/rfc8482
https://www.geeksforgeeks.org/dig-command-in-linux-with-examples/
https://www.geeksforgeeks.org/host-command-in-linux-with-examples/
https://www.digitalocean.com/community/tutorials/how-to-retrieve-dns-information-using-dig
https://phoenixnap.com/kb/linux-dig-command-examples
https://phoenixnap.com/kb/linux-host
