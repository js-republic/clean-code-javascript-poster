Ne pas mettre de commentaire à toutes les sauces
===

**Les commentaires sont des excuses**, pas un pré-requis. Un bon code se comprend de lui-même. Les commentaires doivent être présents uniquement pour expliquer 
une logique complexe (algorithme mathématique, etc) 

Mauvais :
```javascript 1.8
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
```javascript 1.8
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
###Les commentaires ne sont pas là non plus pour journaliser :
``` javascript
/**
 * 2016-12-20: Removed monads, didn't understand them (RM)
 * 2016-10-01: Improved using special monads (JP)
 * 2016-02-03: Removed type-checking (LI)
 * 2015-03-14: Added combine with type-checking (JR)
 */
```
###Pas pour découper des longs fichiers :
``` javascript
////////////////////////////////////////////////////////////////////////////////
// Scope Model Instantiation
////////////////////////////////////////////////////////////////////////////////
$scope.model = {
  menu: 'foo',
  nav: 'bar'
};
```
###Ni pour positioner la fin des blocs (trop) complexes :
``` javascript
while (toto < MAX_VALUES){
    if (test > MIN_VALUES){
    } // if
} // while
```




