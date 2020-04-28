# Function Expressions

In JavaScript, a function is not a 'magical language structure', but a special kind of value.

The syntax we used before is called a `Function Declaration`:

```javascript
function sayHi() {
  alert("Hello");
}
```

There is another syntax for creating a function that is called a `Function Expression`. It looks like this:

```javascript
let sayHi = function () {
  alert("Hello");
};
```

In this expression syntax the function is created and assigned to a variable explicitly like any other value. No matter how the function is called, it's just a value store in the variable `sayHi`.

The meaning of these code samples is the same: "create a function and put it inot the variable `sayHi`".

We can even print out that value using alert:

```javascript
function sayHi() {
  alert("Hello");
}

alert(sayHi); // shows the function code
```

The last line in this snippet does not run the function, because there are no parenthesis after `sayHi`. There are programming languages where any mention of a function name causes its execution, but JavaScript is not like that.

In JavaScript, a function is a value, so we can deal with it as a value. The code above shows it's string representation, which is the source code.

However, a function is still a special value as we can call it like `sayHi()`. But it is still a value, so we can work with it like one.

We can copy a function to another variable:

```javascript
function sayHi() {
  // 1: Create
  alert("Hello");
}

let func = sayHi; // 2: Copy

func(); // 3: Run the Copy, it works!
sayHi(); // 3: Run the Original, it works too!
```

### Why does a function expression have a semi-colon at the end?

- There is no need for `;` at the end of code blocks and syntax structures like `if{ ... }`, `for{ }`, `function f { }`, etc.
- A function expression is used inside the state, as a value it's not a code block, but rather an assignment. The semicolon `;` is strongly recommended at the end of statements, no matter what the value is.

## Callback Functions

Let's look at more examples of passing functions as values and using function expressions.

We'll write a function `ask(question, yes, no)` with three parameters:

- `question`: Text of the question
- `yes`: Function to run if the answer is `Yes`.
- `no`: Function to run if the answer is `No`.

The function should ask the `questuib` and, depending on the user's answer, call `yes()` or `no()`.

```javascript
function ask(question, yes, no) {
  if (confirm(question)) yes();
  else no();
}

function showOk() {
  alert("You agreed.");
}

function showCancel() {
  alert("You canceled the execution");
}

// usage: function showOk, showCancel are passed as arguments.
ask("Do you agree?", showOk, showCancel);
```

The arguments `showOk` and `showCancel` of `ask` are called callback functions / callbacks as they are functions that are expected to be "called back" at a later time in the program if necessary.

We can use function expressions to make the code even shorter.

```javascript
function ask(question, yes, no) {
  if (confirm(question)) yes();
  else no();
}

ask(
  "Do you agree?",
  function () {
    alert("You agreed.");
  },
  function () {
    alert("You canceled the execution.");
  }
);
```

Here the functions are declared right inside the `ask(...)` call. They have no name, and so are called "anonymous". Such functions are not accessible outside of `ask`.

## Function Expression vs Declaration

- Function Declaration: a function, declared as a seperate statement, in the main code flow.
- Function Expression: a function created inside an expression or inside another syntax construct. (right side of an assignment operator)

### Key Notes

- A function expression is created when the execution reaches it and is usable only from that moment
- A function declaration can be called earlier than it is defined
  - When the JavaScript engine prepares to run a script, it first looks for global function declarations and creates those functions. After all of these function declarations are processed, only then does the code begin executing.
- In `strict mode`, when a function declaration is within a code block, it's visible everywhere inside that block but not outside it.

## When to choose Function Declaration versus Function Expression?

Rule of thumb is to always consider a funtion declaration first, and only use an expression if the declaration doesn't suite the scenario (like a conditional declaration).
