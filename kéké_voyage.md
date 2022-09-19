# Contexte du projet

<span class="colour" style="color:var(--text-color,#000000)">Votre client, une agence de voyages, souhaite proposer la possibilité de réserver en ligne des billets d'avion à leurs clients.</span>

<span class="colour" style="color:var(--text-color,#000000)">Votre mission est de concevoir à l'aide du standard UML la modélisation de la plateforme.</span>

<span class="colour" style="color:var(--text-color,#000000)">La plateforme devra permettre :</span>

* Un vol est ouvert à la réservation et refermé sur ordre de la compagnie.
* Un vol peut être annulé par la compagnie
* Un client peut réserver un ou plusieurs vols, pour des passagers différents.
* Une réservation concerne un seul vol et un seul passager.
* Une réservation peut être annulée ou confirmée.
* Un vol a un aéroport de départ et un aéroport d’arrivée.
* Un vol a un jour et une heure de départ, et un jour et une heure d’arrivée.
* Un vol peut comporter des escales dans des aéroports.
* Une escale a une heure d’arrivée et une heure de départ.
* Chaque aéroport dessert une ou plusieurs villes.
* Des compagnies aériennes proposent différents vols.<span class="colour" style="color:rgb(0, 0, 0)"></span>

# Regle de gestion

RESERVATION

* un email de contact
* un numéro de téléphone
* nom
* prenom
* un n° de passport
* peu être annuler par le CLIENT
* une réservation ne peu être que pour une seul personne et un seul vol
* numéro de réservation
* peu être confirmé par l'agence

VOL

* le vol contient un numero de vol
* aeroport de depart, une date, une heure
* aeroport d'arrive, une date, une heure
* vol avec un ou plusieur passager
* un vol ne peux pas être reservable ou non
* un vol peut faire des escale dans un AEROPORT
* le vol est un trajet d'un aeroport à un autre
* un vol peut être annulé par la compagnie
* numéro de vol

COMPAGNIE

* contiens un nom
* peu avoir un ou plusieurs vol

ESCALE

* une date et une heure d'arrivé
* une date et une heure de départ
* un aeroport d'arrivé
* un aeroport de dépar

AEROPORT

* ce trouve dans une ville

VILLE

* un nom
* se trouve dans une ville
* Pays

## Dictionnaire de données

| Nom | Type | Désignation |
| --- | :---: | :---------- |
| nom\_compagnie | Alphanumérique | nom de la compagnie aérienne |
| numero\_vol | Numérique | id destination du vol |
| nombre\_billet | Numérique | nombre de billet réserver |
| reservation | Alphanumérique | réservation fait par le client |
| ouverture\_reservation | Boolean | ouverture/fermeture de la reservation par la compagnie |
| annulation\_reservation | Boolean | annulation ou non de la réservation par le client |
| annulationvol | Boolean | annulation du vol ou non par la compagnie |
| aeroport | Alphanumérique | annulation ou non de la réservation par le client |
| date\_depart | Date | date du depart du vol |
| date\_arriver | Date | date d'arriver du vol |
| nom\_ville | Alphanumérique | nom de l'aéroport |
| nom\_pays | Alphabétique | nom du pays |
| confirmation\_vol | Boolean | validation ou non d'un vol |
| depart\_escale | Date/heure | depart de l'escale |
| arriver\_escale | Date/heure | arriver de l'escale |
| email\_contact | Alphanumérique | email de contact de la personne ayant reserver |
| nompassager | Alphabétique | nom du passager |
| prenom\_passager | Alphabétique | prenom du passager |
| age\_passager | Numérique | age du passager |
| passeport\_passager | Alphanumérique | passeport du passager |
| price\_reservation | Numérique | prix de la réservation |
| date\_reservation | Date/heure | date de la réservation |

# MCD - Modèle Conceptuel de Données

Le MCD a pour but de décrire de manière<span class="colour" style="color:rgb(36, 41, 47)"> formelle les données d'un système d'information (SI). Le MCD décrit la sémantique, c’est-à-dire le sens, attachée à ces données et à leurs rapports, et non l’utilisation qui en est faite.</span>

Afficher le MCD

# MLD - Modèle Logique de Données

Le MLD est <span class="colour" style="color:rgb(36, 41, 47)">la transformation du MCD en un ensemble de tables. Il est la représentation des données d'un système d'information et est généré à partir du MCD.</span>

Afficher le MCD

# MPD - Modèle Physique de Données


## Script SQL

```
CREATE TABLE company(
   Id_company COUNTER,
   company_name VARCHAR(50),
   IATA_code VARCHAR(50),
   PRIMARY KEY(Id_company)
);

CREATE TABLE country(
   Id_country COUNTER,
   PRIMARY KEY(Id_country)
);

CREATE TABLE city(
   Id_city COUNTER,
   Id_country INT NOT NULL,
   PRIMARY KEY(Id_city),
   FOREIGN KEY(Id_country) REFERENCES country(Id_country)
);

CREATE TABLE airport(
   Id_airport COUNTER,
   airport_name VARCHAR(50),
   country VARCHAR(50),
   city VARCHAR(50),
   zip_code INT,
   Id_city INT NOT NULL,
   PRIMARY KEY(Id_airport),
   FOREIGN KEY(Id_city) REFERENCES city(Id_city)
);

CREATE TABLE flight(
   Id_flight COUNTER,
   numero_vol VARCHAR(50),
   starting_date DATE,
   arriving_date DATE,
   starting_time TIME,
   arriving_time TIME,
   flight_status INT,
   Id_airport_arriving INT NOT NULL,
   Id_airport_start INT NOT NULL,
   Id_company INT NOT NULL,
   PRIMARY KEY(Id_flight),
   FOREIGN KEY(Id_airport_arriving) REFERENCES airport(Id_airport),
   FOREIGN KEY(Id_airport_start) REFERENCES airport(Id_airport),
   FOREIGN KEY(Id_company) REFERENCES company(Id_company)
);

CREATE TABLE booking(
   Id_booking COUNTER,
   booking_number VARCHAR(50),
   last_name VARCHAR(50),
   first_name VARCHAR(50),
   date_of_birth DATE,
   passport_number VARCHAR(50),
   email VARCHAR(50),
   Id_flight INT NOT NULL,
   PRIMARY KEY(Id_booking),
   FOREIGN KEY(Id_flight) REFERENCES flight(Id_flight)
);

CREATE TABLE stopover(
   Id_flight INT,
   Id_airport INT,
   starting_date DATE,
   arriving_date TIME,
   PRIMARY KEY(Id_flight, Id_airport),
   FOREIGN KEY(Id_flight) REFERENCES flight(Id_flight),
   FOREIGN KEY(Id_airport) REFERENCES airport(Id_airport)
);

```


Afficher le MCD


