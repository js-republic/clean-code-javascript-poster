# La fonction parfaite

### Ne doit réaliser qu'une seule tâche.

Mauvais :
```ecmascript 6
function emailClients(clients) {
  clients.forEach(client => {
    const clientRecord = database.lookup(client);
    if (clientRecord.isActive()) { email(client); }
  });
}
```

Bon :
```ecmascript 6
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

Mauvais :
```ecmascript 6
function createMenu(title, body, buttonText, cancellable) { /* ... */ }
```

Bon :
```ecmascript 6
function createMenu(menuConfig) { /* ... */ }
const menuConfig = { title: 'Foo', body: 'Bar', buttonText: 'Baz', cancellable: true };
createMenu(menuConfig);
```

#### Dont aucun n'est un flag

Si votre fonction reçoit un flag, c'est qu'elle effectue plusieurs tâches.

Mauvais :
```ecmascript 6
function createFile(name, temp) {
  if (temp) {
    fs.create(`./temp/${name}`);
  } else {
    fs.create(name);
  }
}
```

Bon :
```ecmascript 6
function createFile(name) {
  fs.create(name);
}

function createTempFile(name) {
  createFile(`./temp/${name}`);
}
```

### Manier le destructuring comme des paramètres nommés

Bon :
```ecmascript 6
function createMenu({title, body, buttonText, cancellable = true}) { /* ... */ }

createMenu({ title: 'Foo', body: 'Bar', buttonText: 'Baz'});
```

### Ne dois pas avoir d'effet de bord

Une fonction ne doit pas modifier un argument reçu ou une variable extérieure.

Mauvais :
```ecmascript 6
const addItemToCart = (cart, item) => cart.push({ item, date: Date.now() });
```

Bon :
```ecmascript 6
const addItemToCart = (cart, item) => [...cart, { item, date: Date.now() }];
```

### Préférer les valeurs par défaut des arguments

Mauvais :
```ecmascript 6
function createMicrobrewery(name) {
  const breweryName = name || 'Hipster Brew Co.';
}
```

Bon :
```ecmascript 6
function createMicrobrewery(breweryName = 'Hipster Brew Co.') { /* ... */ }
```

### Aimer la programmation fonctionnelle

Mauvais :
```ecmascript 6
const programmerOutput = [
  { name: 'Uncle Bobby', linesOfCode: 500 },
  { name: 'Suzie Q', linesOfCode: 1500 },
  { name: 'Jimmy Gosling', linesOfCode: 150 },
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
```ecmascript 6
const INITIAL_VALUE = 0;
const getTotalLineOfCode = () => 
  programmerOutput
     .map(programmer => programmer.linesOfCode)
     .reduce((acc, linesOfCode) => acc + linesOfCode, INITIAL_VALUE);
}
```
