# Object Methods, 'this'

Objects are usually created to represent entities of the real world, like users, orders and so on:

```javascript
let user = {
  name: "John",
  age: 30,
};
```

And, in the real world, a user can act: select something from the shopping cart, logout etc.

Actions are represented in JavaScript by functions in properties.

## Method Examples

A function that is a property of an object is called a `method`. Here's an example:

```javascript
let user = {
  name: "John",
  age: 30,
};

user.sayHi = function () {
  alert("Hello!");
};

user.sayHi(); // Hello!
```

We could also do use a predeclared function like this:

```javascript
let user = {...}

function sayHi(){
  alert("Hello!");
}

user.sayHi = sayHi;

user.sayHi(); //Hello!
```

### Method Shorthand

There exists a shorter syntax for methods in an object literal:

```javascript
// these objects do the same
user = {
  sayHi: function () {
    alert("Hello!");
  },
};

// method shorthand
user = {
  sayHi() {
    alert("Hello!");
  },
};
```

As shown we can omit `function` and just write `sayHi()`. However, there are subtle differences between the notations, especially when it comes to inheritance. In almost all cases, the shorter syntax is preffered.

## 'this' in Methods

It's common that an object needs to access the information stored in the object to do its job.

For instance the code inside `user.sayHi()` may need the name of the `user`.

**To access the object, a method can use the `this` keyword.**

For instance:

```javascript
let user = {
  name: "John",
  age: 30,

  sayHi() {
    // "this" is the "current object"
    alert(this.name);
  },
};

user.sayHi(); // John
```

Technically `user.name` would also work, but it's unreliable (copied objects will reference the older one).

## `this` is not bound

In JavaScript, keyword `this` behaves unlike most other programming languages. It can be used in any function.

There's no syntax error in the following example:

```javascript
function sayHi() {
  alert(this.name);
}
```

The value of `this` is evaluated during the run-time, depending on the context.

For instace, here the same function is assigned to two different objects and has different "this" in the calls:

```javascript
let user = { name: "John" };
let admin = { name: "Admin" };

function sayHi() {
  alert(this.name);
}

user.f = sayHi;
admin.f = sayHi;

user.f(); // John
admin.f(); // Admin
admin["f"](); // Admin (also works!)
```

### When calling `this` without an object: `this == undefined`

## Arrow Functions have no `this`

Arrow functions are special: they don't have their own `this`. If we reference `this` from an arrow function, it's taken from the outer "normal" function (non-arrow):

```javascript
let user = {
  firstName: "Ilya",
  sayHi() {
    let arrow = () => alert(this.firstName);
    arrow();
  },
};

user.sayHi(); //Ilya
```

As shown here, when `arrow()` was called, `this.firstName` behaved as if the statement was in the outer function `sayHi()`.
