# H5 Tekniikoita

## x) Lue ja tiivistä
Tässä tehtävässsä tiivistän Haaga-Helian ammattikorkeakoulun 2019-vuoden opiskelijan, Toni Sepän, kotitehtäväraportin h4. Tässä raportissa hän luo scriptitiedoston, jonka suorittamalla hänen koneestaan tulee automaattisesti salt-orja. Hän myös raportoi myöhemmissä tehtävissä asentavansa Vagrant-virtualisointiohjelman sekä Windows 10 USB-tikun (Seppä, T 2019)

Tehtävässä Seppä:
- Luo "Slave.sh" nimisen tiedoston, jonka sisältöön hän määrittelee seuraavat tekstit (Kommentit ovat minun lisäyksiäni, jossa selitän komennon toiminnan):
```bash
#!/bin/bash # Tämä määrittää oletukseksi bashin.
sudo apt-get update # Tämä päivittää Linuxissa uusimmat pakettivarastot.
sudo apt-get install -y salt-minion # Tämä asentaa koneelle salt-minionin. "-y" Suorittaa hyväksyttää automaattisesti kaikki kohdat, joissa käyttäjältä kysytään yes/no -kysymyksiä.
echo master: 104.248.143.181$’\r’id: orja1 | sudo tee /etc/salt/minion # Tämä lisää Salt-masterin IP-osoitteen ja käyttäjän ID:n tiedostoon /etc/salt/minion, jotta tietokone voi tunnistaa ja yhdistyä oikeaan Salt-masteriin.
sudo systemctl restart salt-minion # Tämä uudelleenkäynnistää salt-minionin
```
- Seppä lisäsi luomaansa tiedostoon suoritusoikeudet ```$ sudo chmod 755 slave.sh``` komennolla
- Hän suoritti luomanssa scripti-tiedoston ja siirtyi master-koneelle hyväksymään luodun orjan ```$ sudo salt-key -A``` komennolla
- Sepän luoma Orja1 hyväksyttiin minioniksi salt-masteriin onnistuneesti
- Seppä aloittaa Vagrantin asennuksen päivittämällä Linuxin pakettivarastot ja asentamalla Vagrantin komennoilla ```$ sudo apt-get update ``` & ```$ sudo apt-get install vagrant```
- Hän myös asentaa samalla tavalla Virtualbox virtualisointialustan
- Hän luo Ubuntu/trusty64-virtuaalikoneen Vagrantilla ja ottaa siihen SSH-yhteyden
- Tehtävän viimeisessä vaiheessa hän loi Windows 10 USB-boottaustikun. Tässä hän käytti graafista käyttöliittymää ja Media Creation Tool-työkalua

## a) Asenna Salt Windowsille (Karvinen, T 2021)

Asensimme Saltin Windowsille Palvelinten hallinta -kurssin ensimmäisellä luennollamme 26.3.2024 Tero Karvisen ohjaamana. Todensin kuitenkin sen asennuksen tätä raporttia varten ```salt-call --local``` komennolla sekä ```salt-call --local info state.single user.present ron``` komennolla. Ensimmäinen näistä ilmaisee Saltin versionumeron, jonka tulosteesta voimme päätellä Saltin olevan asentuneena Windows-koneellani. Jälkimmäinen komento tarkistaa Saltin kautta lokaalisti, että onko käyttäjä "ron" olemassa. Tulostuksesta selviää, että käyttäjä "ron" on olemassa sekä ajan tasalla.

![1](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/18e23db3-5a98-49df-b913-e0f6c119c05c)

## b) Kerää Windows-koneesta tietoa grains.items -toiminnolla

Keräsin Windows-koneestani tietoja erilaisilla grains.items komennoilla. Aloitin yksinkertaisesti selvittämällä tietoja koneeni käyttöjärjestelmästä. Komennolla ```salt-call --local grains.item osmanufacturer osfinger osversion``` etsitään grains.itemeistä tietoa koneessani pyörivästä käyttöjärjestelmästä, sen valmistajasta sekä käyttöjärjestelmän versionumerosta. Tulostus paljastaa koneeni käyttöjärjestelmän takana olevan OS-mafia Microsoft Corporation ja läppärini pellin alla kehrää Windows 10:n versio 10.0.19045.

![osfinger](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/70daae52-caad-4bd2-997d-75bab52a8b9d)

Seuraavaksi lähdin tutkimaan Windows-koneeni prosessoritietoja. Tämä onnistui komennolla ```salt-call --local grains.item cpu_model cpuarch```. Komento ilmoittaa minun käyttäväni AMD64 arkkitehtuurilla pyörivä Intel core i5 kymppigeneraation CPU.

![CPU](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/584ec809-cee0-4f43-95d4-984b99d893f3)

Kolmanneksi tutkin vähän asentamaani Saltin tietoja ```salt-call --local grains.item saltpath saltversion``` komennolla. Ensimmäinen tulostus kertoo Saltin asennuspolun ja jälkimmäinen tulostus sen versionumeron, joka minun tapauksessani on 3007.0.

![salthaku](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/66889239-4da9-4085-b3c2-cb96840ea3a7)

## c) Kokeile Saltin file -toimintoa Windowsilla

Kokeilin Saltin file -toimintoa Windowsilla luomalla uuden tiedoston tekstisisällöllä, testaamalla sen harmonisuuden ja lopuksi toistamalla sen sisällön.

Aloitin luomalla tiedoston ```salt-call --local -l info state.single file.managed C:/Users/Ron/salt-testausta/keppinayttely contents="Tiesitkos, etta tanaan 27.4.2024 on koirien keppinayttely Helsingissa"``` komennolla, joka luo Saltin välityksellä "keppinayttely" nimisen tiedoston sille osoitettuun C:/Users/Ron/salt-testausta -hakemistoon, jonka sisältö vastaa contents-kohdassa määrittelemääni.

![make1](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/ba48a835-20c0-4720-891c-c147b93bf320)

Toistan komennon varmistamalla harmonaalisen, idempotentin, tilan. Tulos näyttää hyvältä, joten eiköhän jatketa.

![make2](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/c1569bfc-7f03-4132-b70e-008177118586)

Lopuksi siirryn kyseiseen C:/Users/Ron/salt-testausta/ -hakemistoon, jossa totean ```ls``` komennolla tiedoston olemassaolon ja ```cat keppinayttely``` komennnolla sen sisältötekstin. Tiedosto oli luotuna ja teksti vastasi aiemmin määrittelemääni!

![make3](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/e8b48c6b-47f0-488a-bf62-cf59c971f53f)

## d) CSI Kerava

Kirjauduttuani t001 Vagrant-virtuaalikoneelleni, siirryin siellä /etc/ -hakemistoon suorittamaan  ```$ find -printf '%T+ %p\n'| sort``` komennon. Käytin tehtävässä apuna 'find' MAN-sivuja (The Linux Documentation Project 2023) sekä Vivek Giten blogitekstiä (nixCraft 2024).

![find1final](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/ac19a089-e1b2-4a17-8762-3dc3b8706abb)

Suoritin kotihakemistossani saman komennon.

![findhomefinal](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/d5430d3f-d34e-4bf7-9613-9cede22ccb6d)

```$ find -printf '%T+ %p\n' | sort``` Komennossa "find" on etsintäkomento, joka suorittaa tiedostohakuja hakemistorakenteista käyttäjän määrittelyjen mukaisesti. ```-printf '%T+ %p\n'``` avulla printattuun hakutulosteeseen sisältyy tiedostojen muokkausaika (%T+) ja sen polku (%p). Lopuksi ```| sort``` lajittelee tulostetut tiedostot niiden muokkausaikojen mukaan.

## References

nixCraft 2024. How to find the oldest file in Linux / Unix file system. https://www.cyberciti.biz/link/how-to-find-the-oldest-file-in-a-directory-tree/

Karvinen, T 2024. Infra as Code. https://terokarvinen.com/2024/configuration-management-2024-spring/

Karvinen, T 2021. Run Salt Command Locally. https://terokarvinen.com/2021/salt-run-command-locally/?fromSearch=run%20salt

Seppä, T. 2019. h4. https://salthomework.wordpress.com/h4/

The Linux Documentation Project 2023. Find(1) - Linux manual page. https://man7.org/linux/man-pages/man1/find.1.html
