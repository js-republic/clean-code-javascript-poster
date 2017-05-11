# Fonctions

### Une tâche par fonction

Une fonction ne doit réaliser qu'une seule tâche.

Mauvais :

```js
function emailClients(clients) {
  clients.forEach(client => {
    const clientRecord = database.lookup(client);
    if (clientRecord.isActive()) {
      email(client);
    }
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

### Au maximum deux arguments

Dans l'idéal, une fonction ne doit reçevoir que deux arguments au maximum.
Pour reçevoir plus d'arguments, utilisez le destructuring.

Mauvais :

```js
function createMenu(title, body, buttonText, cancellable) { /* ... */ }
```

Bon :

```js
function createMenu({ title, body, buttonText, cancellable }) { /* ... */ }

createMenu({
  title: 'Foo',
  body: 'Bar',
  buttonText: 'Baz',
  cancellable: true,
});
```

### N'utilisez pas de flag en tant qu'argument

Si votre fonction reçoit un flag, c'est qu'elle effectue plusieurs tâches.
Séparez votre code en plusieurs fonctions.

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

### Évitez les effets de bord

Une fonction ne doit ni modifier un argument reçu, ni modifier des
variables déclarés en dehors.

Mauvais :

```js
const addItemToCart = (cart, item) => {
  cart.push({ item, date: Date.now() });
};
```

Bon :

```js
const addItemToCart = (cart, item) => {
  return [...cart, { item, date: Date.now() }];
};
```

### Utilisez les valeurs par défaut des arguments

Mauvais :

```js
function createMicrobrewery(name) {
  const breweryName = name || 'Hipster Brew Co.';
}
```

Bon :

```js
function createMicrobrewery(breweryName = 'Hipster Brew Co.') { /* ... */ }
```

### Encapsulez les conditions

Encapsuler une condition complexe dans une fonction bien nomée permet
d'obtenir un code compréhensible dès la première lecture.

Mauvais :

```js
if (fsm.state === 'fetching' && isEmpty(listNode)) { /* ... */ }
```

Bon :

```js
function shouldShowSpinner(fsm, listNode) {
  return fsm.state === 'fetching' && isEmpty(listNode);
}

if (shouldShowSpinner(fsmInstance, listNodeInstance)) { /* ... */ }
```

### Priviligiez la programmation fonctionnelle

Mauvais :

```js
const programmerOutput = [
  { name: 'Uncle Bobby', linesOfCode: 500 },
  { name: 'Suzie Q', linesOfCode: 1500 },
  { name: 'Jimmy Gosling', linesOfCode: 150 },
  { name: 'Gracie Hopper', linesOfCode: 1000 },
];

let totalOutput = 0;

for (let i = 0; i < programmerOutput.length; i++) {
  totalOutput += programmerOutput[i].linesOfCode;
}
```

Bon :

```js
const INITIAL_VALUE = 0;

const totalOutput = programmerOutput
  .map((programmer) => programmer.linesOfCode)
  .reduce((acc, linesOfCode) => acc + linesOfCode, INITIAL_VALUE);
```

### N'ajoutez pas vos fonctions dans le scope global

Ajouter une méthode à un objet JavaScript natif est une mauvaise pratique.

Mauvais :

```js
Array.prototype.diff = function(comparisonArray) { /* ... */ }
```

Bon :

```js
class SuperArray extends Array {
  constructor(...args) {
    super(...args);
  }

  diff(comparisonArray) { /* ... */ }
}
```
