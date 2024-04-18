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

### Rules of YAML

- YAML on merkintäkieli, jonka tehtävänä on kääntää sen tietorakenteet Python-muotoon Salt:ia varten

- YAML:ia käyttäessä tulisi tietää muutamia sääntöjä, kuten:
  - Data on jäsennelty avain-arvo pareiksi
  - Parit merkitään kaksoispisteellä ja välilyönnillä. ": " = "avain: arvo"
  - Isoilla ja pienillä kirjaimilla on merkitystä
  - Käytä sisennyksessä välilyöntejä, älä tabulaattoria

### YAML simple structure

- YAML koostuu kolmesta perus elementtityypistä:
  - Skalaarit (scalars) ovat avain: arvo kartoituksia, joissa arvo voi olla numero, merkkijono tai totuusarvomuuttuja
  - Listat (lists) ovat luetteloita, joissa avaimilla voi olla useampia arvoja. Ne merkitään avaimesta seuraavalle riville sisennetyillä tavuviivoilla allekkain
  - Sanastot (dictionaries) ovat kokoelmia avain-arvo kartoituksista ja listoista

### Lists and dictionaries - YAML block structures

###

## a) Hello SLS!

## b) Top

## c) Apache easy mode

## d) SSHouto

## References

Salt Project s.a. Salt overview. https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html

Karvinen 2023: Salt Vagrant - automatically provision one master and two slaves. https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file

Karvinen 2024: Infra as Code 2024. https://terokarvinen.com/2024/configuration-management-2024-spring
