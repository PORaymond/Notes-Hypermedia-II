
## Premières manipulations MongoDB avec mongosh## 
```mongosh
test> show dbs;
test> use formation;
formation> show dbs;
formation> db.etudiants.insert({"nom": "julien"});
formation> db.etudiants.insert({"nom": "houda"});
formation> show dbs;
formation> use formation;
formation> db.professeurs.insert({"nom": "claude"});
formation> db.professeurs.insert({"nom": "karim"});
formation> db.professeurs.insert({"nom": "haythem"});
formation> use college
college> db.createCollection("personnels");
college> db.personnels.insert({"nom":"Sylvain"});
college> db 
college> db.dropDatabase();
```

# Opérations CRUD
## C: CRÉATION ou INSERTION
college> use formation;

###### INSÉRER UN PREMIER DOCUMENT 
```mongosh

formation> db.professeurs.insert({ 
"name":"Maxime Gagnon", 
"birthday":ISODate("1990-10-10T09:00:00Z"), 
"adress":{ 
"street":"43 rue pointe aux trembles", 
"zipcode":"999", 
"city":"Montreal" 
},
"hobbies":["programmation","natation"]
});

formation> db.professeurs.insert({ "name":"Maxime Gagnon", "birthday":ISODate("1990-10-10T09:00:00Z"), "adress":{ "street":"43 rue pointe aux trembles", "zipcode":"999", "city":"Montreal"},"hobbies":["programmation","natation"]});
```
###### INSÉRER UN DEUXIÈME DOCUMENT 
formation> db.professeurs.insert({ 
"name":"Maxime Gagnon",  
"adress":{ 
"street":"11 rue PIE-IX", 
"zipcode":"888", 
"city":"Montreal" 
},
"hobbies":"cuisine"
});


# INSÉRER UN TROISIÈME DOCUMENT 
formation> db.professeurs.insert({ 
"name":"Robert Tremblay",  
"adress":{ 
"street":"13 rue PIE-IX", 
"zipcode":"111", 
"city":"Toronto" 
},
"hobbies":["dormir","jeux vidéo"]
});


# INSÉRER UN QUATRIÈME DOCUMENT 
formation> db.professeurs.insert({ 
"name":"Karim Benzema",  
"adress":{ 
"street":"18 rue PIE-IX", 
"zipcode":"666", 
"city":"Toronto" 
},
"hobbies":["dormir","soccer"]
});

# INSÉRER UN CINQUIÈME DOCUMENT 
formation> db.professeurs.insert({ 
"name":"Cristiano Ronaldo",  
"adress":{ 
"street":"20 rue Hochelaga", 
"zipcode":"666", 
"city":"Toronto" 
},
"hobbies":["dormir","soccer"]
});

# INSÉRER UN SIXIÈME DOCUMENT 
formation> db.professeurs.insert({ 
"name":"Thibaut Courtois",  
"adress":{ 
"street":"66 rue Hochelaga", 
"zipcode":"666", 
"city":"Toronto" 
},
"hobbies":["dormir","soccer"]
});



# INSÉRER UN SEPTIÈME DOCUMENT 
formation> db.professeurs.insert({ 
"name":"Marco Asensio",  
"adress":{ 
"street":"38 rue Hochelaga", 
"zipcode":"666", 
"city":"Toronto" 
},
"hobbies":["dormir","soccer"]
});

# INSÉRER UN Huitième DOCUMENT 
formation> db.professeurs.insert({ 
"name":"Toni Kroos",  
"adress":{ 
"street":"55 rue Laurier", 
"zipcode":"777", 
"city":"Vancouver" 
},
"hobbies":["dormir","soccer"]
});

# INSÉRER UN Neuvième DOCUMENT 
formation> db.professeurs.insert({ 
"name":"David Alaba",  
"adress":{ 
"street":"22 rue Laurier", 
"zipcode":"777", 
"city":"Vancouver" 
},
"hobbies":["dormir","soccer"]
});

# INSÉRER UN Dixème DOCUMENT 
formation> db.professeurs.insert({ 
"name":"Luca Modric",  
"adress":{ 
"street":"11 rue wellington", 
"zipcode":"111", 
"city":"Vancouver" 
},
"hobbies":["dormir","soccer"]
});

# INSÉRER UN Onzième DOCUMENT 
formation> db.professeurs.insert({ 
"name":"Frederico valverde",  
"adress":{ 
"street":"77 rue wellington", 
"zipcode":"111", 
"city":"Vancouver" 
},
"hobbies":["dormir","soccer"]
});

# INSÉRER UN Douzième DOCUMENT 
formation> db.professeurs.insert({ 
"name":"Eden Hazard",  
"adress":{ 
"street":"88 rue wellington", 
"zipcode":"666", 
"city":"Vancouver" 
},
"hobbies":["dormir","soccer"]
});

# INSÉRER UN Treizième DOCUMENT 
formation> db.professeurs.insert({ 
"name":"Vinicius Junior",  
"adress":{ 
"street":"99 rue wellington", 
"zipcode":"666", 
"city":"Vancouver" 
},
"hobbies":["dormir","soccer"]
});


# INSÉRER UN Quatorzième DOCUMENT 
formation> db.professeurs.insert({ 
"name":"Lucas Vazquez",  
"adress":{ 
"street":"16 rue PIE-IX", 
"zipcode":"888", 
"city":"Montreal" 
},
"hobbies":"cuisine"
});

# INSÉRER UN Quinzième DOCUMENT 
formation> db.professeurs.insert({ 
"name":"Luis Lopez",  
"adress":{ 
"street":"17 rue PIE-IX", 
"zipcode":"888", 
"city":"Montreal" 
},
"hobbies":"cuisine"
});


## R: RETREIVE ou AFFICHAGEformation>db.professeurs.find()


## U: UPDATE
```mongosh
formation>db.professeurs.update(
{"name": "Maxime Gagnon"},
{$set:{"adress.zipcode":444}}
)
```

## R: RETREIVE ou AFFICHAGE
```mongosh
formation>db.professeurs.find()
```

#	On ne peut pas modifier qu’un seul document 
# 	En effet :(C'est le premier dans les résultats de recherche)
# 	multi:true pour modifier plus de deux résultats

## U: UPDATE(Plusieurs)
db.professeurs.update(
{"name": "Maxime Gagnon"},
{$set:{"adress.zipcode":555}},
{multi:true}
)

## R: RETREIVE ou AFFICHAGEformation>db.professeurs.find()


## R: RETREIVE ou EFFECTUER UNE RECHERCHEformation>
```mongosh
db.professeurs.find()
formation>db.professeurs.find({"name": "Maxime Gagnon"})
formation>db.professeurs.find({"adress.zipcode":1111})
formation>db.professeurs.find({"city":"Montreal"})
formation>db.professeurs.find({"city":"Toronto"})
formation>db.professeurs.find({"city":"Vancouver"})
formation>db.professeurs.find({"hobbies":"dormir"})
formation>db.professeurs.find({"hobbies":"cuisine"})
formation>db.professeurs.find({"adress.zipcode":{$gt:222}})
formation>db.professeurs.find({"adress.zipcode":{$gt:222}, "name":"Karim Benzema"})
formation>db.professeurs.find({$or: [{"adress.zipcode":{$gt:222}}, {"name":"Robert Tremblay"}]})
formation>db.professeurs.find({$or: [{"hobbies":"dormir"}, {"name":"Maxime Gagnon"}]}).sort({"name":1})
formation>db.professeurs.find({$or: [{"hobbies":"dormir"}, {"name":"Maxime Gagnon"}]}).sort({"name":-1,"adress.zipcode":1})
formation>db.professeurs.find({$or: [{"hobbies":"dormir"}, {"name":"Maxime Gagnon"}]}).sort({"adress.zipcode":1,"name":-1})
formation>db.professeurs.find({$or: [{"hobbies":"dormir"}, {"name":"Maxime Gagnon"}]}).sort({"adress.zipcode":-1,"name":1})
formation>db.professeurs.find({$or: [{"hobbies":"dormir"}, {"name":"Robert Tremblay"}]}).limit(6)
formation>db.professeurs.find({$or: [{"hobbies":"dormir"}, {"name":"Robert Tremblay"}]}).limit(4)
formation>db.professeurs.find({$or: [{"hobbies":"dormir"}, {"name":"Robert Tremblay"}]}).limit(1)
formation>db.professeurs.find({$or: [{"hobbies":"dormir"}, {"name":"Robert Tremblay"}]}).sort({"adress.zipcode":1,"name":1}).limit(10)
formation>db.professeurs.find({$or: [{"hobbies":"dormir"}, {"name":"Robert Tremblay"}]}).sort({"adress.zipcode":1,"name":1}).limit(3)
formation>db.professeurs.find({$or: [{"hobbies":"dormir"}, {"name":"Robert Tremblay"}]}).sort({"adress.zipcode":1,"name":-1}).limit(3)
formation>db.professeurs.find({$or: [{"hobbies":"dormir"}, {"name":"Robert Tremblay"}]}).limit(1).skip(1)
formation>db.professeurs.find({$or: [{"hobbies":"dormir"}, {"name":"Robert Tremblay"}]}).limit(10).skip(2)
```



## D: DELETE ou EFFECTUER UNE SUPPRESSION
```mongosh
formation>db.professeurs.find({"hobbies":"cuisine"})
formation>db.professeurs.remove({"hobbies":"cuisine"})
formation>db.professeurs.find({"hobbies":"cuisine"})
formation>db.professeurs.find({"hobbies":"dormir"})
formation>db.professeurs.remove({"hobbies":"dormir"},{justOne:true})
formation>db.professeurs.find({"hobbies":"dormir"})
formation>db.professeurs.remove({})
formation>db.professeurs.find()
formation>show collections;
```
[Retour Mongo](../index.md)

[Retour Cours04](../../cours/2022-11-20-IntroMongo/Cours04.md)
