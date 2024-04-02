# x) Lue ja tiivistä

## GitHub (Karvinen 2023)
- Tee käyttäjätunnukset GitHubiin
- Luo uusi repository
- Luo uusi tiedosto luomaasi repositoryyn
- Julkaise!

## SALT (Karvinen 2021)
- SALT:illa voit ohjata konettasi paikallisesti
- pkg.installed – varmistaa (tietyn) palvelun olemassa-/poissaolon
- file.managed – varmistaa (tietyn) tiedoston olemassa-/poissaolon
- service.running – varmistaa, että daemonit uudelleenkäynnistyvät, kun asetukset muuttuvat
- user.present – varmistaa (tietyn) käyttäjän olemassa-/poissaolon
- cmd.run – suorittaa (mielivaltaisesti) komentoja koneella/koneilla

## Raportointiohjeet (Karvinen 2006)
- Raportoinnissa kirjataan ylös mitä tehdään ja mikä tärkeintä, mihin tekemiset johtavat
- Erityisesti ongelmatilanteita kohdatessa hyvä raportointi auttaa hahmottamaan tilannetta ja helpottaa ongelmanratkaisua myös tulevaisuudessa
- Toistettavuus: Samalla ohjeella toteutetut työt tulisivat tuottaa saman lopputuloksen. Muista raportoida myös käyttämääsi toimintaympäristöä
- Täsmällisyys: Raportoi täsmällisesti mitä olet tehnyt. Testaa lopputulos sekä kirjaa se raporttiin. Jos tulos ei ole toivottu, analysoi mistä ongelma voisi johtua. Jos vaikuttaa siltä, että ongelma ei ole sinun päässäsi, ilmoita siitä tarvittaessa eteenpäin sille kuuluville tahoille
- Helppolukuisuus: Käytä muotoiluja oikein sekä kirjoita huolellista tekstiä. Muista tarkistaa teksti mahdollisilta kirjoitusvirheiltä
- Lähdeviittaukset: Viittaa lähteisiin akateemisten käytäntöjen mukaisesti, oli kyseessä sitten asiantuntijan opinnäytetyö tai opiskelijakaverin raportti
- Vakiotekstejä: Jos raporteissasi toistuu samat elementit (esim. GNU General Public Licensen käyttö), merkitse se yhtenäisesti raportteihin
- Pahoja mokia: älä sepitä omiasi. Älä myöskään plagioi toisten töitä tai käytä toisten kuvia omissa teoksissasi. Viittaa aina lainattuun sisältöön lähdeviitteillä

# a) Hello Windows/Mac Salt World!
Asensin salt-minionin Windows-koneelleni Palvelinten hallinta -kurssin ensimmäisellä luennollame 26.3.2024 Tero Karvisen ohjaamana. Asennuksen onnistumisen voin todeta Windows PowerShellissä esimerkiksi seuraavalla komennolla: ```get-service salt-minion```

![salt-minion-asennettuna-pienempi](https://github.com/RonSkogberg/palvelinten_hallinta/assets/148875466/c49f76a0-e0f5-466d-8beb-29fca2a45506)

Kuten tulostuksesta voidaan todeta, palvelu nimeltään salt-minion on asennettuna ja sen status on "Running", joten se on myös käynnissä.

# b) Hello Vagrant!
Salt-minionin tavoin asensin myös Vagrantin Windows-koneelleni kurssin ensimmäisellä luennolla. Vagrantin olemassaolon varmistin käyttäen komentoa: ```vagrant --version```

![vagrant-asennettua](https://github.com/RonSkogberg/palvelinten_hallinta/assets/148875466/21b6e471-83b1-4c9c-9536-45f131dae6c9)

Tulostus ilmoittaa Vagrantin version olevan 2.4.1 ja täten varmistaa sen olemassaolon.

# c) Tee Vagrantilla uusi Linux-virtuaalikone.

Ehdin harjoitella Linux-virtuaalikoneiden luontia Vagrantilla luennon aikana, joten seuraava tehtävä ei tuottanut ongelmia. Käyttäen komentoa ```vagrant init debian/bullseye64``` Vagrant luo Vagrantfile-konfiguraatiotiedoston, joka toimii niin sanotusti pohjana tuleville virtuaalikoneille. Edellä mainittu komento tarkentaa vielä, että haluan virtuaalikoneiden käyttävän Debian bullseyen 64-bittistä arkkitehtuuria. Tämän jälkeen varmistin vielä ```ls``` komennolla, että luomani Vagrantfile on luotu työhakemistooni ja siellähän se oli!

![vagrant-asennus](https://github.com/RonSkogberg/palvelinten_hallinta/assets/148875466/10e3cd57-c4af-4747-b627-4f189f52e798)

Tarkistuksen jälkeen suoritan vielä ```vagrant up``` komennon, joka luo uuden virtuaalikoneen käyttäen aiemmin luomani Vagrantfile-konfiguraatiotiedoston asetuksia. Pienen odottelun jälkeen uusi Debian-virtuaalikone oli luotu. 

Tarkistin virtuaalikoneen toiminnan ottamalla siihen SSH-yhteyden käyttäen ```vagrant ssh``` komentoa. SSH-yhteyden luonti näytti onnistuvan, mutta tuplavarmistin olevani Linux-ympäristössä suorittamalla ```$ hostnamectl```, jonka tulostus paljasti virtuaalikoneeni olevan Debian-kone Linux-kernelillä.

![vagrant_testaus](https://github.com/RonSkogberg/palvelinten_hallinta/assets/148875466/e50cb82d-ea30-421d-8189-6e2796ede1f1)

# a) Asenna Salt (salt-minion) Linuxille (uuteen virtuaalikoneeseesi)
Ollessani SSH-yhteydessä luomaani Linux-virtuaalikoneeseeni, halusin tarkistaa oliko Salt jo asennettuna siihen. Tähän käytin komentoa ```$ sudo servie salt-minion status```, jonka jälkeen tulostus ilmoittaa ettei näin ole ("Unit salt.minion.service could not be found."). Valmistelin salt-minionin asennusta käyttäen komentoa ```$ sudo apt-get update```, joka päivittää Linuxin pakettivarastot ajan tasalle, minkä jälkeen asensin salt-minionin virtuaalikoneelleni komennolla: ```$ sudo apt-get install salt-minion```.

![salt-minion-asennus-linuxille](https://github.com/RonSkogberg/palvelinten_hallinta/assets/148875466/4acf3e35-7d57-4749-81f6-22b1bb98848f)

Lopuksi tarkistin vielä salt-minionin olemassaolon ja toimivuuden komennolla ```$ sudo service salt-minion status```, joka kertoo kyseisen palvelun tilan. Tulostus ilmaisee tilan olevan "active (running)", mikä tarkoittaa että salt-minion on asennettu sekä toiminnassa.

![salt-minion-testaus-linux](https://github.com/RonSkogberg/palvelinten_hallinta/assets/148875466/af730561-443c-4fd6-9528-a51eb6e72499)

# b) Viisi tärkeintä
Tässä tehtävässä keskityn viiteen tärkeimpään Saltin tilafunktioon. Käytin tehtävässä Tero Karvisen tekemiä materiaaleja (Karvinen 2021 & Karvinen 2024)

## pkg.installed

![pkg installed](https://github.com/RonSkogberg/palvelinten_hallinta/assets/148875466/572cc55f-4d30-478b-9d69-6fca72911950)

```$ sudo salt-call --local -l info state.single pkg.installed nano```

Tässä annan paikallisen salt-käskyn, joka tarkistaa onko nano-tekstieditorin asennettu, ja kuten kuvasta näkyy, on se jo esiasennettuna, eikä täten latausta tapahdu.
Jos nanoa ei olisi ollut esiasennettuna, olisi tämä käsky ladannut ja asentanut sen.

```$ sudo salt-call --local -l info state.single pkg.removed nano```

Tällä salt-käskyllä olisin voinut poistaa kyseisen nano-tekstieditorin. En kuitenkaan halua tehdä sitä, sillä nano on must-have työkalu tekstipohjaisessa käyttöliittymässä. ;)

## file.managed
![file managed](https://github.com/RonSkogberg/palvelinten_hallinta/assets/148875466/116c79a3-dfc1-4a8c-a0ba-381e7ce52a2a)

```$ sudo salt-call --local -l info state.single file.managed /home/vagrant/kiisu.txt```

Tällä salt-käskyllä pystyn tarkistamaan onko tiedosto (tässä tapauksessa "kiisu.txt") olemassa. Koska kyseistä tiedostoa ei ollut olemassa, loi käsky sellaisen tiedoston. Tällaisten käskyjen jälkeen on aina hyvä tarkistaa lopputulos esimerkiksi ```$ ls -la``` komennolla.

```$ sudo salt-call --local -l info state.single file.absent /home/vagrant/kiisu.txt```

Tällä pystyn poistamaan kyseisen tiedoston, jos se on jo olemassa.

## service.running
![service](https://github.com/RonSkogberg/palvelinten_hallinta/assets/148875466/6d54b372-4a01-42b6-9c5d-d645fa46a6e2)

```$ sudo salt-call --local -l info state.single service.running ssh enable=True```

Tällä salt-käskyllä pystyn tarkistamaan onko esimerkiksi ssh käynnissä. Käynnissähän se on!

```$ sudo salt-call --local -l info state.single service.dead ssh enable=False```

Tällä käskyllä taas saan sen otettua pois päältä.

## user.present
![user](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/4fb12c92-6cb3-49a2-b5a0-50dc38732c27)


```$ sudo salt-call --local -l info state.single user.present karvinen```

Tällä salt-käskyllä pystymme tarkistamaan onko käyttäjää "karvinen" olemassa. Jos sitä ei ole, luo tämä käsky sellaisen. Käyttäjän tarkistus/poisto tapahtuu seuraavalla käskyllä:

```sudo salt-call --local -l info state.single user.absent karvinen```

## cmd.run
![cmd](https://github.com/RonSkogberg/palvelinten_hallinta/assets/148875466/83e146c6-71ab-42ff-8eb7-874045c1d15c)

```$ sudo salt-call --local -l info state.single cmd.run 'apt-get update'```

Tällä salt-käskyllä pystyn suorittamaan esimerkiksi päivityskomentoja mielivaltaisesti.

# c) Idempotentti
Idempontti IT-maailmassa tarkoittaa tilaa, jossa toistettaessa samaa komentoa useita kertoja, ei sen tulokset ensimmäisen kerran jälkeen muutu. Esimerkiksi tehtävässä "Viisi tärkeintä" loin "kiisu.txt" tiedoston käyttäen komentoa:

```$ sudo salt-call --local -l info state.single file.managed /home/vagrant/kiisu.txt```

Jos suoritan saman saman käskyn uudestaan, huomataan, että kyseinen tiedosto on jo olemassa. Täten uutta tiedostoa ei luoda, vaikka ensimmäisen kerran suorittaessa käskyn se loi kyseisen tiedoston. Täten vaikka toistaisimme kyseisen käskyn satoja kertoja, ei sen lopputulos muutu ensimmäisen käskykerran jälkeen.

![potenssi](https://github.com/RonSkogberg/palvelinten_hallinta/assets/148875466/24f52ae3-d52d-4d4e-b0ba-ee6748912c1e)

# d) Tietoa koneesta
Suoritettuani seuraavan komennon, sain paljon hyödyllistä tietoa (virtuaali)koneestani, joista tosin en puolia ymmärtänyt. Sain poimittua sieltä kuitenkin esimerkiksi koneeni prosessoritietoja ja DNS-palvelimen IP-osoitteita:

```$ sudo salt-call --local grains.items``` 

![grains](https://github.com/RonSkogberg/palvelinten_hallinta/assets/148875466/6b077f6d-cf3a-4a6d-b159-7f2542840d21)

Suorittamalla seuraavan komennon, sain vielä tietää virtuaalikoneeni käyttöjärjeslmätietoja:

```$ sudo salt-call --local grains.item osfinger```

![osfinger](https://github.com/RonSkogberg/palvelinten_hallinta/assets/148875466/da8fc606-b43f-43a4-915c-cc569fbfd826)

## References
Karvinen 2006: Raportin kirjoittaminen. https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/

Karvinen 2021: Run Salt Command Locally. https://terokarvinen.com/2021/salt-run-command-locally/

Karvinen 2023: Create a Web Page Using Github. https://terokarvinen.com/2023/create-a-web-page-using-github/

Karvinen 2024: Infra as Code 2024. https://terokarvinen.com/2024/configuration-management-2024-spring/
