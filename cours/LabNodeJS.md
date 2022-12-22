# Lab Node.js
Créer une application CRUD simple avec Node, Express et MongoDB
Référence : https://zellwk.com/blog/crud-express-mongodb/
***

## 1 Introduction

Stack MERN = front end + back end

Mongo (BDD côté serveur) \
Express (Serveur) \
React (JS côté client) \
Node.js (JS côté serveur) 
***
## 2 Node 
1. Exécutons :
   ```
   node -v 
   npm -v 
   npm init ⇒ package.json 
   ```
2. Nous créons un fichier server.js.
3. server.js :
   ```Node.js
   console.log('May Node be with you')
   ```
4. Nous exécutons avec : 
   ```
   node server.js
   ```


***
## 3 Installation des dépendances


1. Exécutez ces commandes :
   ```npm
   npm install express --save 
   ```
   ```
   npm install nodemon --save-dev 
   ```
   ```
   npm install body-parser --save 
   ```
   ```
   npm install mongodb --save
   ```
   ```
   npm install ejs --save
   ```
   - Express est un serveur
   - Nodemon nous évite de rafraîchir le serveur (nous utiliserons la commande npm run dev au lieu de node server.js) 
   - "body-parser" est un middleware (application intermédiaire). Il est responsable de l'analyse des corps de requête entrants dans un middleware avant de le gérer. 
   - Mongodb est notre base de données. 
   - Ejs est un langage de modèles qui permet de générer du html.
   - Vérifiez qu’ils sont installés dans *package.json* 
   
     - Middleware
     : (ou intergiciel en français) logiciel qui agit comme passerelle entre les autres applications, outils et bases de données pour offrir aux utilisateurs des services unifiés.
     
2. Utiliser nodemon au lieu de node. 

   Ajouter cette ligne dans package.json sous la clé scripts. 
   ```
   "dev" : "nodemon server.js"
   ```
   Ensuite tester avec : 
   ```
   npm run dev 
   ```
***
## 4 Travailler avec le routing côté serveur

1. Nous modifions server.js en ajoutant ces lignes de code :
   ```javascript
   const express = require('express');
   const app = express();
   
   app.listen(3000, function() {
   console.log('listening on 3000')
   })
   
   
   app.get('/', function(req, res) {
   res.send('Hello World')
   })
   
   
   app.get('/college', function(req, res) {
   res.send('Hello College')
   })
   
   app.get('/qui-sommes-nous', function(req, res) {
   res.send('Nous sommes des experts nodejs')
   })
   ```
2. Nous modifions encore une fois server.js en ajoutant ces lignes de code : 
   ```javascript
   const express = require('express');
   const app = express();
   
   app.listen(3000, function() {
   console.log('listening on 3000')
   })
   
   
   app.get('/', (req, res) => {
   res.sendFile(__dirname + '/index.html')
   })
   
   app.get('/page1', (req, res) => {
   res.sendFile(__dirname + '/page1.html')
   })
   
   app.get('/page2', (req, res) => {
   res.sendFile(__dirname + '/page2.html')
   })
   ```
   *Nous effaçons l'ancien contenu et nous créons deux pages index.html et page1.html et page2.html*
3. Ajout des pages page1.html et page2.html \
*page1.html version 1*
   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
     <meta charset="UTF-8">
     <title>Page 1</title>
   </head>
   <body>
       <h1>Page 1</h1>
   </body>
   </html>
   ```
   *page2.html version 1*
   
   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
     <meta charset="UTF-8">
     <title>PAGE 2</title>
   </head>
   <body>
     <h1>PAGE 2</h1>
   </body>
   </html>
   ```
***
## 5 Ajout du body-parser - réponse json

1. Ajoutons body-parser dans server.js
   ```javascript
   const express = require('express')
   const bodyParser= require('body-parser')
   const app = express()
   ```
   Il faut ajouter body-parser avant les CRUD handlers (GET, POST, PUT, DELETE)!
   ```javascript
   app.use(bodyParser.urlencoded({ extended: true }))
   ```

   LES CRUD handlers sont ajoutés de cette façon ...
   ```javascript
   app.get('/', (req, res) => {/*...*/})
   app.post('/quotes', (req, res) => {/*...*/})
   ```
2. Modifions index.html tel que suit :
   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
       <meta charset="UTF-8">
       <title>MY APP</title>
   </head>
   
   <body>
       <h1> May Node and Express be with you. </h1>
       <form action="/quotes" method="POST">
           <input type="text" placeholder="name" name="name">
           <input type="text" placeholder="quote" name="quote">
           <button type="submit">Submit</button>
       </form>
   </body>
   
   </html>
   ```
3. Ajoutons ce code à server.js :   
   ```javascript
   app.post('/quotes', (req, res) => {console.log('Hellooooooooooooooooo!')})
   ```
4. Testez
   ```
   npm run dev
   ```
   Ensuite saisir : 
   ```
   http://localhost:3000/
   ```
   Cliquez sur le bouton submit, il va afficher hellooooooooooooo sur la console. 
5. Un autre test avec GET ??? \
   Ajoutez ce code dans server.js
   ```javascript
   app.get('/testget', (req, res) => {
      res.sendFile(__dirname + '/raniapage.html')
   })
   ```
   Allez dans index.html et modifiez le formulaire
   ```html
   <body>
       <h1> May Node and Express be with you. </h1>
       <form action="/testget" method="GET">
           <input type="text" placeholder="name" name="name">
           <input type="text" placeholder="quote" name="quote">
           <button type="submit">Submit</button>
       </form>
   </body>
   ``` 
   Évaluation formative : différence entre res.send et res.sendFile
6. On revient à POST ? \
   Effacer l'ancien code du 5.4 et revenir à l'étape 5.3
   *server.js*
   ```javascript
   app.post('/quotes', (req, res) => {
   console.log('Hellooooooooooooooooo!')
   })
   ```
   *index.html*
   ```html
    <form action="/quotes" method="POST">
        <input type="text" placeholder="name" name="name">
        <input type="text" placeholder="quote" name="quote">
        <button type="submit">Submit</button>
    </form>
   ```
***
## 6 Transformer la saisie utilisateur dans le formulaire en json
1. Ajoutez ce code dans server.js
   ```javascript
   const express = require('express');
   const bodyParser= require('body-parser')
   const app = express();
   
   app.use(bodyParser.urlencoded({ extended: true }))
   ```
2. Supprimer ce code dans server.js
   ```javascript
   app.post('/quotes', (req, res) => {console.log('Hellooooooooooooooooo!')})
   ```
3. Le remplacer par ce code
   ```javascript
   app.post('/quotes', (req, res) => {console.log(req.body)})
   ```
4. Tester \
   Remplir le formulaire pour avoir la requête \
   Cliquez sur submit \
   Observez la console !!!


[Retour à l’index du cours](../README.md)
