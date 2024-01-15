# Briefs-kekes-voyages

Conception de la modélisation UML d'un système simplifié de réservation de vols pour l'agence de voyage Kékés Voyages.

<a href="https://briefskekevoyages.notion.site/Briefs-K-k-s-Voyages-UML-dd64da28651049e684b0996a561a51ae"><img src="https://img.shields.io/badge/Notion-000?logo=notion&logoColor=fff&style=for-the-badge"></img></a>

## Acteurs :

Futur client = Utilisateur n’ayant pas créer de compte, pouvant s’inscrire

Client = Utilisateur ayant créer un compte et étant donc connecté

Compagnie aérienne = Compagnies proposant les vols

Kékés Voyages = l’Agence de Voyages

## Règle de gestion

### Dans le diagramme de cas d’utilisation :

Le futur client peut Créer un compte, après l’avoir fait il devient client

- Un client peut se connecter et se déconnecter
- Kékés Voyages peut intégrer une compagnie sur sa plateforme
- Kékés Voyages peut supprimer un client de sa plateforme
- Un client doit être connecter (includes “s’identifier”) pour :
  - Un client peut gérer son compte :
    - Modifier et/ou supprimer ses données (cas particuliers)
    - Supprimer son compte (cas particuliers)
  - Un client peut réserver un vol
  - Un client doit avoir réserver un vol (includes “Réserver un vol”) pour gérer ses réservations :
    - Un client peut annuler son vol (cas particulier)
    - Un client peut confirmer son vol (cas particulier)
- La compagnie aérienne peut proposer différents vols à la réservation
- La compagnie aérienne doit avoir proposer différents vols à la réservation pour :
  - La compagnie aérienne peut ouvrir un vol à la réservation
  - La compagnie aérienne doit avoir ouvert un vol à la réservation pour :
    - La compagnie aérienne peut refermer un vol à la réservation
    - La compagnie aérienne peut annuler un vol à la réservation

### Dans le diagramme de classe :

L’utilisateur hérite de Passager

- Il y a 1 utilisateur pour 1 ou plusieurs réservations

- Il y a 1 seule réservation pour 1 seul passager

- Il y a plusieurs passagers pour 1 seul vol

- Il y a plusieurs vols pour plusieurs compagnies

- Il y a plusieurs vols pour 2 aéroports (de départ & d’arrivé)

- Il y a 1 vol pour 0 ou plusieurs escales (agrégation faible)

- Il y 1 aéroport pour 1 escale (agrégation faible)

Agrégation faible = ici l’escale peut ne pas exister sans altérer le reste du diagramme, un vol peut ne pas avoir d’escale, un aéroport peut ne pas être une escale.

**Définition des règles de gestion dans le diagramme de classes :**

Dans le cadre de la définition des règles de gestion dans le diagramme de classes, nous allons intégrer des contraintes et des règles spécifiques dans certaines classes du modèle. Les règles de gestion doivent garantir l'intégrité et la cohérence des données du système.

- **Règles de gestion liées aux classes :**

  - Chaque classe a un id qui lui est propre

- **Règles de gestion liées à la classe `Utilisateur` :**
  Un Utilisateur est un client
  **_Contraintes_**
  Un client peut réserver SEULEMENT si une compagnie aérienne a proposé un vol.
  Un client peut confirmer son vol MAIS avant le départ du vol Si il n’a pas annuler son vol
  Un client peut annuler son vol MAIS avant le départ du vol Si il n’a pas confirmer son vol
  ***
  **_Obligations_**
  Un client DOIT confirmer son vol Si il souhaite réellement le prendre SI il ne l’a pas annulé
- **Règles de gestion liées à la classe `Passager` :**

  - Un passager n’existe seulement si un utilisateur lui a réserver un vol

- **Règles de gestion liées à la classe `Reservation` :**

  - Une réservation concerne SEULEMENT un seul vol pour un seul passager.
  - Une réservation ne peut être faite que si le vol est ouvert à la réservation.

- **Règles de gestion liées à la classe `Vol` :**

  - Un vol ne peut pas avoir une date de départ ultérieure à la date d'arrivée.
  - Un vol a un aéroport de départ et un aéroport d’arrivée.
  - Un vol a un jour et une heure de départ, et un jour et une heure d’arrivée.
  - Un vol peut comporter des escales dans des aéroports.

- **Règles de gestion liées à la classe `Escale` :**

  - L'heure de départ d'une escale doit être antérieure à l'heure d'arrivée.
  - Une escale a une heure d’arrivée et une heure de départ.
  - Contrainte sur les escales : Les escales d'un vol doivent avoir une heure de départ antérieure à l'heure d'arrivée.

- **Règles de gestion liées à la classe `Aéroport` :**
  - Chaque aéroport dessert une ou plusieurs villes.

### Dans le diagramme de séquence :

_Partie concernant le compte de l’utilisateur :_

- **Si l’utilisateur n’a pas de compte**
  - l’utilisateur clique sur s’inscrire
  - La plateforme renvoie le formulaire d’inscription
  - L’utilisateur mets ses informations personnelles obligatoires
  - La plateforme envoie un mail de confirmation
  - L’utilisateur valide son mail
  - La plateforme renvoie une instance d’utilisateur
- **Si l’utilisateur a déjà un compte**

  - L’utilisateur clique sur se connecter
  - L’utilisateur renseigne ses informations
  - La plateforme vérifie les informations
  - La plateforme informe l’utilisateur qu’il est connecté
  - **Si l’utilisateur modifie son compte**
    - L’utilisateur clique sur modifier son compte
    - L’utilisateur renseigne ses informations actuelles
    - L’utilisateur renseigne ses nouvelles informations
    - La plateforme confirme à l’utilisateur la modification de son compte
  - **Si l’utilisateur supprime son compte**
    - L’utilisateur clique sur supprimer son compte
    - L’utilisateur confirme la suppression de son compte
    - La plateforme confirme la suppression du compte de l’utilisateur

  _Partie concernant la réservation :_

- La compagnie aérienne ouvre le vol à la réservation
- La plateforme vérifie si l’utilisateur est connecté
- L’utilisateur renseigne les informations personnelles du passager au système de réservation
- Le système de réservation renvoie le formulaire de paiement à l’utilisateur
- L’utilisateur paie la réservation
- Le système de réservation renvoie à l’utilisateur un billet à valider pour un passager
- **Si l’utilisateur confirme son billet à la plateforme de réservation**
  - La plateforme de réservation envoie un billet validé au passager
  - **Si l’utilisateur annule le vol:**
    - La compagnie aérienne annule la validité des tickets
    - La compagnie aérienne rembourse les passagers
  - **Si l’utilisateur confirme le vol**
    - L’aéroport fait décoller l’avion pour le vol
    - **Si il y a une escale pendant le vol:**
      - Le vol s’arrête à l’escale
      - Le vol décolle à partir de l’escale
    - Le vol arrive à l’aéroport
    - La compagnie aérienne ferme le vol
- **Si l’utilisateur annule son billet:**
  - La plateforme de réservation annule le billet pour 1 passager

## Livrables

<ul>
<li>Règles de gestion</li>
<li>Diagramme de cas d'utilisation</li>
<li>Diagramme de classe</li>
<li>Diagramme de séquence</li>
</ul>

## Contributeurs

-**_Yoan Bor_**

<a href="https://github.com/yoanbor"><img src="https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white"></img></a>

-**_Florian Poteau_**

<a href="https://github.com/florianpoteau"><img src="https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white"></img></a>
