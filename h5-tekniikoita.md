# H5 Tekniikoita

## x) Lue ja tiivistä

###

###

###

###

## a) Asenna Salt Windowsille

Asensimme Saltin Windowsille Palvelinten hallinta -kurssin ensimmäisellä luennollamme 26.3.2024 Tero Karvisen ohjaamana. Todensin kuitenkin sen asennuksen tätä raporttia varten ```salt-call --local``` komennolla sekä ```salt-call --local info state.single user.present ron``` komennolla. Ensimmäinen näistä ilmaisee Saltin versionumeron, jonka tulosteesta voimme päätellä Saltin olevan asentuneena Windows-koneellani. Jälkimmäinen komento tarkistaa Saltin kautta lokaalisti, että onko käyttäjä "ron" olemassa. Tulostuksesta selviää, että käyttäjä "ron" on olemassa sekä ajan tasalla.

![1](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/18e23db3-5a98-49df-b913-e0f6c119c05c)

## b) Kerää Windows-koneesta tietoa grains.items -toiminnolla

Keräsin Windows-koneestani tietoja erilaisilla grains.items komennoilla. Aloitin yksinkertaisesti selvittämällä tietoja koneeni käyttöjärjestelmästä. Komennolla ```salt-call --local grains.item osmanufacturer osfinger osversion``` etsitään grains.itemeistä tietoa koneessani pyörivästä käyttöjärjestelmästä, sen valmistajasta sekä käyttöjärjestelmän versionumerosta. Tulostus paljastaa koneeni käyttöjärjestelmän takana olevan OS-mafia Microsoft Corporation ja läppärini pellin alla kehrää Windows 10:n versio 10.0.19045.

![osfinger](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/70daae52-caad-4bd2-997d-75bab52a8b9d)

Seuraavaksi lähdin tutkimaan Windows-koneeni prosessoritietoja. Tämä onnistui komennolla ```salt-call --local grains.item cpu_model cpuarch```. Komento ilmoittaa minun käyttäväni AMD64 arkkitehtuurilla pyörivä Intel core i5 kymppigeneraation CPU.

![CPU](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/584ec809-cee0-4f43-95d4-984b99d893f3)

Kolmanneksi tutkin vähän asentamaani Saltin tietoja ```salt-call --local grains.item saltpath saltversion``` komennolla. Ensimmäinen tulostus kertoo Saltin asennuspolun ja jälkimmäinen tulostus sen versionumeron, joka minun tapauksessani on 3007.0.

![salthaku](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/66889239-4da9-4085-b3c2-cb96840ea3a7)

## c) Kokeile Saltin file -toimintoa Windowsilla

![make1](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/ba48a835-20c0-4720-891c-c147b93bf320)

![make2](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/c1569bfc-7f03-4132-b70e-008177118586)

![make3](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/e8b48c6b-47f0-488a-bf62-cf59c971f53f)

## d) CSI Kerava

![find1final](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/ac19a089-e1b2-4a17-8762-3dc3b8706abb)

Kotona tein

![findhomefinal](https://github.com/RonSkogberg/palvelinten_hallinta_2024/assets/148875466/d5430d3f-d34e-4bf7-9613-9cede22ccb6d)


## References

Karvinen, T 2024. Infra as Code. https://terokarvinen.com/2024/configuration-management-2024-spring/

Karvinen, T 2021. Run Salt Command Locally. https://terokarvinen.com/2021/salt-run-command-locally/?fromSearch=run%20salt

Seppä, T. 2019. h1, korjaukset lopussa. https://salthomework.wordpress.com/h1/
