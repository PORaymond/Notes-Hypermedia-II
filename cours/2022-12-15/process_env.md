# Variable d’environnement
1. dans un terminal
    ```cmd
      npm install  dotenv --save
    ``` 
2. dans server.js
    ```javascript
    require('dotenv').config()
    ```
3. dans .gitignore
    ```.gitignore
    .env
    ```
4. Créer un fichier .env dans le projet. Dans ce fichier 
   ```javascript
   connectionString = connectionString = "mongodb+srv://<username>:<password>@<clustername>/<database_name>"
   ```
5. Dans server.js
   
   ```javascript
   const = connectionString = process.env.connectionSting;
   ```

On peut se servir de la valeur de `connnection String` au besoin 
[Référence](https://stackabuse.com/managing-environment-variables-in-node-js-with-dotenv/)
---
[Retour](etapesSupplementaire.md)
