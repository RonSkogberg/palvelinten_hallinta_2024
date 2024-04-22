# H4 Demoni

## x) Lue ja tiivistä

### Infra as Code - Your wishes as a text file (Karvinen 2023)

- Luo uusi hakemisto sijaintiin /srv/salt/ (esim. hello-niminen)

- Luo sinne init.sls tiedosto, jonka sisältö on YAML-muodossa

- Kirjoita init.sls tiedostoon haluamasi Saltstack-konfiguraation. Se voi olla esim. paketinasennus käyttäen "file.managed" tilaa

- Suorita käyttäen ```$ sudo salt '*' state.apply hello``` komentoa. Tämä komento käyttää hello-hakemistossa olevaa init.sls tilaa kaikkiin orja-koneisiin

### top.sls - What Slave Runs What States (Karvinen 2023)

- top.sls tiedoston avulla voidaan määritellä se, että mitä tiloja suoritetaan millekin orjalle

- Luo top.sls tiedosto tuttuun /srv/salt/ hakemistoon

- Kirjoita top.sls tiedostoon haluamasi Saltstack-konfiguraation. Käyttäen sisennyksen jälkeen esimerkiksi '*' lisäystä suoritetaan sen jälkeen listatut tilat (esim. edellisen kohdan hello) kaikille orjille

- Tämän jälkeen sinun ei tarvitse nimetä erikseen eri moduleita suorittaessasi komentoja. Esimerkiksi ```$ sudo salt '*' state.apply``` suorittaa hellon automaattisesti kaikille orjille

### Rules of YAML (Salt Project s.a.)

- YAML on merkintäkieli, jonka tehtävänä on kääntää sen tietorakenteet Python-muotoon Salt:ia varten

- YAML:ia käyttäessä tulisi tietää muutamia sääntöjä, kuten:
  - Data on jäsennelty avain-arvo pareiksi
  - Parit merkitään kaksoispisteellä ja välilyönnillä. ": " = "avain: arvo"
  - Isoilla ja pienillä kirjaimilla on merkitystä
  - Käytä sisennyksessä välilyöntejä, älä tabulaattoria

### YAML simple structure (Salt Project s.a.)

- YAML koostuu kolmesta perus elementtityypistä:
  - Skalaarit (scalars) ovat avain: arvo kartoituksia, joissa arvo voi olla numero, merkkijono tai totuusarvomuuttuja
  - Listat (lists) ovat luetteloita, joissa avaimilla voi olla useampia arvoja. Ne merkitään avaimesta seuraavalle riville sisennetyillä tavuviivoilla allekkain
  - Sanastot (dictionaries) ovat kokoelmia avain-arvo kartoituksista ja listoista

### Lists and dictionaries - YAML block structures (Salt Project s.a.)
- YAML on jaettu lohkoiksi.
- Sisennysten käyttö on tärkeää, sillä se määrittää kontekstin. Tämä tapahtuu yleensä kahdella välilyönnillä
- Listan tai sanaston tyyppinen kokoelma merkitään väliviivalla ja välilyönnillä, esim. ("- ")

## a) Hello SLS! (Karvinen 2024)

Tässä tehtävässä aloitan vaatimattomasti tekemällä Hei maailma -tilan kirjoittamalla sen init.sls tiedostoon. init.sls on Saltin konfiguraatiotiedosto, jonne voimme määritellä orjien hallinnointiin käytettäviä konfiguraatioita. Tehtävän alussa luon Saltin päähakemistoon, uuden hakemiston nimeltään "heippa". Tänne luon init.sls tiedoston, jonka sisälle määrittelen file.managed-tilan, joka luo tiedosto "heipparon" haluamaani kohdekakemistoon. Suorittamalla ```$ sudo salt '*' state.apply heippa``` komennon, tulee init.sls konfiguraatiot käyttöön kaikilla orja-koneilla. Lopuksi vielä toistin komennon varmistaakseni harmonisen tilan.

![1](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/69e2ff38-165f-47bd-bacf-81481177cd60)

## b) Top (Karvinen 2024)

Tässä tehtävänäni on luoda top.sls, jonka avulla määritetään mitä joukkomäärityksiä suoritetaan orjille. Luon top.sls tiedoston Saltin päähakemistoon ja konfiguroin sen sisälle listan, jonka sisällä olevat tilat suoritetaan orjille, kun käytän komentoa ```$ sudo salt '*' state.apply```. Koska aiemmassa tehtävässä loin jo heipparon-tiedoston orjille, ei tämä komento tehnyt mitään muutoksia.

![2](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/8e2c1c90-d4ba-4f23-a0fb-46e049cc59b2)

Huomasin näin jälkikäteen, että tehtävässä pyydettiin luomaan "useita" tiloja, joita tässä ajetaan, mutta jatkoin käyttämällä aiemmassa tehtävässä luomaani "heippaa". Käytännössä eri tiloja pystyy suorittaa luomalla useita eri hakemistoja, joihin konfiguroin eri init.sls tiedostoja, esimerkiksi pkg.installed. Lopuksi listaan kaikki tilat tähän top.sls tiedostoon.

Halusin vielä testata top.sls toimivuuden tekemällä muutoksia "heippa" hakemiston init.sls tiedostoon. Lisäsin konfiguraatiokäskyyn lisäyksen, että heipparon tulee sisältää tekstin "top.sls muutosteksti". Tämän jälkeen tallensin init.sls:än ja suoritin ```$ sudo salt '*' state.apply``` jälleen kerran. Tulostus ilmoitti muutoksien tapahtuneen.

![3](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/0b31a357-15c5-4c42-a365-1ddc460c2f20)

Suoritettuani testit herra-koneellani, kävin vielä orja-koneellani tarkistamassa lisäämäni kommentin syntymisen. "top.sls muutosteksti" oli lisätty heipparon-tiedostoon orja-koneellani, joten testi näyttäisi onnistuneen.

![4](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/c794a66b-b494-4666-994d-870bdedf5897)

![15](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/ac52a4b9-e0e7-4e52-bc8f-b5db13268f6e)

## c) Apache easy mode (Karvinen 2024)

Tässä tehtäväni on asentaa Apache, korvata sen testisivu ja varmistaa demonin käynnistys. Aloitan tehtävän luomalla init.sls-tiedoston /srv/salt/apache hakemistoon herra-koneella. Määrittelen konfiguraatiotiedostoon Apachen asennksen sekä ron.conf-tiedoston sijaintiasetukset sekä symbolisen linkin. 

![6](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/670eeff3-405d-4bf3-9ca0-318032cb8c1d)

![7](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/36c4f509-097b-4abb-8513-f23224d1d8fb)

Yrittäessäni suorittaa apachen asennusta komennolla ````$ sudo salt-call --local --state-output=terse state.apply apache``` kohtasin ongelman: Vain 2/3 tilasta onnistui ja keskimmäinen kohta huusi punaista. 

![8](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/92a6abe7-8c67-4dfa-9261-d6a3d5a3b73f)

Ongelma ei sinänsä ollut suuri, sillä tulostuksesta käy ilmi, että olin unohtanut kopioida ron.conf tiedoston /etc/apache2/sites-available/ -hakemistosta /srv/salt/apache hakemistoon. Ollessani .../sites-available/ hakemistossa suoritin ```$ sudo cp ron.conf /srv/salt/apache/```. Tämä kopioi tiedoston myös apache-hakemistoon ja suorituksen jälkeen 3/3 kohtaa näyttivät vihreätä!

![9](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/a9a6aa06-1f49-411c-b3b5-b5fe86f9a41c)

![15](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/eba0dd02-642b-4e10-864a-518e9bd51630)

Minun tuli vielä muokata init.sls tiedostoa apache-hakemistossa ja lisätä apache2.service lisäys, jotta ohjelma käynnistyy aina, kun muutoksia tapahtuu. Lopuksi suoritin tilan ja kaikki näyttää toimivan hyvin.

![14](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/ee05eb5f-b9b4-4344-b6db-8a49ec99fbf8)

## d) SSHouto (Karvinen 2024)

Tässä tehtävässä minun tulee lisätä uusi portti, jossa SSHd kuuntelee. Aloitin tehtävän muokkaamalla /etc/ssh/sshd_config-tiedostoa, jonne lisäsin portin 22 kaveriksi portin 1234. 

![11](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/832995f0-47d5-43e9-b862-d6c4c44c7fed)

Käynnistettyäni SSH-palvelun uudestaan tarkistin myös ```$ nc -vz localhost ...``` komennolla, että portit ovat auki. Tulostus kertoo, että aukihan ne ovat.

![13](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/bb48c929-f635-4aa2-b963-6c0f295e82f8)

Tässä kohtaa jäin pohtimaan, että mitä muuta minun tulisi tehdä. Olin lisännyt uuden portin ja varmistanut sen aukiolon, mutten aivan hiffannut miten tästä tulisi jatkaa. Pitääpä käydä keskustelua kurssikaverin kanssa siitä, että miten hän on tehtävän kanssa edennyt.

## References

Salt Project s.a.: salt.states.file. https://docs.saltproject.io/en/latest/ref/states/all/salt.states.file.html#salt.states.file.keyvalue

Karvinen 2023: Salt Vagrant - automatically provision one master and two slaves. https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file

Karvinen 2024: Infra as Code 2024. https://terokarvinen.com/2024/configuration-management-2024-spring

Karvinen 2018: Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port. https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh
