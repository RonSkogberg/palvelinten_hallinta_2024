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

## b) Top

## c) Apache easy mode

## d) SSHouto

## References

Karvinen 2018

Karvinen 2023: Salt Vagrant - automatically provision one master and two slaves. https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file

Karvinen 2024: Infra as Code 2024. https://terokarvinen.com/2024/configuration-management-2024-spring

Karvinen 2018: Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port. https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh
