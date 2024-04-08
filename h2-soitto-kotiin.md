# H2 Soitto kotiin

## Lue & tiivistä

### Two Machine Virtual Network With Debian 11 Bullseye and Vagrant
- Päivitä Linuxin asennuspaketit
- Asenna Vagrant ja Virtualbox
- Luo mieleisesi Vagrantfile (määrittelytiedosto, joka luo virtuaalikoneet)
- Testaa luomiesi virtuaalikoneiden yhteyksien toiminta, esim. pingaamalla niitä toisiinsa

### Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux
- Päivitä Linuxin asennuspaketit
- Asenna Salt-master yhdelle virtuaalikoneelle ja ota sen IP-osoite ylös
- Asenna Salt-minion muille virtuaalikoneille ja lisää masterin IP-osoite /etc/salt/minion sijaintiin
- Muista uudelleenkäynnistää salt-minion, jotta muutokset astuvat voimaan
- Hyväksy salt-masterilla orjien avaimet
- testaa master-minion -yhteyksien toiminta

### Hello Salt Infra-as-Code
- Luo .sls päätteinen tiedosto, johon kirjoitat infraa koodina sijaintiin /srv/salt/
- Kyseinen tiedosto sisältää määritelmät, että mitä/missä/minne tehdään
- Suorita
- Testaa tulokset ja varmista idempotenssin synty

## a) Asenna kaksi virtuaalikonetta samaan verkkoon (Karvinen 2021)
Käytin tässä tehtävässä 2.4.2024 opetuskerralla luomaani Vagrantfileä, jonka pohjana toimi Karvisen mallipohja kyseisestä tiedostosta (Karvinen 2021). Vagrantfilen avulla loin kaksi virtuaalikonetta t001 & t002, joihin asesin Saltin herra-orja arkkitehtuurin myöhemmissä tehtävissä. Koska Vagrantfile oli jo olemassa, suoritin pelkän ```vagrant up``` komennon, jonka johdosta koneet luotiin. Tarkistin niiden olemmassaolon vielä Virtualboxista ja siellähän ne olivat!

![1testi](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/52a4f6f7-af89-49b0-9811-dd35f5586b92)

![2](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/601ebc50-d3c3-43ee-b2a4-8ccc7c498c37)

Otin molempiin virtuaalikoneisiin vuorollaan yhteyden ```vagrant ssh``` komennolla ja tarkistin ensitöikseni t001 koneelta että sen ip-osoite oli sama, jonka olin Vagrantfileen määritellyt. t001-virtuaalikone tulee ottamaan Salt-master roolin, joten sen ip-osoitetta tarvitaan myöhemmin. ```$ ip a``` komento hoiti homman kotiin otin t001-koneen ip-osoiteen 192.168.88.101 ylös. Koska t001:n ip-osoite vastasi Vagrantfilen määrityksiä, pystyin myös olettamaan, että t002-koneen ip-osoite on sama kuin määrityksissä. Pingasin t001 koneelta t002 sekä päinvastoin ja lopputulos oli selvä: paketteja ei ollut hävinnyt pingauksien aikana, joten yhteydet molempiin suuntiin toimi täydellisesti! Tässä tehtävässä seurasin Karvisen tekemiä ohjeistuksia (Karvinen 2018a).

![3](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/4326cffd-9208-4dad-830c-3a85f8a92266)

![4](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/82fbf3b9-8cae-4014-b4d4-22f9518726cc)

## b) Asenna Saltin herra-orja arkkitehtuuri toimimaan verkon yli & c) Aja shell-komento orjalla Saltin master-slave yhteyden yli
Nyt kun yhteydet olivat toiminnassa, asensin seuraavaksi Saltin herra-orja arkkitehtuurin koneille. Aloitin asentamisen päivittämällä Linuxin pakettivarastot komennolla ```$ sudo upt-get update```, jonka jälkeen asensin Salt-masterin t001-koneelle komennolla ```$ sudo apt-get -y install salt-master```. Asennuksen jälkeen totesin salt-masterin asennuksen onnistuneen komennolla ```$ systemctl status salt-master```, jonka tulos näytti vihreätä.

![5](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/579e06c8-9825-4bba-b3a3-52538cf37097)

![6](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/5541db0a-d097-476d-b198-7bd6c606c285)

Toistin täysin samat toimenpiteet t002-koneella korvaten asennuskomennon ```$ sudo apt-get -y install salt-minion``` komennolla. Varmistin tälläkin kertaa salt-minionin toimivuuden ja sehän toimi.

![7](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/0c254c6f-506a-4766-94d9-cf6f3ce1c1cc)

![8](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/1c6ddc82-c6f1-468c-ab7f-f2733bab3c3f)

Orjan tulee tietää, missä sen herra on, ja tähän tarvitsemme herrakoneen IP-osoitetta. Muokkasin orjakoneella (t002) ```$ sudoedit /etc/salt/minion``` komennolla /etc/salt -hakemistossa olevaa minion-tiedostoa, jonne lisäsin t001-koneen ip-osoitteen 192.168.88.101 sekä ID-nimen "ron". Lopuksi käynnistin salt-minionin uudestaan komennolla ```$ sudo systemctl restart salt-minion```, jotta päivittämäni asetukset astuvat voimaan.

![12](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/603fd55c-8bd5-43fd-9d12-ee9cfc2399c9)

Minun tuli vielä hyväksyä masterin puolella ron-minionin avain, jotta herra-orja-suhde olisi valmis. ```$ sudo salt-key -A``` komennolla tämä onnistui ja varmistin vielä ```$ sudo salt-key``` komennolla, että ron on hyväksyttyjen avaimien listalla. Lopuksi testasin yksinkertaisella shell-komennolla ```$sudo salt '*' cmd.run 'whoami'```, että saamme orjaan yhteyttä. Orja vastasi kutsuumme, eli kaikki toimii kuten halusimmekin.

![14](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/eb04e830-b2f3-48c0-8553-e1066b755a0b)

## d) Aja useita idempotentteja komentoja master-slave yhteyden yli

Suoritin muutamia idempotentteja komentoja master-slave yhteyden yli, mistä ensimmäisenä esimerkkinä toimii doggo.txt nimisen tiedoston luonti. Tämä onnistui komennolla ```$ sudo salt '*' state.single file.managed name=/tmp/doggo.txt```, joka luo kaikille orjille doggo.txt nimisen tiedoston sijaintiin "/tmp". Kuten kuvassakin esiintyvät testit osoittavat, loi kyseinen komento ensimmäisellä kerralla tiedoston. Kun komennon suoritti vielä toisen kerran, kertoo tulostus tiedoston olemassaolosta eikä täten tee mitään muutoksia tehden tilasta idempotentin.

![Johonkin](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/54389ec9-67b1-49d1-a971-564ed25b476d)

Samantyyppisesti käytin myös pkg.installed komentoa asentaakseni "treen" komennolla ```$ sudo salt '*' state.single pkg.installed tree``` orjakoneille ja totesin asennuksen samoilla testeillä

![19 ja puol](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/383c61bf-97e0-4f77-b2c2-85bbcfe50783)

## e) Kerää teknistä tietoa orjista verkon yli

Yksinkertaisilla grains.item komennoilla sain pyydettyä orjaa ilmoittamaan hänen ipv4-osoitteensa sekä käyttämänsä käyttöjärjestelmän (sekä sen version).

![18](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/649d8cb8-2f57-4573-ad64-c6e5c4a45c18)

## f) Hello, IaC (Karvinen 2018b)

Tein yksinkertaista infraa koodina luoden kiisu.sls tiedoston, johon käytin pohjana Karvisen ohjeistusta Salt stateista (Karvinen 2018b). 

![15](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/80b244dd-784d-4867-bcc0-9765f0e419d1)

Tämän lisäksi loin kiisu.txt tiedoston, johon lisäsin nanolla hieman tekstiä sisään.

![16](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/c203b287-8c17-4905-827d-f17b673d2a93)

Suoritin salt-komennon, joka luo kyseisen kiisu.txt tiedoston orja-koneille samalla sisällöllä höystettynä. Varmistin idempotenssin toistamalla komennon, jolloinka tulostus varmisti tiedoston luonnin ja sen olemassaolon.

![17](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/f69a95f8-482e-4583-90cb-29195bfc7c03)

Lopuksi kävin vielä itse orja-koneella katsomassa hakemiston, johon kiisu.txt tiedosto oli luotu. Tiedosto löytyi kuin löytyikin paikaltaan ja sen sisältö vastasi aiemmin määrittämääni!

![20](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/6bdba7bc-7804-4443-8c1f-3d84049cfd1a)

## References

Karvinen 2018a: Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux. https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/

Karvinen 2018b: Salt States – I Want My Computers Like This. https://terokarvinen.com/2018/salt-states-i-want-my-computers-like-this/

Karvinen 2021: Two Machine Virtual Network With Debian 11 Bullseye and Vagrant. https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/

Karvinen 2024: Infra as Code 2024. https://terokarvinen.com/2024/configuration-management-2024-spring/
