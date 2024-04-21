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

## a) Hello SLS!

Tässä tehtävässä aloitan vaatimattomasti tekemällä Hei maailma -tilan kirjoittamalla sen init.sls tiedostoon. init.sls on Saltin konfiguraatiotiedosto, jonne voimme määritellä orjien hallinnointiin käytettäviä konfiguraatioita. Tehtävän alussa luon Saltin päähakemistoon, uuden hakemiston nimeltään "heippa". Tänne luon init.sls tiedoston, jonka sisälle määrittelen file.managed-tilan, joka luo tiedosto "heipparon" haluamaani kohdekakemistoon. Suorittamalla ```$ sudo salt '*' state.apply heippa``` komennon, tulee init.sls konfiguraatiot käyttöön kaikilla orja-koneilla. Lopuksi vielä toistin komennon varmistaakseni harmonisen tilan.

![1](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/69e2ff38-165f-47bd-bacf-81481177cd60)

## b) Top

Tässä tehtävänäni on luoda top.sls, jonka avulla määritetään mitä joukkomäärityksiä suoritetaan orjille. Luon top.sls tiedoston Saltin päähakemistoon ja konfiguroin sen sisälle listan, jonka sisällä olevat tilat suoritetaan orjille, kun käytän komentoa ```$ sudo salt '*' state.apply```. Koska aiemmassa tehtävässä loin jo heipparon-tiedoston orjille, ei tämä komento tehnyt mitään muutoksia.

![2](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/8e2c1c90-d4ba-4f23-a0fb-46e049cc59b2)

Huomasin näin jälkikäteen, että tehtävässä pyydettiin luomaan "useita" tiloja, joita tässä ajetaan, mutta jatkoin käyttämällä aiemmassa tehtävässä luomaani "heippaa". Käytännössä eri tiloja pystyy suorittaa luomalla useita eri hakemistoja, joihin konfiguroin eri init.sls tiedostoja, esimerkiksi pkg.installed. Lopuksi listaan kaikki tilat tähän top.sls tiedostoon.

Halusin vielä testata top.sls toimivuuden tekemällä muutoksia "heippa" hakemiston init.sls tiedostoon. Lisäsin konfiguraatiokäskyyn lisäyksen, että heipparon tulee sisältää tekstin "top.sls muutosteksti". Tämän jälkeen tallensin init.sls:än ja suoritin ```$ sudo salt '*' state.apply``` jälleen kerran. Tulostus ilmoitti muutoksien tapahtuneen.

![3](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/0b31a357-15c5-4c42-a365-1ddc460c2f20)

Suoritettuani testit herra-koneellani, kävin vielä orja-koneellani tarkistamassa lisäämäni kommentin syntymisen. "top.sls muutosteksti" oli lisätty heipparon-tiedostoon orja-koneellani, joten testi näyttäisi onnistuneen.

![4](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/c794a66b-b494-4666-994d-870bdedf5897)

## c) Apache easy mode

![6](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/670eeff3-405d-4bf3-9ca0-318032cb8c1d)

![7](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/36c4f509-097b-4abb-8513-f23224d1d8fb)

![8](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/92a6abe7-8c67-4dfa-9261-d6a3d5a3b73f)


## d) SSHouto

## References

Salt Project s.a.: salt.states.file. https://docs.saltproject.io/en/latest/ref/states/all/salt.states.file.html#salt.states.file.keyvalue

Karvinen 2023: Salt Vagrant - automatically provision one master and two slaves. https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file

Karvinen 2024: Infra as Code 2024. https://terokarvinen.com/2024/configuration-management-2024-spring

Karvinen 2018: Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port. https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh
