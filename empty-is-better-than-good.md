Pas de code, c'est mieux qu'un beau code
===

Et oui, cela demandera toujours moins de travail de ne rien maintenir plutôt que maintenir un beau code. Ne gardez que les lignes utiles tout en gardant un code compréhensible et maintenable.

## Les commentaires sont des excuses

Pas un pré-requis. Un bon code se comprend de lui-même. Les commentaires doivent être présents uniquement pour expliquer 
une logique complexe (algorithme mathématique, etc) 

Mauvais :
```js
function hashIt(data) {
  // The hash
  let hash = 0;

  // Length of string
  const length = data.length;

  // Loop through every character in data
  for (let i = 0; i < length; i++) {
    // Get character code.
    const char = data.charCodeAt(i);
    // Make the hash
    hash = ((hash << 5) - hash) + char;
    // Convert to 32-bit integer
    hash &= hash;
  }
}
```

Bon :
```js
function hashIt(data) {
  let hash = 0;
  const length = data.length;

  for (let i = 0; i < length; i++) {
    const char = data.charCodeAt(i);
    // Make the hash
    hash = ((hash << 5) - hash) + char;
    // Convert to 32-bit integer
    hash &= hash;
  }
}
```
### Les commentaires ne sont pas là non plus pour journaliser :

Git marche beaucoup (beaucoup) mieux pour ça.

```js
/**
 * 2016-12-20: Removed monads, didn't understand them (RM)
 * 2016-10-01: Improved using special monads (JP)
 * 2016-02-03: Removed type-checking (LI)
 * 2015-03-14: Added combine with type-checking (JR)
 */
```
### Pas pour découper des longs fichiers :

Vos fonctions ne sont pas sensé être longues, ni vos fichiers et donc ne nécessitent pas de commentaire d'organisation.

```js
////////////////////////////////////////////////////////////////////////////////
// Scope Model Instantiation
////////////////////////////////////////////////////////////////////////////////
$scope.model = {
  menu: 'foo',
  nav: 'bar'
};
```
### Ni pour positioner la fin des blocs (trop) complexes :

Même principe, préférez scinder votre algorithme en sous-fonctions et par conséquant améliorer la lisibilité plutôt que commenter un grand bloque.

```js
while (toto < MAX_VALUES){
    if (test > MIN_VALUES){
    } // if
} // while
```

## Élaguez votre code

### Supprimez le code inutilisé

Aucune raison de conserver un code jamais appelé (même commenté), supprimez-le.
Vous pourrez toujours le retrouver dans votre outil de versionning.

Mauvais :

```js
function oldRequestModule(url) { /* ... */ }
function newRequestModule(url) { /* ... */ }

// inventoryTracker('apples', oldRequestModule, 'www.inventory-awesome.io');
inventoryTracker('apples', newRequestModule, 'www.inventory-awesome.io');
```

Bon :

```js
function newRequestModule(url) { /* ... */ }

inventoryTracker('apples', newRequestModule, 'www.inventory-awesome.io');
```

### Ne vous répétez pas

Chaque duplication de code entraîne plus de maintenance, plus de bugs et moins de
lisibilité. Refactorisez votre code afin d'améliorer vos lendemains !

Mauvais :

```js
function showDeveloperList(developers) {
  developers.forEach(developer => {
    render({
      expectedSalary: developer.calculateExpectedSalary(),
      githubLink: developer.getGithubLink(),
    });
  });
}

function showManagerList(managers) {
  managers.forEach(manager => {
    render({
      expectedSalary: manager.calculateExpectedSalary(),
      portfolio: manager.getMBAProjects(),
    });
  });
}
```

Bon :

```js
function showEmployeeList(employees) {
  employees.forEach(employee => {
    const portfolio = employee.type === 'manager'
      ? employee.getMBAProjects()
      : employee.getGithubLink();

    render({
      expectedSalary: employee.calculateExpectedSalary(),
      portfolio,
    });
  });
}
```
