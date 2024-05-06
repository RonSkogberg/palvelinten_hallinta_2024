# h6 Benchmark

## x) Lue ja tiivistä (Salt Project. s.a.)

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
  - ```pkg.list_pkgs``` Listaa järjestelmään asennetut paketit
  - ```pkg.list_available``` - Listaa saatavilla olevat paketit
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

Lisenssi:
  - Mustonen ei ole erikseen Wordpress-artikkelissaan määritellyt käyttämäänsä lisenssiä. Wordpress yleisesti käyttää GNU General Public License (GPLv2 tai tuoreempi) -lisenssiä, joka avoimen lähdekoodin lisenssin kautta antaa käyttäjälle laajat käyttöoikeudet, mutten näin epäselvässä tilanteessa uskaltaisi käyttää/soveltaa Mustosen projektia sen arvioinnin lisäksi

Tekijä & vuosi:
  - Janne Mustonen (2020)

Riippuvuudet:
  - Ubuntu (+ muut Debian-perheen distrot), Atom- & Stacer-repository, minion-kone

Kiinnostavaa:
  - Lopputulos onnistunut ja kuvat asennetuista ohjelmista hyvä lisä artikkeliin. Sovellukset toimivat hyvin yhdessä (ns. samaa teemaa) ja vaikuttavat tarkoin harkituilta

Avoimet Kysymykset ja muut huomiot:
  - Raportin synty ja sen tavoitteet oli mielestäni kuvailtu hyvin. Aihe oli tarpeeksi yksinkertainen, mutta juuri sellainen jota pienellä muokkauksella voi soveltaa useisiin eri ympäristöihin (koti-/yrityskoneisiin). Mielestäni myös tiiviisti kirjoitettu ja selkeästi ilmaistu, mitä mikäkin konfiguraatio muodostuu ja mistä ne on opittu/lainattu

### Toni Vapalon projekti (Vapalo 2021)
Tarkoitus:
  - Vapalon projektin tarkoituksena on automatisoida Saltin avulla kaksi kehitysympäristöä (Python flask & React). Kehitysympäristöjen automatisoinnin hyötynä on, että uusien ympäristöjen uudelleenluonti on nopeaa, jos esimerkiksi käyttäjä tekee testejä eri ympäristöissä ja ympäristöt esimerkiksi hajoavat. 

Lisenssi:
  - Vapalo ei ole sivustonsa artikkelissa määrittänyt mitään lisenssiä, mutta hänen linkkaamassaan GitHub-repossaan (jossa on projektiin liittyvää aineistoa), hän käyttää GPL-3.0 lisenssiä. Kuten Mustosen Lisenssi-osiossa ilmaisinkin, antaa GPL-lisenssi käyttäjälle yleismaalliset vapaudet muokata sekä käyttää hänen luomaansa sisältöä omiin tarkoituksiinsa

Tekijä & vuosi:
  - Toni Vapalo (2021)

Riippuvuudet:
  - Debian 10, GitHub, vbox.list

Kiinnostavaa:
  - Vaikkei lopputulos kuvastanut alkutavoitteita, oli ympäristöjen luominen yleisesti ottaen onnistunut. Kuvittelisin tästä olevan pienellä viilauksilla hyötyä jollekin, joka haluaa luoda tämän kaltaisia kehitysympäristöjä

Avoimet Kysymykset ja muut huomiot:
  - Ihan hyvä raportti näin yleisesti. Kuvia oli paljon, ehkä vähän liikaakin, mutta parempi niin kuin päinvastoin

### Simo Tossavaisen projekti (Tossavainen 2021)
Tarkoitus:
  - Tossavaisen projektin tarkoituksena on luoda simppeli hyötyohjelmamoduli, vähän samantapainen kuin Mustosella, mutta tässä hän myös konfiguroi Firefoxin asetukset tottumustensa mukaisiksi. Tällainen ratkaisu on hyvä, jos haluaa luoda valmiin asennustilan, jonka suorittaa esimerkiksi aina uuden koneen hankkiessaan, jolloin itselle suotuisat asetukset ovat aina valmiina heti asennuksen jälkeen

Lisenssi:
  - Tossavainen ilmoittaa lisenssikseen GNU GENERAL PUBLIC LICENSE, eli hänen tuotoksensa on vapaata riistaa omaan käyttöön avoimen GPL-lisenssin mukaisesti

Tekijä & vuosi:
  - Simo Tossavainen (2021)

Riippuvuudet:
  - Mozilla Firefox, tree, Libreoffice, 

Kiinnostavaa:
  - find-komennon käyttö oli hyvä tapa löytää Firefoxin suorittamia muutoksia. Komennon avulla Tossavainen pystyi helposti päättelemään mitä hänen Firefoxin työpöydällä tekemät muutokset muokkasivat, jolloin niiden poimiminen oli helppoa

Avoimet Kysymykset ja muut huomiot:
  - Simppeli, mutta informoiva ohje kuinka asentaa ohjelmia Saltilla. Kiinnostavampi osuus tehtävässä oli Firefoxin konfigurointien metsästys ja muokkaus

## c) Testbench

Tässä tehtävässä minun tulee ajaa jonkun edellisen tehtävän tiloista. Valitsin Simo Tossavaisen projektin, sillä se oli sopivan simppeli meikäläisen makuun, enkä ollut käyttänyt Apachen find-komentoa muutamaa kertaa enempää. Projektissa käytetyt ratkaisut eivät myöskään lataa mitään paketinhallinnan ulkopuolelta, joten se on turvallinen ratkaisu tällaiseen testailuun.

[Päivitän tätä vielä 6.5.2024]

## d) Viisi idea

Tässä tehtävässä minun tulee listata viisi ideaa omalle modulille. 

Mahdollisia moduli-ideoita ovat esimerkiksi:
  - Opiskelijoille sopivan paketinasennustilan luominen (Asentaa listan ohjelmistoja useille minioneille. Paketteja kuten Blender, Shotcut, Scilab...)
  - Sääpalvelu (Hakee tietoja netistä ja palauttaa ne käyttäjälle)
  - Muistiinpanojen hallinta (Hyvä opiskelijalle, joka haluaa hallinoidun tavan hallita muistiinpanoja Saltia käyttäen)
  - Tyhjien koneiden automaattinen luonti konfiguroiduilla asetuksilla
  - Oppimispäiväkirjan ylläpito

## References

Salt Project. s.a. Windows Package Manager. Lähde: https://docs.saltproject.io/en/latest/topics/windows/windows-package-manager.html#list-pkgs

Karvinen, T. 2024. Infra as Code - Palvelinten hallinta 2024. Lähde: https://terokarvinen.com/2024/configuration-management-2024-spring/

Mustonen, J. 2020. Oma moduuli h7(Palvelinten hallinta). Lähde: https://jannelinux.design.blog/2020/05/19/oma-moduuli-h7/

Vapalo, T. 2021. Oma moduli. Lähde: https://tonivapalo.com/posts/palvelintenhallinta/phvt7/

Tossavainen, S. 2021. h7 Oma moduli. Lähde: https://simotossavainen.wordpress.com/2021/05/19/h7-oma-moduli/
