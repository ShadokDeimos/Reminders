# PROLOG

## Shortcuts

Espace      Continuer
Enter       Passer à la ligne / Finir

## Déclarer un ensemble de faits

Créer un fichier "faits.pl"

```
animal(chien).
animal(chat).
prenom(paul).
prenom(pierre).
prenom(jean).
```

consult(faits).

Voici les faits affirmés par notre programme :
* chien et chat sont des animaux
* paul, pierre et jean sont des prénoms

Une telle déclaration est appelée une règle
* le symbole :- dans une règle se lit "si"
* le symbole , (virgule) dans une règle se lit "et"

### Poser des question à Prolog

prenom(jean).       =>  Jean est il un prénom  => FALSE

animal(\_).          => Existe-t'il des animaux?

listing.           => Permet d'afficher le code source de la base de faits du programme courant.
