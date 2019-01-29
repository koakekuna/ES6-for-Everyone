[![](https://es6.io/images/ES62.png)](https://es6.io/)

# ES6 for Everyone

Hello! This repo is for tracking and documenting the lessons from Wes Bos's ES6 for Everyone course. I also include summaries of lessons learned after each topic.

## Module 1 – New Variables – Creation, Updating, and Scoping
- 3 way to declare variables: `var`, `const`, and `let`
  - `var` is _function_ scoped, and could bleed into the global variables
  - `let` and `const` are _block_ scoped, meaning they are always contained within a pair of curly braces
  - `let` variables can be redeclared, while `const` variables cannot be updated once declared
    - When declaring an object with `const`, the key value pairs can change, but the object itself cannot be redeclared
- temporal dead zone - variables created with `var` can be accessed before they're declared (although their value will be undefined) whereas variables created with `let` and `const` will throw an error
- best practices in the field
  - use `const` by default
  - only use `let` if rebinding is needed

## Module 2 – Function Improvements: Arrows and Default Arguments
- 3 main benefits

  - much more concise than regular functions
  - implicit returns, which allows nifty one liners
  - does not rebind the value of this when within another function

  ```js
  const names = ["mark", "steve", "ryan"];
  // Regular way
  const fullNames = names.map(function(name) {
    return `${name} smith`;
  });

  // Basic arrow function
  const fullNames2 = names.map(name => {
    return `${name} smith`;
  });

  // No need for parenthesis if only one parameter
  const fullNames3 = names.map(name => {
    return `${name} smith`;
  });

  // Implicit return - one line no curly brackets
  const fullNames4 = names.map(name => `${name} smith`);

  // Empty parenthesis required when no arguments are passed
  const fullNames5 = names.map(() => `John smith`);
  ```

- arrow functions are anonymous functions, but you can put them in a variable to name them

```js
const sayMyName = name => {
  alert(`Hello ${name}!`);
};
sayMyName("Koa");
```

- return an object with arrow functions by wrapping in parenthesis

```js
const race = "100m Dash";
const winners = ["Hunter Gath", "Singa Song", "Imda Bos"];

const win = winners.map(winner, i => ({ name: winner, race: race, place: i }));
```

- the value of `this` within an arrow function is inherited from the parent scope, not the block
- default arguments can be set when defining the function
  - pass undefined if you want to skip an argument and use the default argument

```js
function calculateBill(total, tax = 0.13, tip = 0.15) {
  return total + total * tax + total * tip;
}

const totalBill = calculateBill(100, undefined, 0.25);
```

- when not to use arrow functions
  - you really need `this`
  - you need a method to bind to an object
  - you need to add a prototype method
  - you need the arguments object

## Module 3 – Template Strings
- use backticks to interpolate a string
```js
const name = "Snickers";
const sentence = `My dog's name is ${name}`;
```
- create HTML markup using template literals
```js
const dogs = [
  { name: 'Snickers', age: 2 },
  { name: 'Hugo', age: 8 },
  { name: 'Sunny', age: 1 }
];

const markup = `
  <ul class="dogs">
    ${dogs.map(dog => `<li>${dog.name} is ${dog.age * 7}</li>`).join('')}
  </ul>
`;
document.body.innerHTML = markup;
```
- use tagged template literals to run a custom function right in front of the template string. this allows us to build the string ourselves instead of letting the browser do it.
```js
// strings argument is an array containing the partial strings in-between the variables
// values are the variables and will always be one less than strings
function highlight(strings, ...values) {
  let str = '';
  strings.forEach((string, i) => {
    str += `${string} <span contenteditable class="h1">${values[i] || ''}</span>`;
  });
  return str;
}

const name = 'Snickers';
const age = 100;

const sentence = highlight`My dog's name is ${name} and he is ${age} years old;
document.body.innerHTML = sentence;
```

## Module 4 – Additional String Improvements
- 4 new methods:
  - `string.startsWith()`
  - `string.endsWith()`
  - `string.includes()`
  - `string.repeat()`
- startsWith and endsWith can accept a second parameter to specify the position to start the search
- case sensitive

## Module 5 – Destructuring
- extract data from objects and arrays into their own object
```js
const koa = {
  first: 'Koa',
  last: 'Kekuna',
  location: {
    country: 'USA',
    state; 'PA',
    zipcode: '19446'
  }
}
const { country, state, zipcode } = koa.location;

const details = ['Koa', 123, 'kekoaponolani.com'];
const [name, id, website] = details;
```
- easily swap variables
```js
let inRing = 'Hulk Hogan';
let onSide = 'The Rock';

[inRing, onSide] = [onSide, inRing];
```
- destructure functions by wrapping the arguments in curly braces as well as the parameters when calling the function to allow leaving some params out or switching the order
```js
  function convertCurrency(amount) {
    const converted = {
      USD: amount * 0.76,
      GPB: amount * 0.53,
      AUD: amount * 1.01,
      MEX: amount * 13.30
    };
    return converted;
  }

  // argument wrapped in curly braces, also set the object's default to be an empty object
  function tipCalc({ total = 100, tip = 0.15, tax = 0.13 } = {}) {
    return total + (tip * total) + (tax * total);
  }

  // parameters wrapped in curly braces and order is switched and some params are left out
  const bill = tipCalc({ tip: 0.20, total: 200 });
  console.log(bill);
```

## Module 6 Iterables and Looping
- the "for of" loop
  - combines the best of a regular for loop, forEach, and for in - cleaner syntax, can break or continue within the loop, and does not loop over the properties in a modified prototype
  - can use to loop over anything 'iterable' including `arguments` and NodeList
  ```js
  const cuts = ['Chuck', 'Brisket', 'Shank', 'Short Rib'];

  for (const [i, cut] of cuts.entries()) {
    console.log(`${cut} is the ${i + 1} item`);
  }
  ```
- since objects are not iterable, we can use a few different methods to loop over an object
  - object.entries() will be coming in ES2017
  - Object.keys(object), but might as well just use "for in" instead

## Module 7 An Array of Array Improvements
