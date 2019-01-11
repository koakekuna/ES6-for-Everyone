[![](https://es6.io/images/ES62.png)](https://es6.io/)

# ES6 for Everyone

Hello! This repo is for tracking and documenting the lessons from Wes Bos's ES6 for Everyone course. I also include summaries of lessons learned after each topic.

## Module 1
- 3 way to declare variables: `var`, `const`, and `let`
  - `var` is *function* scoped, and could bleed into the global variables
  - `let` and `const` are *block* scoped, meaning they are always contained within a pair of curly braces
  - `let` variables can be redeclared, while `const` variables cannot be updated once declared
    - When declaring an object with `const`, the key value pairs can change, but the object itself cannot be redeclared
- temporal dead zone - variables created with `var` can be accessed before they're declared (although their value will be undefined) whereas variables created with `let` and `const` will throw an error
- best practices in the field
  - use `const` by default
  - only use `let` if rebinding is needed

## Module 2
- 3 main benefits
  - much more concise than regular functions
  - implicit returns, which allows nifty one liners
  - does not rebind the value of this when within another function
  ```js
  const names = ['mark', 'steve', 'ryan'];
  // Regular way
  const fullNames = names.map(function(name) {
    return `${name} smith`;
  });

  // Basic arrow function
  const fullNames2 = names.map((name) => {
    return `${name} smith`;
  });

  // No need for parenthesis if only one parameter
  const fullNames3 = names.map(name => {
    return `${name} smith`;
  });

  // Implicit return - one line no curly brackets
  const fullNames4 = names.map(name =>  `${name} smith`);

  // Empty parenthesis required when no arguments are passsed
  const fullNames5 = names.map(() =>  `John smith`);
  ```
- arrow functions are anonymous functions, but you can put them in a variable to name them
```js
const sayMyName = (name) => { alert(`Hello ${name}!`) };
sayMyName('Koa');
```
- return an object with arrow functions by wrapping in parenthesis
```js
const race = '100m Dash';
const winners = ['Hunter Gath', 'Singa Song', 'Imda Bos'];

const win = winners.map(winner, i => ({name: winner, race: race, place: i}) );
```
- the value of `this` within an arrow function is inherited from the parent scope, not the block
- default arguments can be set when defining the function
  - pass undefined if you want to skip an argument and use the default argument
```js
function calculateBill(total, tax = 0.13, tip = 0.15) {
  return total + (total * tax) + (total * tip);
}

const totalBill = calculateBill(100, undefined, 0.25);
```
- when not to use arrow functions
  - you really need `this`
  - you need a method to bind to an object
  - you need to add a prototype method
  - you need the arguments object

## Module 3