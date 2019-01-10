[![](https://es6.io/images/ES62.png)](https://es6.io/)

# ES6 for Everyone

Hello! This repo is for tracking and documenting the lessons from Wes Bos's ES6 for Everyone course. I also include summaries of lessons learned after each topic.

# Module 1
- 3 way to declare variables: `var`, `const`, and `let`
  - `var` is *function* scoped, and could bleed into the global variables
  - `let` and `const` are *block* scoped, meaning they are always contained within a pair of curly braces
  - `let` variables can be redeclared, while `const` variables cannot be updated once declared
    - When declaring an object with `const`, the key value pairs can change, but the object itself cannot be redeclared
- temporal dead zone - variables created with `var` can be accessed before they're declared (although their value will be undefined) whereas variables created with `let` and `const` will throw an error
- best practices in the field
  - use `const` by default
  - only use `let` if rebinding is needed

# Module 2
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
```


