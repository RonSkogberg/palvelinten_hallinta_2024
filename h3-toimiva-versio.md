# h3 Toimiva versio

## a) Online

Tässä osiossa tehtävänäni on luoda GitHubiini uusi varasto ja vähintään yksi uusi tiedosto sinne. Uusi varasto toimii annetun tehtävän tulevien osioiden leikkikenttänä.

Kirjauduttuani GitHubiin käyttäjätunnuksillani, pystyin luomaan uuden varaston (repository) suoraan etusivulta painamalla "Create a new repository" painiketta. Täytin luontilomakkeen tiedot/asetukset. Varmistin, että loin pyydetyn README.md tiedoston ja käytin pyydettyä "summer" nimikettä tehtävänannon mukaisesti. Lopuksi valitsin GNU General Public License 3 -lisenssin.

![1](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/958e4455-ad06-4181-b974-7aa4c146879c)

Luotuani varaston varmistin vielä sen olemassaolon siirtymällä sinne. Lisenssit ja tiedostot näyttivät olevan kunnossa, joten eiköhän jatketa seuraavaan tehtävään.

![2](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/eddb6323-6df2-4764-8645-4c83bbba4b5b)

## b) Dolly

Tässä osiossa tehtävänäni on kloonata edellisessä osiossa luomani varasto, tehdä muutoksia sinne ja puskea ne palvelimelle. Lopuksi vielä tarkistin muutosten tapahtuneen.

Muistin, että generoimme luennolla Karvisen opastamana avainparin ```$ ssh-keygen``` komennolla, josta lisäsimme julkisen SSH-avaimen GitHub-käyttäjillemme. Halusin kuitenkin tehtävää varten luoda täysin uuden avainparin ja lisätä uuden julkisen SSH-avaimeni GitHubiin. Edellä mainittu ```$ ssh-keygen``` komento generoi sekä julkisen, että yksityisen SSH-avaimen piilotettuun .ssh -hakemistoon (piste hakemiston edessä tarkoittaa, että se on piilotettu). Suoritin generoinnin edellä mainitulla komennolla, jonka jälkeen johdosta komentorivi ilmoitti minulla olevan jo SSH-avaimet oletushakemistossa /home/vagrant/.ssh ja että haluanko korvata ne uusilla. Suoritin yliajon ja siirryin tehtävän seuraavaan osioon.

![6](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/f6b25567-7885-4cc2-a522-31012ae1eca7)

Siirryin tarkistamaan SSH-avaimieni oletushakemiston sekä varmentamaam avaimien olemassa olon ja siellähän molemmat avaimeni olivat. Avasin id_rsa.pub-tiedoston ja kopioin julkisen avaimeni Githubin käyttäjälleni.

![9](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/7f366ab8-8854-43bb-bb4e-39aa53dc64df)

Nyt kun sain kopioitua GitHubistani reponi kloonauslinkin, siirryin virtuaalikoneeni terminaalin puolelle viimeistelemään kloonauksen ```$ git clone git@github.com:RonSkogberg/summer-comer.git``` komennolla. Kloonauksen aikana komentorivillä kysytään, että hyväksykö yhteyden luonnin siitäkin huolimatta, ettei GitHubin isäntäpalvelimen aitoutta voida varmentaa. Vastasin "yes", sillä pystyin tässä tapauksessa luottamaan yhteyden luotettavuuteen. Lopputuloksena syntyy "summer-comer" niminen hakemisto, johon siirryn seuraavaksi. Varmistin ```$ ls``` komennolla että hakemistossa on repon luomisvaiheessa tekemäni README.md -tiedosto.

![11](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/1a89203f-be9a-4e66-81bf-59279e481fcb)




## c) Doh!

## d) Tukki

## e) Suolattu rakki

## b) Dolly
