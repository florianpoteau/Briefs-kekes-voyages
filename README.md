# Briefs-kekes-voyages

Conception de la modélisation UML d'un système simplifié de réservation de vols pour l'agence de voyage Kékés Voyages.

## Projet

### Acteurs :

- Client
- Compagnie aérienne
- Utilisateur (Passager)

### Flux d'information :

- Informations sur les vols (disponibilité, horaires, escales)
- Informations sur les réservations (état, passagers)
- Informations sur les compagnies aériennes

### Fonctionnalités requises :

- Ouverture et fermeture des réservations de vol
- Annulation de vol par la compagnie
- Réservation de vols par les clients
- Annulation ou confirmation des réservations
- Gestion des détails des vols (aéroport de départ et d'arrivée, horaires, escales)
- Gestion des passagers et de leurs informations
- Gestion des compagnies aériennes

### Recensement des règles de gestion :

- Kékés Voyages peut intégrer une compagnie sur sa plateforme
- Un utilisateur peut créer un compte
- Un utilisateur doit avoir créer un compte pour :
  - Un utilisateur peut se connecter et se déconnecter
  - Kékés Voyages peut supprimer un utilisateur de sa plateforme
  - Un utilisateur doit être connecter pour :
    - Un utilisateur peut gérer son compte (modifier et/ou supprimer ses données et/ou supprimer son compte)
    - Un utilisateur peut réserver un vol
    - Un utilisateur doit avoir réserver un vol pour :
      - Un utilisateur peut annuler son vol
      - Un utilisateur peut confirmer son vol
- La compagnie aérienne peut proposer différents vols à la réservation
- La compagnie aérienne doit avoir proposer différents vols à la réservation pour :
  - La compagnie aérienne peut ouvrir un vol à la réservation
  - La compagnie aérienne doit avoir ouvert un vol à la réservation pour :
    - La compagnie aérienne peut refermer un vol à la réservation
    - La compagnie aérienne peut annuler un vol à la réservation

### Définition des règles de gestion dans le diagramme de classes :

Dans le cadre de la définition des règles de gestion dans le diagramme de classes, nous allons intégrer des contraintes et des règles spécifiques dans certaines classes du modèle. Les règles de gestion doivent garantir l'intégrité et la cohérence des données du système.

- **Règles de gestion liées aux classes :**

  - Chaque classe a un id qui lui est propre

  ***

- **Règles de gestion liées à la classe `Utilisateur` :**

  Un Utilisateur est un client

  **Contraintes**
  Un client peut réserver SEULEMENT si une compagnie aérienne a proposé un vol.
  Un client peut confirmer son vol MAIS avant le départ du vol Si il n’a pas annuler son vol
  Un client peut annuler son vol MAIS avant le départ du vol Si il n’a pas confirmer son vol

  **Obligations**
  Un client DOIT confirmer son vol Si il souhaite réellement le prendre SI il ne l’a pas annulé

  ***

- **Règles de gestion liées à la classe `Passager` :**

  - Un passager n’existe seulement si un utilisateur lui a réserver un vol

  ***

- **Règles de gestion liées à la classe `Reservation` :**

  - Une réservation concerne SEULEMENT un seul vol pour un seul passager.
  - Une réservation ne peut être faite que si le vol est ouvert à la réservation.

  ***

- **Règles de gestion liées à la classe `Vol` :**

  - Un vol ne peut pas avoir une date de départ ultérieure à la date d'arrivée.
  - Un vol a un aéroport de départ et un aéroport d’arrivée.
  - Un vol a un jour et une heure de départ, et un jour et une heure d’arrivée.
  - Un vol peut comporter des escales dans des aéroports.

  ***

- **Règles de gestion liées à la classe `CompagnieAerienne` :**

  -

  ***

- **Règles de gestion liées à la classe `Escale` :**

  - L'heure de départ d'une escale doit être antérieure à l'heure d'arrivée.
  - Une escale a une heure d’arrivée et une heure de départ.
  - Contrainte sur les escales : Les escales d'un vol doivent avoir une heure de départ antérieure à l'heure d'arrivée.

  ***

- **Règles de gestion liées à la classe `Aéroport` :**
  - Chaque aéroport dessert une ou plusieurs villes.

## Livrables

<ul>
<li>Règles de gestion</li>
<li>Diagramme de cas d'utilisation</li>
<li>Diagramme de classe</li>
<li>Diagramme de séquence</li>
</ul>

## Contributeurs

- **Yoan Bor**

  - Profil GitHub : [Yoan Bor](https://github.com/yoanbor)

- **Florian Poteau**
  - Profil GitHub : [Florian Poteau](https://github.com/florianpoteau)
