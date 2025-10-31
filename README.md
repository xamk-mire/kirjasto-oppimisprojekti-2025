# Kirjaston-lainaus-ja-palautus-oppimisprojekti-2024

Oppimisprojekti on täysin opiskelijan itsenäinen suoritus ja ratkaisuihin tarvittavaan materiaaliin perehtyminen sekä niiden löytäminen on osa suoritusta. Projektilla siis harjoitellaan ja opitaan myös itsenäisiä tiedonhaun ja dokumentaation lukemisen taitoja, joka on keskeinen osa sovellusohjelmoijan osaamista. 

Oppimisprojektissa toteutettava sovellus on kuvitteellinen kirjaston lainaus- ja palautusautomaatti, tarkemmin sen ohjelmisto. Sovelluksen vaatimukset ovat kuvattu oppimistehtävien tapaan GitHub-projektina. Oppimisprojektista kirjoitetaan myös raportti, mutta oppimistehtävistä poiketen projektiraportissa on osana suoritusta teoreettinen osuus. 

# Kirjaston tietokanta schema
Alta löydät oppimisprojektissa käytettävän relaatiotietokannan scheman (skeema/malli/kaava).

Itse tietokannan taulut löytyvät **LibraryTables** -kansion sisältä. Jokaisesta taulusta on olemassa 2 eri tiedosto muotoa .sql ja .csv, mutta itse sisältö on sama riippumatta käytettävästä tiedostosta.

## 1. Books
Tallentaa kirjaston kirjojen tiedot.

| Sarakkeen nimi    | Tietotyyppi | Kuvaus                                 |
|-------------------|-------------|----------------------------------------|
| book_id           | INT         | Pääavain, kirjan yksilöllinen tunniste |
| isbn10            | VARCHAR     | Kirjan 10-numeroinen ISBN-numero       |
| title             | VARCHAR     | Kirjan otsikko                         |
| subtitle          | VARCHAR     | Kirjan alaotsikko, jos on              |
| authors           | VARCHAR     | Kirjoittajien nimet (voi olla luettelo) |
| categories        | VARCHAR     | Kirjan kategoriat tai genret           |
| thumbnail         | VARCHAR     | Kirjan pikkukuvan URL tai polku        |
| description       | TEXT        | Kirjan kuvaus tai tiivistelmä          |
| published_year    | YEAR        | Vuosi, jolloin kirja julkaistiin       |
| average_rating    | DECIMAL     | Kirjan keskimääräinen arvio            |
| num_pages         | INT         | Kirjan sivumäärä                       |
| ratings_count     | INT         | Kirjan saatujen arvioiden määrä        |

## 2. Members
Tallentaa kirjaston jäsenten tiedot.

| Sarakkeen nimi    | Tietotyyppi | Kuvaus                                 |
|-------------------|-------------|----------------------------------------|
| member_id         | INT         | Pääavain, jäsenen yksilöllinen tunniste |
| first_name        | VARCHAR     | Jäsenen etunimi                        |
| last_name         | VARCHAR     | Jäsenen sukunimi                       |
| email             | VARCHAR     | Jäsenen sähköpostiosoite               |
| phone             | VARCHAR     | Jäsenen puhelinnumero                  |

## 3. Transactions
Seuraa kirjojen lainausta ja palautusta.

| Sarakkeen nimi    | Tietotyyppi | Kuvaus                                 |
|-------------------|-------------|----------------------------------------|
| transaction_id    | INT         | Pääavain, tapahtuman yksilöllinen tunniste |
| book_id           | INT         | Vierasavain, viittaa Books-tauluun (book_id) |
| member_id         | INT         | Vierasavain, viittaa Members-tauluun (member_id) |
| issue_date        | DATE        | Päivä, jolloin kirja lainattiin        |
| due_date          | DATE        | Päivä, jolloin kirja tulee palauttaa   |
| return_date       | DATE        | Päivä, jolloin kirja palautettiin      |
| status            | ENUM        | Tapahtuman tila (esim. 'lainattu', 'palautettu', 'myöhässä') |
| late_fee          | DECIMAL     | Myöhästymismaksu, jos kirja palautettiin myöhässä |

## 4. Fees
Tallentaa myöhästymismaksut ja niiden maksutilanteen.

| Sarakkeen nimi    | Tietotyyppi | Kuvaus                                 |
|-------------------|-------------|----------------------------------------|
| fee_id            | INT         | Pääavain, maksutapahtuman yksilöllinen tunniste |
| transaction_id    | INT         | Vierasavain, viittaa Transactions-tauluun (transaction_id) |
| member_id         | INT         | Vierasavain, viittaa Members-tauluun (member_id) |
| fee_amount        | DECIMAL     | Myöhästymismaksun määrä                |
| payment_status    | ENUM        | Maksun tila (esim. 'maksamaton', 'maksettu') |
| payment_date      | DATE        | Päivä, jolloin maksu suoritettiin      |
