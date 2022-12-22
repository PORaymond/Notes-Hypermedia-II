# Application avec Semantic-ui

Semantic ui
: Une librairie css 

## Installer semantic ui React 


```cmd
 npx create-react-app demo2
 cd demo2
 npm start
```
Ouvrir votre application demo2  \
Dans App.js supprimer la ligne 7 à 20
Remplacer ce code par
```html
<h1> Bonjour groupe ! Nous allons apprendre SEMANTIC UI</h1>
```

installer semantic ui REACT
``` cmd
npm install semantic-ui-react semantic-ui-css
```
Ouvrir le fichier package.json et observez

Ces deux dépendances ont été ajoutées
```
"semantic-ui-css": "^2.5.0",
"semantic-ui-react": "^2.1.3",
```
---
## Semantic ui React ajouter cdn 
Dans _public/index.html_ (avant la fermeture de la balise `</head>`,
(ligne 28 dans index.html) ajoutez cette ligne :
```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/2.3.1/semantic.min.css">
```
---

## UN PEU DE STYLE AVEC CSS
Supprimer le code dans votre fichier App.css
Remplacer le par celui-ci ci-bas :
```css
body {
  margin:0;
  padding:0;
  font-family: sans-serif;
  background: #d3d3d3;
  text-align: center;
}
.app{
  width: 920px;
  margin: 0 auto;
}
```

---

# Appeler le composant Recherche
Allez dans App.js et appelez le composant Recherche dans le return

Votre App.js devient comme suit :
```javascript
import './App.css';
import Recherche from './Recherche';

function App() {
  return (
    <div className="App">
    <h1> Bonjour groupe ! Nous allons apprendre SEMANTIC UI</h1>
   <Recherche/>
   </div>
  );
}

export default App;
```


Pour résumer, index.js appelle le composant App.js

Et le composant App.js appelle le composant Recherche.js

---


# Une vraie barre de Recherche

Remplacez le code dans Recherche.js par le suivant 

Copier et coller le code suivant :
```javascript
import { Component } from "react";
class Recherche extends Component {
render(){

        const optionsDpt = [
            { value: "44", key: "44", text:"Loire Atlantique"},
            { value: "49", key: "49", text:"Maine et Loire"},
            { value: "53", key: "53", text:"Mayenne"},
            { value: "72", key: "72", text:"Sarthe"},
            { value: "85", key: "85", text:"Vendée"},
        ];
 
     
        const optionsType = [
            { value: "cpam", key:"cpam", text: "Caisse primaire d'assurance maladie"},
            { value: "cci", key:"cci", text: "Chambre de commerce et d'industrie"},
            { value: "crous", key:"crous", text: "Crous et ses antennes"}
        ]
 
        
        return(
            <div className="recherche">
                <Select placeholder="Choisissez un département" options={optionsDpt}  />
                <Select placeholder="Choisissez une administration"  options={optionsType}  />
                <Button primary> Lancer la recherche </Button>
                <Button secondary> Vider la recherche </Button>
 
            </div>
        )
    }
}
export default Recherche;
```
#2 vous allez remarquer en enregistrant votre travail qu'une erreur soit générée
C'est parce que `<Button>` et `<Select>` n'ont pas leur `import`
Il faut simplement ajouter les imports de cette manière
Faites une saisie partielle `<But` et laissez le plugin effectuer
l'auto-complete, ce qui importera les dépendances rapidement
et automatiquement. Voici ce qui va être ajouté :
``` javascript
import { Button, Select } from "semantic-ui-react";
```

App.js
```javascript
import './App.css';
import Recherche from './Recherche';

  function App() {
    return (
      <div className="App">
      <h1> Bonjour groupe ! Nous allons apprendre SEMANTIC UI</h1>
      <Recherche/>
      </div>
  );
}

export default App;
```

---
# Ajoutez de la dynamicité (states)

On ajoute state ici :
```javascript
class Recherche extends Component {
   state ={
      depart: "", categorie:""
   }
   
}
```

On ajoute l'attribut value dans  les composants de Semantic UI React `<Select>` :
```javascript
  <Select placeholder="Choisissez un département" options={optionsDpt} value={this.state.depart}  />
  <Select placeholder="Choisissez une administration"  options={optionsType} value={this.state.categorie}  />
```
Nous remarquons qu'aucun élément n'a été modifié
 Nous allons associer des fonctions qui nous permettront de
Changer l'état en fonction de la selection de l'utilisateur
Première fonction
onDepartementChange ()

Deuxième fonction
onCategorieChange ()

Voici les implémentations:

onDepartementChange = (e,data) => { this.setState({depart:data.value})}
onCategorieChange = (e,data) => {this.setState({categorie:data.value})}

Ensuite, ajoutez dans nos 2 composants Select ces fonctions
dans l'événement associé au composant Select
Un bouton (événement je clique) ==> onClick =
Un select (je change de sélection) ==> onChange = {this.onDepartementChange}


Ajoutez un console.log à l'intérieur de la fonction render(){}
Pour afficher les états (depart et categorie) qui changent !!!
```
render(){
   console.log(this.state.depart, this.state.categorie)
}
```

Le code final de Recherche.js:

```javascript
import { Component } from "react";
import { Button, Select } from "semantic-ui-react";

class Recherche extends Component {

state ={ depart: "", categorie:""}


onDepartementChange = (e,data) => { this.setState({depart:data.value})}
onCategorieChange = (e,data) => {this.setState({categorie:data.value})}


    render(){
      
        console.log(this.state.depart, this.state.categorie)

        const optionsDpt = [
            { value: "44", key: "44", text:"Loire Atlantique"},
            { value: "49", key: "49", text:"Maine et Loire"},
            { value: "53", key: "53", text:"Mayenne"},
            { value: "72", key: "72", text:"Sarthe"},
            { value: "85", key: "85", text:"Vendée"},
        ];
 
     
        const optionsType = [
            { value: "cpam", key:"cpam", text: "Caisse primaire d'assurance maladie"},
            { value: "cci", key:"cci", text: "Chambre de commerce et d'industrie"},
            { value: "crous", key:"crous", text: "Crous et ses antennes"}
        ]
 
        
        return(
            <div className="recherche">
                <Select placeholder="Choisissez un département" options={optionsDpt} value={this.state.depart}  onChange={this.onDepartementChange} />
                <Select placeholder="Choisissez une administration"  options={optionsType} value={this.state.categorie}  onChange={this.onCategorieChange} />
                <Button primary> Lancer la recherche </Button>
                <Button secondary> Vider la recherche </Button>
                
            </div>
        )
    }
}
export default Recherche;

```
[Retour](../README.md)
