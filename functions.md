# La fonction parfaite

Element de base en JavaScript, prenez grand soin de vos fonctions, ce sont les fondations d'un projet robuste. 

### Ne doit réaliser qu'une seule tâche.

Cela limite les incrompréhensions et améliore la composabilité des fonctions (cf. programmation fonctionnelle)

Mauvais :
```js
function emailClients(clients) {
  clients.forEach(client => {
    const clientRecord = database.lookup(client);
    if (clientRecord.isActive()) { email(client); }
  });
}
```

Bon :
```js
function emailClients(clients) {
  clients
    .filter(isClientActive)
    .forEach(email);
}

function isClientActive(client) {
  const clientRecord = database.lookup(client);
  return clientRecord.isActive();
}
```

### Idéalement, ne recevoir que deux arguments maximum.

Un nombre réduit d'argument rend plus simple l'utilisation de la fonction et réduit
la combinatoire de test.

Mauvais :
```js
function createMenu(title, body, buttonText, cancellable) { /* ... */ }
```

Bon :
```js
function createMenu(menuConfig) { /* ... */ }
const menuConfig = { title: 'Foo', body: 'Bar', buttonText: 'Baz', cancellable: true };
createMenu(menuConfig);
```

#### Dont aucun n'est un flag

Si votre fonction reçoit un flag, c'est qu'elle effectue plusieurs tâches.

Mauvais :
```js
function createFile(name, temp) {
  if (temp) {
    fs.create(`./temp/${name}`);
  } else {
    fs.create(name);
  }
}
```

Bon :
```js
function createFile(name) {
  fs.create(name);
}

function createTempFile(name) {
  createFile(`./temp/${name}`);
}
```

### Manier le destructuring comme des paramètres nommés

On connait ainsi le rôle de chaque paramètre, les mettres dans l'ordre que l'on veut et même en "ignorer" certains.

Bon :
```js
function createMenu({title, body, buttonText, cancellable = true}) { /* ... */ }

createMenu({ title: 'Foo', body: 'Bar', buttonText: 'Baz'});
```

### Ne dois pas avoir d'effet de bord

Une fonction ne doit pas modifier un argument reçu ou une variable extérieure car cela nuit à sa composabilité.

Mauvais :
```js
const addItemToCart = (cart, item) => cart.push({ item, date: Date.now() });
```

Bon :
```js
const addItemToCart = (cart, item) => [...cart, { item, date: Date.now() }];
```

### Aimer la programmation fonctionnelle

JavaScript le facilite, préférez la programmation fonctionelle à la programmtion impérative. Elle est plus élégante et facile à tester. 

Mauvais :
```js
const programmerOutput = [
  { name: 'Uncle Bobby', linesOfCode: 500 },
  { name: 'Gracie Hopper', linesOfCode: 1000 },
];

const getTotalLineOfCode = () => {
  let totalOutput = 0;
  for (let i = 0; i < programmerOutput.length; i++) {
    totalOutput += programmerOutput[i].linesOfCode;
  }
  return totalOutput;
}
```

Bon :
```js
const INITIAL_VALUE = 0;
const getTotalLineOfCode = () => 
  programmerOutput
     .map(programmer => programmer.linesOfCode)
     .reduce((acc, linesOfCode) => acc + linesOfCode, INITIAL_VALUE);
}
```
### Et ne doit pas être placé en global !

Car cela entrainera beaucoup d'effet de bord innattendu.

Mauvais :
```js
Array.prototype.diff = function diff(comparisonArray) {
  const hash = new Set(comparisonArray);
  return this.filter(elem => !hash.has(elem));
};
```

Bon :
```js
class SuperArray extends Array {
  diff(comparisonArray) {
    const hash = new Set(comparisonArray);
    return this.filter(elem => !hash.has(elem));
  }
}

```
