# Arrow Functions

There is a more modern simple/concise syntax for creating functions, that's often better than function expressions.

It's called `arrow functions`. They look like this:

```javascript
let func = (arg1, arg2, ...argN) => expression;
```

it's a shorter version of:

```javascript
let func = function (arg1, arg2, ...argN) {
  return expression;
};
```

Here's a concrete comparison:

```javascript
let sum (a, b) => a + b;

let sum = function(a, b){
  return a + b;
}
```

The expression was evaluated and returned, there is no need to have a return statement.

## Other Nuances

- If we have only a single argument, then the parenthesis around the argument can be removed: `let double = n => n * 2`
- If there is no argument, the parenthesis will be empty but still must be included: `let sayHi = () => alert("Hello")`

You can dynamically create functions, just like with function expressions:

```javascript
let age = prompt("What is your age?", 18);

let welcome = age < 18 ? () => alert("Hello") : () => alert("Greetings!");

welcome();
```

## Multiline Arrow Functions

If we use curly braces then we need an explicit return statement.

```javascript
let sum = (a, b) => {
  let result = a + b;
  return result;
};
```
