# h6 Benchmark

## x) Lue ja tiivistä

### Introduction
- Saltilla on mahdollista suorittaa Windowsin paketinhallinnointia, johon kuuluu pakettien:
  -  Asennus
  -  Päivitys
  -  Yleinen hallinta
- Se toimii samankaltaisesti, kuin Linuxin ```yum``` ja ```apt```.
- Paketinmäärittämiseen käytetään YAML/JINJA2-tiedostoja (.sls) ja ne sisältävät pakettien asennukseen tarvittavat tiedot:
  - Ohjelmiston nimi
  - Ohjelmiston versio
  - Ohjelmiston latauskohde
  - Muita hienosäätöjä (Käytetäänkö Windowsin asennusajastuksia jne.)
- .sls tiedostoja voidaan myös isännöidä Git-repositorysta käsin
- Asennus/hallinnointi tapahtuu Saltin tai Gitin kautta
- Pakettien asennus suoritetaan ```pkg.install-``` komennolla ja asennuksen tarkistuksen voi tehdä ```pkg.installed-```

### Install libraries
- Käyttäessäsi Saltin Windows-paketinhallintaa isännöidyn Git-repon kautta, tulisi sinun asentaa kirjastot joko ```GitPython```, tai ```pygit2```

### Populate the local Git repository
- Master-ympäristössä .sls-tiedostot eivät ole oletuksena jaettu Saltin kanssa, joten tässä kohtaa tulisi alustaa & kloonata salt-winrepo-ng-repositorio komennolla: ```salt-run winrepo.update_git_repos```
  - Tämä kloonaa winrepo-repositoryn pääkoneelle winrepo_dir_ng -hakemistoon, jonka jälkeen pakettien määrittelytiedostot (.sls) haetaan Git-reposta 

- Masterless-ympäristössä minionille käytetään salt-call:ia alustamaan ja kloonaamaan salt-winrepo-ng
  - Tämä tapahtuu komennolla: ```salt-call --local winrepo.update_git_repos```
- Tämä kloonaa winrepo-repositoryn minionille winrepo_dir_ng -hakemistoon, jonka jälkeen pakettien määrittelytiedostot (.sls) haetaan Git-reposta

### Update minion database
- Suorita pkg.refresh_db Windowsin minioneilla päivittääksesi pakettitietokannat
  - Master-ympäristössä komennolla: ```salt -G 'os:windows' pkg.refresh_db```
  - Masterless ympäristössä komennolla: ```salt-call --local pkg.refresh_db```
- Edellä mainitut komennot päivittävät YAML/JINJA-paketinmäärittelytiedostot ja tulostavat pakettien päivitystietoja (mm. statistiikkaa onnistuneista/epäonnistuneista päivityksistä)

### Install software package
- Voit asentaa ohjelmapaketteja (esim. Firefoxin) käyttäen ```pkg.install``` komentoa:
  - Master-ympäristössä: ```salt * pkg.install 'firefox_x64'```
  - Masterless-ympäristössä: ```salt-call --local pkg.install "firefox_x64"```

### Usage
- Windows-paketinhallinnan alustavien tehtävien jälkeen voit käyttää Saltin paketinhallintakomentoja Windows-minioneilla. Esimerkkinä näistä toimii:
  - ```pkg.list_pkgs``` (Listaa järjestelmään asennetut paketit)
  - ```pkg.list_available``` - 
  - ```pkg.install``` - Asentaa (määritellyn) paketin
  - ```pkg.remove``` - Poistaa (määritellyn) paketin

## a) Paketti Windowsia

Tässä tehtävässä minun tuli asentaa Windowsiin ohjelmia käyttäen Saltin pkg.installed-funktiota. Asensimme 30.4.2024 opetuskerralla paketteja Windowsille käyttäen Saltin paketinhallinnointiratkaisuja, joten tämän tehtävän suoritus ei tuottanut ongelmia. Käytin tehtävässä Windows PowerShellissä ```history``` komentoa palauttaakseni mieleen tarvittavia komentoja, joita olin käyttänyt kyseisellä opetuskerralla.

Aloitin tehtävän päivittämällä Gitin pakettivarastot ```salt-call --local winrepo.update_git_repos``` komennolla. Tämän jälkeen päivitin uusimmat pakettitiedot ```salt-call --local pkg.refresh_db``` komennolla, jonka jälkeen olen valmis asentamaan ohjelmia!

Päätin asentaa 7-Zip pakkausohjelman. Tämä onnistui yksinkertaisesti komennolla ```salt-call --local state.single pkg.installed 7zip```, joka asentaa nimeämäni ohjelman (tässä tapauksessa 7-Zip). Tulostus ilmoittaa asennuksen onnistuneen ja 7-Zip versioksi 22.01.00.0. Suoritin komennon uudelleen varmistaakseni idenpotentin tilan. Toinen tulostus varmistaa 7-Zipin asennetuksi ja sen idempotenttisuuden.

![a](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/1062628c-b443-4712-b32f-d7fec5f4358c)

## b) Benchmark

Tässä tehtävässä minun tuli etsiä 3-7 keskitetyn hallinnan projektia, joita minun tuli arvioida.

### Janne Mustosen projekti (Mustonen 2020)
Tarkoitus:
  - Mustosen projektin tarkoituksena on luoda tila, jonka suorittamalla valmiiksi määritetyt ohjelmat asentuvat uusille koneille valmiiksi konffattuina. Tämän tarkoituksena on helpottaa/nopeuttaa uusien koneiden alustusta (esimerkiksi yritysympäristössä)
Lisenssi

  - Mustonen ei ole erikseen Wordpress-artikkelissaan määritellyt käyttämäänsä lisenssiä. Wordpress yleisesti käyttää GNU General Public License (GPLv2 tai tuoreempi) -lisenssiä, joka avoimen lähdekoodin lisenssin kautta antaa käyttäjälle laajat käyttöoikeudet, mutten näin epäselvässä tilanteessa uskaltaisi käyttää/soveltaa Mustosen projektia sen arvioinnin lisäksi

Tekijä & vuosi:
  - Janne Mustonen (2020)

Riippuvuudet:
  - Ubuntu (+ muut Debian-perheen distrot), Atom- & Stacer-repository, minion-kone

Kiinnostavaa:
  - Lopputulos onnistunut ja kuvat asennetuista ohjelmista hyvä lisä artikkeliin. Sovellukset toimivat hyvin yhdessä (ns. samaa teemaa) ja vaikuttavat tarkoin harkituilta

Avoimet Kysymykset ja muut huomiot:
  - Raportin synty ja sen tavoitteet oli mielestäni kuvailtu hyvin. Aihe oli tarpeeksi yksinkertainen, mutta juuri sellainen jota pienellä muokkauksella voi soveltaa useisiin eri ympäristöihin (koti-/yrityskoneisiin). Mielestäni myös tiiviisti kirjoitettu ja selkeästi ilmaistu, mitä mikäkin konfiguraatio muodostuu ja mistä ne on opittu/lainattu

### Janne Mustosen projekti
Tarkoitus:
  -
Lisenssi:
  -
Tekijä & vuosi:
  - Janne Mustonen (2020)
Riippuvuudet:
  -
Kiinnostavaa:
  -

### Janne Mustosen projekti
Tarkoitus:
  -
Lisenssi:
  -
Tekijä & vuosi:
  - Janne Mustonen (2020)
Riippuvuudet:
  - Ubuntu (+ muut Debian-perheen distrot), Atom- & Stacer-repository
Kiinnostavaa:
  - 
Avoimet Kysymykset ja muut huomiot:



## c) Testbench

## d) Viisi idea

## References

Mustonen, J. 2020. Oma moduuli h7(Palvelinten hallinta). Lähde: https://jannelinux.design.blog/2020/05/19/oma-moduuli-h7/


