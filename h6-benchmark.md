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

## b) Benchmark

## c) Testbench

## d) Viisi idea
