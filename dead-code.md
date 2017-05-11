# Élaguez votre code

### Supprimez le code inutilisé

Aucune raison de conserver une fonction si vous ne vous ne l'appelez jamais !
Débarrassez-vous-en, vous pourrez toujours la retrouver dans votre outil de versionning.
De la même façon, supprimez tout code commenté.

Mauvais :

```js
function oldRequestModule(url) {
  // ...
}

function newRequestModule(url) {
  // ...
}

// inventoryTracker('apples', oldRequestModule, 'www.inventory-awesome.io');
inventoryTracker('apples', newRequestModule, 'www.inventory-awesome.io');
```

Bon :

```js
function newRequestModule(url) {
  // ...
}

inventoryTracker('apples', newRequestModule, 'www.inventory-awesome.io');
```

### Ne vous répétez pas

Si vous avez dupliqué du code, vous pouvez certainement en refactoriser une partie
afin d'ajouter une couche d'abstraction. Ainsi, vous n'aurez par la suite jamais
besoin d'effectuer plusieurs fois les mêmes changements à différents endroits !

Mauvais :

```js
function showDeveloperList(developers) {
  developers.forEach((developer) => {
    const expectedSalary = developer.calculateExpectedSalary();
    const experience = developer.getExperience();
    const githubLink = developer.getGithubLink();

    const data = {
      expectedSalary,
      experience,
      githubLink,
    };

    render(data);
  });
}

function showManagerList(managers) {
  managers.forEach((manager) => {
    const expectedSalary = manager.calculateExpectedSalary();
    const experience = manager.getExperience();
    const portfolio = manager.getMBAProjects();

    const data = {
      expectedSalary,
      experience,
      portfolio,
    };

    render(data);
  });
}
```

Bon :

```js
function showEmployeeList(employees) {
  employees.forEach((employee) => {
    const expectedSalary = employee.calculateExpectedSalary();
    const experience = employee.getExperience();
    const portfolio = employee.type === 'manager'
      ? employee.getMBAProjects()
      : employee.getGithubLink();

    const data = {
      expectedSalary,
      experience,
      portfolio,
    };

    render(data);
  });
}
```
