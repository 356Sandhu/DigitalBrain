# Functions

Allow code to be called many times without repetition.

- building blocks of the program.
- `alert(message)`, `prompt(message, default)`, `confirm(question)` are examples of functions that are already built into javascript. But we can also create our own.

## Function Declaration

To create a function we can use a function declaration

```javascript
function showMessage() {
  alert("Hello Everyone!");
}
```

The `function` keyword goes first, then goes the name of the function, then a list of parameters between the parenthesis (comma-seperation, empty in our case) and finally the code of the function (body) goes between the curly braces.

```javascript
function name(parameters) {
  //...body...
}
```

Our functions can be called by their names: `showMessage()`

```javascript
function showMessage() {
  alert("Hello Everyone!");
}

showMessage();
showMessage();
```

The call `showMessage()` executes the code of the function. Here we will see the message two times.

This example demonstrates one of the main reasons to use functions, which is to avoid code duplication. Otherwise, we would've had to write the `console.log()` everytime we wanted to print our greeting.

## Local Variables

A variable that is declared inside a function is only visible inside of the function. For example:

```javascript
function showMessage() {
  let message = "Hello, I'm JavaScript!"; // Local Variable

  alert(message);
}

showMessage(); // Hello, I'm JavaScript

alert(message); // ERROR! The variable is local to the above function, therefore we can't access it here. To this function, it's as if it doesn't even exist.
```

Local variables are destroyed when the function ends.

## Outer Variables

A function can access outer variables and modify them as well.

for instance:

```javascript
let userName = "John";

function showMessage() {
  userName = "Bob"; // (1) changed the outer variable

  let message = "Hello, " + userName;
  alert(message);
}

alert(userName); // John, as it's called before the function
showMessage(); // Hello Bob
alert(userName); // Bob, as the showMessage() function changed the outer variable.
```

Outer variables are only used if a local one with that name doesn't exist, and an outer one does. If a local variable with the name does exist, then it will be the one the function deals with.

### Global Variables

Variables declared outside of any function are considered to be global variables.

Global Variables are visible from any function (unless shadowed by locals with the same names)

It's good practice to minimize the use of global variables. Modern code has few or no global variables at all. However, sometimes they can be useful to store project-level data.

## Parameters

We can pass arbritrary data to functions using parameters (also called function arguments).

In the example below the function has 2 parameters (from and text).

```javascript
function showMessage(from, text) {
  alert(from + ": " + text);
}

showMessage("Ann", "Hello!"); // Ann: Hello! (*)
showMessage("Ann", "What's up!"); // Ann: What's up? (**)
```

When the function is called in lines (\*) and (\*\*), the given values are copied to local variables from and text. Then the function uses them.

## Default Values

If a parameter is not provided, then its value becomes undefined.

For instance the aforementioned function `showMessage(from, text)` can be called with a single argument: `showMessage("Ann");`

That's not an error. Such a call would output: `Ann: undefined`. There's no `text`, so it's assumed that `text === undefined`.

If we want to use a default `text` in this case, then we can specify it from after `=` :

```javascript
function showMessage(from, text = "no text given") {
  alert(from + ": " + text);
}

showMessage("Ann"); //Ann: no text given
```

### Evaluation of Default Parameters

A default parameter is evaluated every time the function is called without the respective parameter. In the following example, `anotherFunction()` is called everytime `showMessage()` is called without the `text` parameter:

```javascript
function showMessage(from, text = anotherFunction()) {
  // anotherFunction() only executed if no text given
  // it's result becomes the value of text
}
```

### Old Style for Default Parameters

JavaScript hasn't always supported default parameters, so before it was added as a standard, explicit checks for parameters being `undefined` were done.

```javascript
function showMessage(from, text) {
  if (text === undefined) {
    text = "no text given";
  }

  alert(from + ": " + text);
}
```

another way was:

```javascript
function showMessage(from, text) {
  text = text || "no text given";
}
```

## Returning a Value

Functions can return a value back into the calling code as the result.
The `return` directive can be in any place of the function, so when the execution reachs it, the function stops and the value is returned to the calling code.

There can be multiple returns, but only 1 can be reached per function call.

Example:

```javascript
function checkAge(age) {
  if (age >= 18) {
    return true;
  } else {
    return confirm("Do you have permission from your parents?");
  }
}

let age = prompt("How old are you?", 18);

if (checkAge(age)) {
  alert("Access granted");
} else {
  alert("Access denied");
}
```

It's also possible to `return` without a value. That causes a function to exit immediately.

Empty and no returns always return `undefined`

## Naming Functions

Functions are actions. So their name is usally a verb, and breif. They should be as accurate as possible and in most cases start off with a verbal prefix ('get...', 'calc...', 'create...', 'show...', etc.).

### One Function: one action

A function should do exactly what it's name suggests and nothing more.

Two independent actions should be 2 independent functions.
