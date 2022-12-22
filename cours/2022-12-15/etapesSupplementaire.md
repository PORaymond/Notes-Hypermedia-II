# Étapes supplémentaires

[Vidéo à partir de 15:18](https://crosemont.sharepoint.com/sites/msteams_0202a0/_layouts/15/stream.aspx?id=%2Fsites%2Fmsteams%5F0202a0%2FShared%20Documents%2FGeneral%2FRecordings%2FHYPERM%C3%89DIA%20II%2D20221215%5F095303%2DMeeting%20Recording%2Emp4&referrer=Teams%2ETEAMS%2DELECTRON&referrerScenario=teamsSdk%2DopenFilePreview)\
[Et la suite](https://crosemont.sharepoint.com/sites/msteams_0202a0/_layouts/15/stream.aspx?id=%2Fsites%2Fmsteams%5F0202a0%2FShared%20Documents%2FGeneral%2FRecordings%2FHYPERM%C3%89DIA%20II%2D20221215%5F101528%2DMeeting%20Recording%2Emp4&referrer=Teams%2ETEAMS%2DELECTRON&referrerScenario=teamsSdk%2DopenFilePreview)

## Connection a mongoDB Atlas
1. Se connecter à [mongoDB Atlas](https://account.mongodb.com/account/login?signedOut=true)
2. S’assurer d’avoir un cluster libre ou [en créer un nouveau](./creerUnNouveauClusterMongoDB.md)
3. Cliquer sur > *Connect*
4. \> *MongoDB Shell*
5. \> *I have the Mongosh installed*
6. Copier la chaine de connection
7. ouvrir cmd
8. Entrer la chaine de connection
9. Entrer votre mot de passe

## Nouvelle BDD
1. Créer une nouvelle bdd
    ```mongosh
    use star-wars-quotes;
    ```
2. Créer une nouvelle table
    ```mongosh
    db.createCollection('quotes');  
   ```
## Connecter notre application à mongoDB Atlas
1. Mettre la chaine de connection dans la variable d’environnement process.env ([procédure](process_env.md))
2. Dans server.js 
    ```javascript
    MongoClient.connect(connectionString, {useUnifiedTopology: true})
   .then(client =>{
      console.log('Connected to DB');
      const db = client.db('star-wars-quotes')
   }) 
    ```

