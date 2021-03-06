Un peu d'algorithmique
==

Les algorithmes on nous apprend surtout à en faire des performants, mais pas forcément comment bien les utilisés ou les organiser.

## Sur-optimiser son code est inutile

Les optimisations de performance sont rarement des modifications qui améliorent la lecture du code. A noté que NodeJS ou le navigateur fait déjà bon nombre d'optimisation par eux-même.
Inutile de faire des boucles inversées ou d'enregistrer la longueur du tableau donc.

Mauvais
```js
for (let i = arr.length; i >= 0; i--) {}
ou 
const length = arr.length;
for (let i=0; i < length; i++) {}
```

## Encapsuler les conditions, pour leur donner un petit nom

Cela permet de savoir vraiment ce qu'on test dans la condition et d'être facilement modifiable.

Mauvais:
```js
if (fsm.state === 'fetching' && isEmpty(listNode)) {
  // ...
}
```
Bon:
```js
function shouldShowSpinner(fsm, listNode) {
  return fsm.state === 'fetching' && isEmpty(listNode);
}

if (shouldShowSpinner(fsmInstance, listNodeInstance)) {
  // ...
}
```

## Préférez le polymorphisme à trop de condition

Mauvais
```js
class TrainCustomer {
  getDiscount (){
    if (this.age < 25)                      return this.age * 0.9;
    else if (this.type === 'trainEmployee') return 30;
    else if (this.hasCard)                  return 10;
    /* ... lot of conditions */
  }
}
```

Good
```js
class TrainCustomer { /*...*/ }

class YoungCustomer extends TrainCustomer {
  getDiscount () { return this.age * 0.9; }
}
class TrainEmployeeCustomer extends TrainCustomer {
  getDiscount () { return 30; }
}
class CardHolderCustomer extends TrainCustomer {
  getDiscount () { return 10; }
}
```


## Pour bien gérer l'asynchronisme, on peut 

### Utiliser les callback

Mais elles sont à éviter car elles sont trop verbeuses et pas assez puissantes pour gérer tous les cas.

Bad
```js
import { get } from 'request';
import { writeFile } from 'fs';

get('https://goo.gl/FxyZ7i', (requestErr, response) => {
  if (requestErr) {
    console.error(requestErr);
  } else {
    writeFile('article.html', response.body, (writeErr) => {
      if (writeErr) {
        console.error(writeErr);
      } else {
        console.log('File written');
      }
    });
  }
});
```      
### Préférer les Promesses

Standard actuel, plus élégantes mais améliorables, notament sur la gestion d'erreur :
`.catch` vs `try/catch`

Better
```js
import { get } from 'request';
import { writeFile } from 'fs';

get('https://goo.gl/FxyZ7i')
  .then(response => writeFile('article.html', response)))
  .then(() => console.log('File written'))
  .catch(err => console.error(err));
```

### Et même les Async/Await

Les Async/Await (définie en ES2017 et présents en NodeJS) permettent d'écrire l'asynchrone de façon synchrone, donnant ainsi une voie commune de gestion d'erreur et d'accumulation de donnée.

Best
```js
import { get } from 'request-promise';
import { writeFile } from 'fs-promise';

async function getCleanCodeArticle() {
  try {
    const response = await get('https://goo.gl/FxyZ7i');
    await writeFile('article.html', response);
    console.log('File written');
  } catch(err) {
    console.error(err);
  }
}
```


