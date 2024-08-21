# x) Raportin kirjoittaminen sekä Free Software Definition
## Raportin kirjoittaminen
- Raporttia kirjoittaessa on tärkeää merkata kaikki vaiheet sekä tehdyt toimenpiteet ylös
- Raporttia kirjoitettaessa on viitattava lähteisiin
- Raportin on oltava selkeästi jäsennelty ja kirjoitusasun täytyy olla siistiä
- Raportissa ei saa väittää tehneensä testejä joita ei ole tehnyt
## Free software Definition
- Vapaus käyttää ohjelmaa miten haluaa ja mihin haluaa
- Vapaus tutustua ohjelman toimintaan sekä tehdä muutoksia siihen. 
- Vapaus jakaa kopioita ohjelmasta 
- Vapaus jakaa kopioita itse muokatusta ohjelmasta
# a) Linuxin asennus virtuaalikoneeseen
## Tietokoneen tiedot: 
| Osa          | Merkki                                                                                                                     |
| ------------ | -------------------------------------------------------------------------------------------------------------------------- |
| Emolevy      | Asus ROG STRIX B550-I GAMING                                                                                               |
| Prosessori   | AMD 5800x3D                                                                                                                |
| RAM          | Corsair 32GB (2 x 16GB) Vengeance LPX, DDR4 3600MHz, CL18,                                                                 |
| Näytönohjain | Asus GeForce RTX 3070 Ti ROG Strix - OC Edition                                                                            |
| SSD          | Samsung 1TB 980 SSD-levy, M.2 2280, PCIe 3.0 x4, NVMe 1.4, sekä Kingston 1TB A2000 NVMe PCIe SSD-levy, M.2 2280, 2200/2000 |
| OS           | Windows 10 Pro Version                                                                                                     |
| Virtalähde   | Corsair 750W SF Series SF750                                                                                               |
### Vaihe1: Asennustiedoston lataaminen
Suunnitelmanani on asentaa Linux Virtualbox ympäristöön. Olen aiemminkin käyttänyt sitä ja tälläkin hetkellä minulla on joitain Linuxin distroja asennettuna. Sen asentamista ei tarvitse siis nyt miettiä. Latasin asennustiedoston tehtävännannosta löytyvän [linkin](http://mirrors.dotsrc.org/debian-cd/12.6.0-live/amd64/iso-hybrid/debian-live-12.6.0-amd64-xfce.iso) kautta. Lataaminen sujui mutkattomasti.
### Vaihe2: VirtualBoxin valmistelu ja asetusten valinta klo 22.24
Käynnistin VirtualBoxin aloitin asennuksen valmistelun. Valitsin ensin VirtualBoxista sinisen tähden jossa lukee "new". Tämän jälkeen painoin alhaalta painikkeesta "expert mode" jolloin pääsin määrittämään asetuksia yhden ikkunan kautta. Valitsin uudelle käyttöjärjestelmälle nimeksi "Debiani" ja tyypiksi Linux. Versioksi valitsin Debian (64-bit). 
**Hardware** kohdasta valitsin Base Memory kohtaan 12000MB ja Processors kohtaan asetin 6 . 
**Hard Disk** kohdassa valitsin "Create a Virtual Hard Disk now" ja tilaa asetin 50GB. Lopuksi painoin kohdasta "Finish"
### Vaihe3: Käynnistysvaihe klo 22.34
Aloitin käynnistysvaiheen valitsemalla "Debiani" koneeni kohdan "Settings". Siellä kohdasta "Controller: IDE" valitsin pienen CD- levy kuvakkeen ja sieltä valitsin Debianin asennustiedoston. 
Valintojen jälkeen painoin "Start" kello 22.37
Ensimmäisenä näytölle ilmestyi Boot menu josta valitsin "Live system(amd64)". Valinnan jälkeen Debian käynnistyi työpöytään.
### Vaihe4: Toimintatarkastus klo 22.40
Päästyäni virtuaalikoneeni työpöytään aloitin kokeilemaan sen toimivuutta ennen asennusta. 
Käynnistin selaimen keskellä näytön alhaalla olevasta pikakuvakkeesta. Kirjoitin Googleen "Foreca Helsinki" ja tarkastin huomisen sään. Tämän jälkeen suljin selaimen varmistuttuani verkon, näppäimistön, näytön sekä hiiren toiminnasta. 
### Vaihe5: Asennusvaihe klo 22.43
Seuraavassa vaiheessa valitsin työpöydältä kuvakkeen "Install Debian". Näytölle ilmestyi ponnahdusikkuna jossa todettiin "Untrusted application launcher". Valitsin tässä kohdassa "Launch anyway". 
- Ensimmäisenä asennusohjelma kysyy kieltä. Kieleksi valitsin "American English". 
- Seuraavana valitaan sijainti ja asetin siihen sijainniksi "Helsinki"
- Kohdassa "Keyboard" valitsin näppäimistöksi "Generic 105-key PC" ja kieleksi "Finnish(Default)" sekä testikentässä kokeilin ääkkösten toiminnan.
-  Kohdassa "Partitions" valitsin "Erase Disk" ja jätin kohdan "Encrypt system" tyhjäksi. "Boot loader location" kohdan jätin koskemattomaksi eli "Master Boot Record of VBOX HARDDISK (/dev/sda)"
- "Users" kohtaan asetin oman nimeni, käyttäjätunnukseni sekä nimesin laitteen. Lopuksi asetin vahvan salasanan sekä jätin kohdan "Log in automatically without asking for the password." tyhjäksi. 
- "Summary" kohdasta katsoin asetusten olevan kuten edellä mainitsin. Lopuksi painoin "Install" painiketta oikeasta alakulmasta kello 22.55.
- Asennus tuli valmiiksi kello 22.58. Valitsin "Restart now" ja painoin "Done" nappulaa.
### Vaihe6: Uudelleenkäynnistys, päivitykset ja palomuurin asettaminen klo 23.03
Uudelleenkäynnistyksen jälkeen syötin käyttäjätunnukseni sekä salasanan. Kone käynnistyi ongelmitta työpöytään.
Käynnistin komentokentän näppäinyhdistelmällä "Ctrl+Alt+T" ja kirjoitin sinne ```sudo apt-get update``` . Komentokentässä näkyi päivityksiä. Tämän jälkeen käytin komentoa ```sudo apt-get -y dist-upgrade``` joka päivitti aivan kaiken. Tämä tehtävä vei aikaa edellistä komentoa kauemmin. Annoin tämän komennon kello 23.08 ja se tuli valmiiksi kello 23.10.
Viimeisenä asensin palomuurin komennolla ```sudo apt-get -y install ufw``` jonka jälkeen käynnistin sen komennolla ```sudo ufw enable```. Komentokenttään tuli ilmoitus "Firewall is active and enabled on system startup". 
# k) Suosikkiohjelmani Linuxilla: Obsidian
## Asennus
Lopuksi asensin testaamisen ilosta Obsidianin. Käytän Obsidiania muistiinpanojen tekemiseen. Sillä ei siis tehdä ihmeellisiä temppuja. Se ei myöskään ole pelkästään Linuxilla toimiva ohjelma jos tässä sellaista haetaan. 
Ensin latasin Obsidianin omilta sivuilta AppImagen. AppImage oli laitettava suoritettavaan muotoon suuntaamalla ensin tiedoston sijaintiin komennolla ```cd Downloads``` ja varmuuden vuoksi tarkastin tiedoston nimen listaamalla hakemiston tiedostot komennolla ```ls```.
Näiden tietojen avulla suoritin komennon ```chmod u+x Obsidian-1.6.7.AppImage```
Ohjelman pystyi nyt käynnistämään komennolla ``Obsidian-1.6.7.AppImage``
## Holvin luonti
Loin oman holvini virtuaalikoneella Obsidianiin vaikka en sitä tule käyttämään. 
![[Pasted image 20240821232927.png]] 
Valitsin kohdan "Create" ja nimesin holvini nimellä "Testi". Valitsin tiedostosijainniksi /home/kreatiini/Desktop. 
Luotuani holvin tein kaksi toisiinsa liittyvää uutta sivua. Linkitin ne toisiinsa näyttääkseni kuinka Obsidian toimii. Myös tämä raportti on kirjoitettu Obsidianissa.
![[Pasted image 20240821233346.png]]
# Lähteet
- Tehtävänannot ja kurssi https://terokarvinen.com/linux-palvelimet/#laksyt
- Install Debian on Virtualbox - Updated 2023 https://terokarvinen.com/2021/install-debian-on-virtualbox/#first-login
- Raportin kirjoittaminen https://terokarvinen.com/2006/raportin-kirjoittaminen-4/
- What is Free Software? https://www.gnu.org/philosophy/free-sw.html#four-freedoms
- Installing Obsidian https://help.obsidian.md/Getting+started/Download+and+install+Obsidian
