# Élaguez votre code

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
