# MongoDB
## Utiliser mongosh
Dans cmd : 

```cmd
mongosh
```

## Base de données

### Afficher toutes les bases de données

```mongosh
show dbs;
```

### Base de données courante

```mongosh
db;
```

### Créer une nouvelle base de données

```mongosh
use <nom de la nouvelle base de donnée>
```

### Supprimer une base de données

```mongosh
db.dropDatabase();
```

## Collections

### Créer une nouvelle collection 
Une collection est créée lorsqu’on déclare l’insertion d’un nouvel enregistrement : 

```mongosh
db.<Nom de la nouvelle collection>.insert(<Nouvel enregistrement>);
```

Mais on peut aussi la créer de façon explicite : 

```mongosh
db.createCollection(<Nom de la nouvelle collection>)
```

### Montrer les *collections* faisant partie de la db
``` mongosh
show collections;
```


## Documents

### Insérer un document (create)

```
db.<Nom de la collection>.insertOne(<Document>)
```
### Lister les documents d’une *collection*

```
db. <nom de la table>.find();
```

Exemple: la db est formation et a une *collection* "professeurs"
```
use formation; 
db.professeurs.find(); 
```

### Chercher les documents correspondants à un filtre (retrieve)

```db.< Nom de la collection >.find(< Filtre au format json >);```

Exemple : chercher les professeurs dont le zipcode est 444

```db.professeurs.find({"zipcode": 444});```

### Mettre à jour un document
```
db.< Collection >.updateOne(< Filtre (json) >, $set< mise à jour(json) >)
```
Remarque : Seul le premier match de cette requête sera changé

Exemple:

```
 db.professeurs.update({"name":"Maxime Gagnon"}, {$set:{"adress.zipcode": 124}});```
```

Pour changer tous les matches :
```
db.<Collection>.update(<Filtre(json)>, {$set :<mise à jour(json)>}, {multi:true});
```

Exemple:

```
db.professeurs.update( {"name": "Maxime Gagnon"}, {$set:{"adress.zipcode":555}}, {multi:true});
```

### Retirer un document
~~```db.<Collection>.remove(<Filtre(json)>, {justOne: true})```~~ obsolète

Exemple:

```mongosh
db.professeurs.deleteOne({"hobbies":"dormir"});
```

[Retour à l’index du cours](../../Index.md)

