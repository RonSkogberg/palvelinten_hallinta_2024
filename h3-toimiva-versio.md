# h3 Toimiva versio

## x) Lue ja tiivistä

# What is Git? (Git s.a)
- Git on versionhallintajärjestelmä, joka tallentaa dataa snapshotteina
- Git toimii paikallisesti, eikä vaadi jatkuvaa internet-yhteyttä
- Gitissä tietoa lisätään, eikä sitä voi suoranaisesti poistaa tai muokata ilman, että muokkauksesta jää jälkiä
    - Tämä edesauttaa Gitin tiedon eheyden säilymistä
- Gitissä tieto voi olla kolmessa eri tilassa: modified, staged, and committed
- Gitillä tehtyjä muutoksia on helppo seurata sen eri työkaluja hyödyntäen

# Gitin käyttö (DataCamp 2019)
- git add = Lisää kaikki muutokset niin sanottuun välitilaan odottamaan commit-komentoa
- git commit = Tallentaa muutokset ja tällöin lisätään commit-viesti, että mitä muutoksia on tehty
- git pull = Vetää repositorysta päivitetyimmän tiedon
- git push = Työntää tehdyt muutokset kyseiseen repoon

# Suolax (Karvinen 2024a)
- Karvinen luo suolax-repon käyttäen GNU GENERAL PUBLIC LICENSE Version 3 -lisenssiä
- Karvinen päivittää repon luomisvaiheessa luomaansa README.md -tiedostoa
- Karvinen luo moduuli-tiedoston, joka Saltilla luo Hello World -tiedoston
- Karvinen luo Makefile-tiedoston, joka sisältää ohjeita koskien edellistä luomaansa tiedostoa (O'reilly s.a)
- Karvinen luo tila-tiedoston, joka asentaa lemppari sovelluksia, kuitenkin vasta pelkän "treen"
- Karvinen päivittää aiemmin luomaansa tila-sovellusta lisäämällä asennettavia sovelluksia ja luo listan top.sls tiedostoon asennetuista sovelluksista
- Karvinen siisti aiemmin luomaansa README.md -tiedostoa. Hän korvasi yhden Salt-komennon toisella
- Karvinen päivitti luomiaan käyttöohjeita

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

Todettuani repon kloonatuksi, loin sinne kesalomalista.md nimisen tiedoston, johon lisäsin hieman tietoa yrityksen työntekijöiden kesäloma-ajankodista. ```$ git add . && git commit ; git pull && git push``` komennolla pystyn siirtämään tekemäni tiedostot/muutokset repositoryyn. komennon "git add . " lisää kaikki muutokset niin sanottuun välitilaan, josta ne lopulta tallennetaan "git commit" komentoa käyttäen. Tämä komento tallentaa muutokset ja silloin lisätään commit-viesti, että mitä muutoksia on tehty (esimerkissäni lisäsin "Add employees' summer vacation schedule file" viestin). "git pull" vetää repositorysta päivitetyimmän tiedon ja "git push" työntää tekemäni muutokset kyseiseen repoon.


![12](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/0539d9b3-b9c5-4f30-83e9-3004d90cc994)

![13](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/c1db2325-96f9-4219-a13e-072f71cc901f)

Lopuksi varmistin vielä nettiselaimeni puolella, että tuotokseni on siirtynyt GitHubin puolelle. Tiedosto oli luotu.

![15](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/aef2783d-ac90-40ac-bd00-d502d28e9670)

## c) Doh!

Tässä osiossa tehtävänäni on tehdä tyhmiä muutoksia gittiin, ilman committia. Lopuksi tuhoan tekemäni muutokset.

Oho! Yrityksen työntekijöiden työluottokorttien pin-koodit vuotivat kesälomalistatiedostoon. Arkaluontoiset tiedot on poistettava heti.

Muokkaan tässä tehtävässä aiemmin luomaani kesalonalista.md -tiedostoa. Tiedostomuutokset tein nanolla ja varmistin cat-komennolla muutokset. Ttehokkain tapa tuhota arkaluontoiset tiedot on käyttää ```$ git reset --hard``` komentoa. Komennon "git reset" osuus purkaa pelkästään commitin. Kun siihen lisätään "--hard" osuus, purkaa se commitin SEKÄ
poistaa indeksistä sekä työkopiosta kaikki viime commitin jälkeiset muutokset (Polvinen 2020). Lopuksi tarkistin, että aiemmin lisätyt tiedot ovat peruutettu lukemalla kesalomalista.md tiedoston sisällön. Tiedot ovat peruutettu ja pin-koodit poistettu listalta.

![14](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/8748937a-60d6-4729-b30d-a3f74d5f7c49)

Huomautuksena vielä, että ```$ git reset --hard``` komentoa ei voi peruuttaa ja sitä tulisi käyttää harkiten, sillä se todellakin poistaa kaikki tallentamattomat muutokset.

## d) Tukki

Tässä osiossa tehtävänäni on tutkia hieman varastoni lokia. Käytin osiossa Tero Karvisen vinkkejä (Karvinen 2024).

Suoritin virtuaalikoneeni terminaalissa komennon ```$ git log -patch``` ja lopputulos näytti tältä:

![16](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/0af856d7-632f-4bde-ba35-fb4397a0f2fa)

Alempi commit-merkintä, jossa authorina on RonSkogberg (yhteen kirjoitettuna), lienee tullut silloin, kun suoritin kloonauksen SSH-linkin kautta. Tässä RonSkogberg viittaa GitHub-käyttäjääni. Ylempi commit-merkintä, jossa on mainittu "Add employees' summer vacation schedule file", viittaa aiempaan kohtaan kun suoritin komennon ``$ git add . && git commit ; git pull && git push``` Dolly-tehtävässä. Lokimerkintöjä näyttää siis jäävän kaikista toimenpiteistä, jotka ovat tallennettu/commattu. Edellisen tehtäväosion (Doh!) lokimerkintää ei jäänyt talteen, koska en suorittanut committia. Tarkastelin lopuksi nimeni ja sähköpostiosoitteen muotoilun ja ne näyttivät mielestäni hyvältä, joten jätin ne sikseen.

## e) Suolattu rakki

Tässä osiossa ajan Salt-tiloja omasta varastostani. Luon yksinkertaisen cowsay.sls tiedoston, joka ajetaan suorittamalla ```$ sudo salt-call --local --file-root /srv/salt/ state.apply cowsay``` komento. Toistin lopussa komennon uudestaan varmistaakseni idempotenttisen tilan.

![17](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/e6b76249-584d-4df5-9cc6-5bc1f074bb09)

## References

DataCamp 2019: GIT Push and Pull Tutorial. https://www.datacamp.com/tutorial/git-push-pull

Git s.a. 1.3 Getting Started - What is Git? https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F

Karvinen 2024a: suolax. https://github.com/terokarvinen/suolax/

Karvinen 2024b: Infra as Code 2024. https://terokarvinen.com/2024/configuration-management-2024-spring/

O'reilly s.a. 1.15. Building A Simple “Hello, World” Application with GNU make. https://www.oreilly.com/library/view/c-cookbook/0596007612/ch01s16.html

Polvinen 2020: Pieni Git-opas. 2.2 Paikallisen commitin muokkaus (git amend). University of Turku. Luettavissa: https://vm.utu.fi/document/fi_pieni-git-opas.pdf
