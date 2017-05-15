Un peu d'algorithmique
==

## Sur-optimiser son code est inutile

Les optimisations de performance sont rarement des modifications qui améliore la lecture du code et sont déjà transformé par NodeJS ou le navigateur qui l'execute.
Inutile de faire des boucles inversées ou d'enregistrer la longueur du tableau.

Mauvais
```ecmascript 6
for (let i = arr.length; i >= 0; i--) {}
ou 
const length = arr.length;
for (let i=0; i < length; i++) {}
```

## Encapsuler le condition, pour leur donner un petit nom

Ca permet de savoir vraiment ce qu'on test et d'être facilement modifiable

Mauvais:
```ecmascript 6
if (fsm.state === 'fetching' && isEmpty(listNode)) {
  // ...
}
```
Bon:
```ecmascript 6
function shouldShowSpinner(fsm, listNode) {
  return fsm.state === 'fetching' && isEmpty(listNode);
}

if (shouldShowSpinner(fsmInstance, listNodeInstance)) {
  // ...
}
```

## Pour bien gérer l'asynchronisme, on peut 

### Utiliser les callback mais elles sont à éviter
```ecmascript 6
import { get } from 'request';
import { writeFile } from 'fs';

get('https://en.wikipedia.org/wiki/Robert_Cecil_Martin', (requestErr, response) => {
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

```ecmascript 6
import { get } from 'request';
import { writeFile } from 'fs';

get('https://en.wikipedia.org/wiki/Robert_Cecil_Martin')
  .then((response) => {
    return writeFile('article.html', response);
  })
  .then(() => {
    console.log('File written');
  })
  .catch((err) => {
    console.error(err);
  });
```

### Et même les Async/Await

```ecmascript 6
import { get } from 'request-promise';
import { writeFile } from 'fs-promise';

async function getCleanCodeArticle() {
  try {
    const response = await get('https://en.wikipedia.org/wiki/Robert_Cecil_Martin');
    await writeFile('article.html', response);
    console.log('File written');
  } catch(err) {
    console.error(err);
  }
}
```


