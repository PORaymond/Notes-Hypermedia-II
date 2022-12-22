# Pour faire fonctionner les projet de M. Rehouma
## Dans le package.json :
Changer ceci :
```json lines
"scripts" : {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  }
```
Pour ceci :
```json lines
"scripts": {
    "start": "react-scripts --openssl-legacy-provider start",
    "build": "react-scripts --openssl-legacy-provider build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  }
```
Cela permet d’utiliser de version antérieure de react-router, etc.

---
[Retour](reactRouter.md)
