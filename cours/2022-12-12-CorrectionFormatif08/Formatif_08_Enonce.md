# Création d'une application Express

Ce projet a pour but de vous faire construire une application Express avec des routes de base et des routes avec paramètres.

## But

Vous devez créer une application qui  utilise les points de terminaisons suivantes :

/voyages
: retourne un tableau de tous les voyages en JSON 

/voyages/id (où id est un nombre ex: / voyages/3 ou / voyages/10) 
: retourne le voyage à l'indice id de la liste de voyages en JSON 

/voyages/random
: retourne un voyage au hasard du tableau de voyages en JSON \

/voyages/{ ORIGIN_COUNTRY_NAME } 
: retourne un tableau de tous les voyages en JSON avec le pays d’origine = ORIGIN_COUNTRY_NAME spécifié \

/voyages/{ DEST_COUNTRY_NAME } 
: retourne un tableau de tous les voyages en JSON avec le pays d’origine = DEST_COUNTRY_NAME spécifié \



# Élément fourni

 Le fichier flight_2015.json des citations.

Le code suivant permet d'importer les voyages dans votre application Express:

```js
// La variable voyages sera un tableau d'objet avec les clés "ORIGIN_COUNTRY_NAME " et "DEST_COUNTRY_NAME" et "count "  
// Le fichier flight_2015.json doit être dans le même dossier que l'application express.
const voyages = require('./flight_2015');
 
// Exemple d'utilisation
console.log(voyages[4].DEST_COUNTRY_NAME) // Affiche Egypt
```

# Requis technique

L'application Express n'est pas fournie, c'est à vous de l'installer avec le express-generator. \
L'application express doit être dans un fichier `app.js`.
