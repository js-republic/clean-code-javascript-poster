Choisis chaque nom avec attention
==

En JavaScript, étant un langage avec un typage non-explicite faible, ne pas prendre un soin tout particulier à donner le meilleur nom à chaque élément, revient à se retirer la dernier moyen de comprendre ce qu'on manipule.

"Programs are meant to be read by humans and only incidentally for computers to execute."
-- Donald Knuth

## Un nom doit être éloquent, prononçable et explicatif !

Un bon nom doit retranscrire la sémantique de ce qu'il nomme, tout en restant prononçable et relativement compréhensible.

Mauvais:
```js
const yyyymmddstr = moment().format('YYYY/MM/DD');

const address = 'One Infinite Loop, Cupertino 95014';
const cityZipCodeRegex = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/;
saveCityZipCodeAndDate(address.match(cityZipCodeRegex)[1], address.match(cityZipCodeRegex)[2], yyyymmdstr);
```
Bon:
```js
const yearMonthDay = moment().format('YYYY/MM/DD');

const address = 'One Infinite Loop, Cupertino 95014';
const cityZipCodeRegex = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/;
const [, city, zipCode] = address.match(cityZipCodeRegex) || [];
saveCityZipCodeAndDate(city, zipCode, yearMonthDay);
```

## Si c'est le même type, c'est le même nom

Veillez à ce que partout dans votre code, un type soit nommé de la même façon.

Mauvais:
```js
getUserInfo();
getClientData();
getCustomerRecord();
```

Bon:
```js
getUser();
```

## Faite la guerre aux valeurs magiques

Une valeur arbitraire dans le code ne donne aucune information sur son identité.
Nommez là pour connaitre son utilité.

Mauvais:
```js
if (m === 525600 ) makeACuriousThing()
```

Bon:
```js
const MINUTES_IN_A_YEAR = 525600;
if (minutes === MINUTES_IN_A_YEAR) makeACuriousThing()
```

## Une convention, et s'y tenir

Le typage n'étant pas explicite en JavaScript, avoir une convention permet de rapidement comprendre ce qu'on manipule et facilite la lecture.

```js
class AnimalSoSweet {}                 // classe : UpperCamelCase

let anAnimal = new AnimalSoSweet();    // variable : LowerCamelCase
function sendARequest(requestToSend){};// fonction : LowerCamelCase

const NB_MS_IN_HOUR = 3600;            // constante : SCREAMING_SNAKE_CASE
// /app/models/mega-user.js            // fichiers : kebab-case (même les classes)
```

## C'est logique de notre tête mais pas dans celles des autres

Il peut paraitre des fois redondant et verbeux de nommer intégralement. Rappeler vous que cette redondance n'est pas explicite pour les autres.

Mauvais :
```js
const locations = ['Austin', 'New York', 'San Francisco'];
locations.forEach(l => {
  doStuff();
  doSomeOtherStuff();
  // ...
  // ...
  // ...
  // C'est quoi déjà 'l' ?
  dispatch(l);
});
```

Bon :
```js
const locations = ['Austin', 'New York', 'San Francisco'];
locations.forEach(location => {
  doStuff();
  doSomeOtherStuff();
  // ...
  // ...
  // ...
  dispatch(location);
});
```

## Pas la peine de sur-contextualiser

Même si un nom doit être entier, le contexte dans lequel il agit complète son identité. Il n'est pas la peine d'en remettre une couche.

Mauvais :
```js
const Car = {
  carMake: 'Honda',
  carModel: 'Accord',
  carColor: 'Blue'
};

function paintCar(car) {
  car.carColor = 'Red';
}
```

```js
const Car = {
  make: 'Honda',
  model: 'Accord',
  color: 'Blue'
};

function paintCar(car) {
  car.color = 'Red';
}
```
## Soyez encore plus attentif avec les fonctions

Là encore JavaScript complique la tâche en n'étant pas préaucupé par le nombre de variable attendu. La fonction nécessite dés lors un effort supplémentaire dans son nom.

Mauvais
```js
function addToDate(date, month) { }
const date = new Date();
addToDate(date, 1); // ça ajoute quoi ?
```
Bon
```js
function addMonthToDate(month, date) { }
const date = new Date();
addMonthToDate(1, date);
```
