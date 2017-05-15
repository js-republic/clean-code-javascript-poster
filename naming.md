Quel est mon nom ?
==

"There are only two hard things in Computer Science: cache invalidation and naming things."
-- Phil Karlton

"Programs are meant to be read by humans and only incidentally for computers to execute."
-- Donald Knuth

## Vous dites un bon nom ?

### Eloquent, Prononçable et Explicatif !

Mauvais:
```js
const yyyymmdstr = moment().format('YYYY/MM/DD');

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

### Si c'est le même type, c'est le même nom

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

### Pourquoi 525600 ?

Mauvais:
```js
if (m === 525600 ) makeACuriousThing()
```

Bon:
```js
const MINUTES_IN_A_YEAR = 525600;
if (minutes === MINUTES_IN_A_YEAR) makeACuriousThing()
```

### Une convention, et s'y tenir

```js
class AnimalSoSweet {}                 // UpperCamelCase

let anAnimal = new AnimalSoSweet();    // LowerCamelCase
function sendARequest(requestToSend){};// LowerCamelCase

const NB_MS_IN_HOUR = 3600;            // SCREAMING_SNAKE_CASE
// /app/models/mega-user.js            // kebab-case
```

### C'est logique de notre tête mais pas dans celles des autres

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

### Pas la peine de sur-contextualiser

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
### Soyez encore plus attentif avec les fonctions

```js
function addToDate(date, month) { }
const date = new Date();
addToDate(date, 1); // ça ajoute quoi ?
```

```js
function addMonthToDate(month, date) { }
const date = new Date();
addMonthToDate(1, date);
```