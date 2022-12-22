// ***************************************//
// ************* EXPLICATION 1 ***********//
// ***************************************//


/*
***require('express') *** :  	Vous utiliserez la fonction require de Node pour utiliser le module express.
***require *** : 			 	require est similaire à des mots-clés comme import ou include dans d'autres langues.
***require('express') *** :  	require prend le nom d'un package comme argument de chaîne et renvoie un package.
*** const express = require('express')***
*** const express ***	  :		L'objet renvoyé n'a rien de spécial.
*** const express ***	  :	Il s'agit souvent d'un objet, mais il peut s'agir d'une fonction, d'une chaîne ou d'un nombre.

*/

// ************* EXPLICATION 1 ***********//
const express = require('express');











// ************* EXPLICATION 2 ***********//
/*
***
Réception des données:
body-parser, extrait les données au format JSON.
body-parser extrait la partie entière du corps d'un flux de demandes entrantes et l'expose sur le body de l'objet request (req.body).
Le json-parser fonctionne de telle sorte  qu'il prend les données JSON d'une demande, les transforme en un objet JavaScript
et les attache ensuite à la propriété body de l'objet request avant que le gestionnaire de route ne soit appelé.
L'intergiciel faisait auparavant partie d'express.js, mais vous devez désormais l'installer séparément.
Ce site body-parser analyse les données codées en JSON, buffer, string et URL soumises à l'aide du module HTTP POST demande.
Installer body-parser en utilisant NPM comme indiqué ci-dessous.
npm install body-parser --save
Source 1: https://prograide.com/pregunta/21487/que-fait-le-body-parser-avec-express
Source 2: https://fullstackopen.com/fr/part3/node_js_et_express
***
*/

// ************* EXPLICATION 2 ***********//
const bodyParser = require('body-parser')








// ************* EXPLICATION 3 ***********//
/*
***
Appelle la fonction express "express()" et place la nouvelle application Express
dans la variable app (pour démarrer une nouvelle application Express).
C'est quelque chose comme si vous créiez un objet d'une classe.
***
*/
// ************* EXPLICATION 3 ***********//
const app = express();






// ************* EXPLICATION 4 ***********//
/*
***
L'encodage d'URL convertit les caractères dans un format qui peut être transmis sur Internet.
Les URL ne peuvent être envoyées que sur Internet en utilisant le jeu de caractères ASCII.
Étant donné que les URL contiennent souvent des caractères
en dehors du jeu ASCII, l'URL doit être convertie dans un format ASCII valide.
***
*/
// ************* EXPLICATION 4 ***********//
app.use(bodyParser.urlencoded({ extended: true }))






// ************* EXPLICATION 5 ***********//
/*
***
Importer le fichier flight_2015new dans la variable voyages
***
*/
// ************* EXPLICATION 5 ***********//
const voyages = require('./flight_2015new');




// ************* EXPLICATION 6 ***********//
/*
***
Initialiser une variable resultat a 404 not found***
*/
// ************* EXPLICATION 6 ***********//
var resultat = "<h1>404 not fund!</h1>"




// ************* EXPLICATION 6 ***********//
/*
***
Seveur en écoute sur le port 3000
*/

// ************* EXPLICATION 7 ***********//
app.listen(3000, function () {
console.log('listening on 3000')
})


/*
***
Définir une première route principale /
*/
// ************* EXPLICATION 8 ***********//
app.get('/', (req, res) => {
res.send('/index.html')
})


/*
***
Récupérer toutes les routes
*/
// ************* EXPLICATION 9 ***********//

// ************* EXPLICATION 9 ***********//
app.get('/voyages', (req, res) => {
resultat = voyages
res.send(resultat)
})



/*
***
Récupérer un voyage avec un id aléatoire
*/
// ************* EXPLICATION 10 ***********//

// ************* EXPLICATION 10 ***********//
app.get('/voyages/random', (req, res) => {
let id = Math.floor(Math.random() * voyages.length)
console.log(id);
resultat = voyages[id]
res.send(resultat)
resultat = "<h1>404 not found!</h1>"
})


/*
***
Récupérer un voyage avec un id spécifié par l'utilisateur
*/
// ************* EXPLICATION 10 ***********//


// ************* EXPLICATION 11 ***********//
app.get('/voyages/:id', (req, res) => {
if (req.params.id < voyages.length) {
resultat = voyages[req.params.id]
}
res.send(resultat)
resultat = "<h1>404 not found!</h1>"
})


/*
***
Récupérer un voyage avec un pays d'origine spécifié par l'utilisateur
*/
// ************* EXPLICATION 12 ***********//
app.get('/voyages/o/:pays', (req, res) => {
resultat = getListO(req.params.pays)
res.send(resultat)
resultat = "<h1>404 not fund!</h1>"
})


/*
***
Récupérer un voyage avec un pays de destination spécifié par l'utilisateur
*/

// ************* EXPLICATION 13 ***********//
app.get('/voyages/d/:pays', (req, res) => {
resultat = getListD(req.params.pays)
res.send(resultat)
resultat = "<h1>404 not fund!</h1>"
})


/*
***
Récupérer la liste de tous les voyages avec un pays d'origine paysO
*/

// ************* EXPLICATION 14 ***********//
const getListO = (paysO) => {
let listO = []
for (let i = 0; i < voyages.length; i++) {
if (voyages[i].ORIGIN_COUNTRY_NAME == paysO) {
listO.push(voyages[i])
}
}
return listO
}

/*
***
Récupérer la liste de tous les voyages avec un pays de destination paysD
*/

// ************* EXPLICATION 15 ***********//
const getListD = (paysD) => {
let listD = []
for (let i = 0; i < voyages.length; i++) {
if (voyages[i].DEST_COUNTRY_NAME == paysD) {
listD.push(voyages[i])
}
}
return listD
}


