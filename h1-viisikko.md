# x) Lue ja tiivistä

## GitHub (Karvinen 2023)
- Tee käyttäjätunnukset GitHubiin)
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
Asensin salt-minionin Windows-koneelleni Palvelinten hallinta -kurssin ensimmäisellä luennollame 26.3.2024 Tero Karvisen ohjaamana. Asennuksen onnistumisen voin todeta Windows PowerShellissä esimerkiksi seuraavalla komennolla: ``` get-service salt-minion```

![salt-minion-asennettuna-pienempi](https://github.com/RonSkogberg/palvelinten_hallinta/assets/148875466/c49f76a0-e0f5-466d-8beb-29fca2a45506)

Kuten tulostuksesta voidaan todeta, palvelu nimeltään salt-minion on asennettuna ja sen status on "Running", joten se on myös käynnissä.

# b) Hello Vagrant!
Salt-minionin tavoin asensin myös Vagrantin Windows-koneelleni kurssin ensimmäisellä luennolla. Vagrantin olemassaolon varmistin käyttäen komentoa: ``` vagrant --version```

![vagrant-asennettua](https://github.com/RonSkogberg/palvelinten_hallinta/assets/148875466/21b6e471-83b1-4c9c-9536-45f131dae6c9)

Tulostus ilmoittaa Vagrantin version olevan 2.4.1 ja täten varmistaa sen olemassaolon.

# c) Tee Vagrantilla uusi Linux-virtuaalikone.

Ehdin harjoitella Linux-virtuaalikoneiden luontia Vagrantilla luennon aikana, joten seuraava tehtävä ei tuottanut ongelmia. Käyttäen komentoa ```vagrant init debian/bullseye64``` Vagrant luo Vagrantfile-konfiguraatiotiedoston, joka toimii niin sanotusti pohjana tuleville virtuaalikoneille. Edellä mainittu komento tarkentaa vielä, että haluan virtuaalikoneiden käyttävän Debian bullseyen 64-bittistä arkkitehtuuria. Tämän jälkeen varmistin vielä ```ls``` komennolla, että luomani Vagrantfile on luotu työhakemistooni ja siellähän se oli!

![vagrant-asennus](https://github.com/RonSkogberg/palvelinten_hallinta/assets/148875466/10e3cd57-c4af-4747-b627-4f189f52e798)

Tarkistuksen jälkeen suoritan vielä ```vagrant up``` komennon, joka luo uuden virtuaalikoneen käyttäen aiemmin luomani Vagrantfile-konfiguraatiotiedoston asetuksia. Pienen odottelun jälkeen uusi Debian-virtuaalikone oli luotu. 

Tarkistin virtuaalikoneen toiminnan ottamalla siihen SSH-yhteyden käyttäen ```vagrant ssh``` komentoa. SSH-yhteyden luonti näytti onnistuvan, mutta tuplavarmistin olevani Linux-ympäristössä suorittamalla ```$ hostnamectl```, jonka tulostus paljasti virtuaalikoneeni olevan Debian-kone Linux-kernelillä.

![vagrant_testaus](https://github.com/RonSkogberg/palvelinten_hallinta/assets/148875466/e50cb82d-ea30-421d-8189-6e2796ede1f1)

# a) Asenna Salt (salt-minion) Linuxille (uuteen virtuaalikoneeseesi)

# b) Viisi tärkeintä

# c) Idempotentti

# d) Tietoa koneesta

## References
Karvinen 2006: Raportin kirjoittaminen. https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/

Karvinen 2021: Run Salt Command Locally. https://terokarvinen.com/2021/salt-run-command-locally/

Karvinen 2023: Create a Web Page Using Github. https://terokarvinen.com/2023/create-a-web-page-using-github/

Karvinen 2024: Infra as Code 2024. https://terokarvinen.com/2024/configuration-management-2024-spring/
