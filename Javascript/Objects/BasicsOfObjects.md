# Objects

Objects are used to store keyed collections of various data and more complex entities.

An object is created with figure brackets `{...}` with an optional list of properties. A `property` is a `key: value` pair, where key is a string (also called property name), and value can be anything.

We can imageine an object as a cabinet with signed files. Every piece of data is stored in its file by the key. It's easy to find a file by it's name or add/remove a file.

An empty object can be created using one of 2 syntaxes:

```javascript
let user = new Object(); // "object constructor" syntax
let user = {}; // Object literal syntax
```

Usually the "object literal" declaration syntax is used.

## Literals and Properties

We can immediately put some properties into `{...}` as `key:value` pairs:

```javascript
let user = {
  // an object
  name: "John", // by key "name" store value "John"
  age: 30, // by key "age" store value 30
};
```

A property has a key (also known as "name" or "identifier") before the colon ":" and a value to the right of it.

Property values are accessible using the dot notation:

```javascript
// get property values of the object:
alert(user.name); // "John"
alert(user.age); // 30
```

To remove a property, we can use the `delete` operator:

```javascript
delete user.age;
```

We can also use multiword property names, but they must be quoted:

```javascript
let user = {
  name: "John",
  age: 30,
  "likes birds": true,
};
```

The last property in the list may end with a comma:

```javascript
let user = {
  name: "John",
  age: 30,
};
```

That is called a "trailing" or "hanging" comma. Makes it easier to add/remove/move around properties, because all lines become alike.

## Square Brackets

For multiword properties, the dot access doesn't work.

The alternative square bracket notation works well for this case:

```javascript
let user = {};
user["likes birds"] = true;
alert(user["likes birds"]);
delete user["likes birds"];
```

Square brackets also provide a way to obtain the property name as the result of any expression - as opposed to a literal string - like from the variable as follows:

```javascript
let key = "likes birds";

// same as user["likes birds"] = true;
user[key] = true;
```

Here the variable `key` may be calculated at run-time or depend on the user input. And then we use it to access the property. That gives us a great deal of flexibilty.

Dot notation doesn't allow us to do this.

### Computer Properties

We can use square brackets in an object literal. That's called computed properties, for instance:

```javascript
let fruit = prompt("Which fruit to buy?", "Apple");

let bag = {
  [fruit]: 5, // the name of the property is taken from the variable fruit
};

alert(bag.apple); // 5
```

Square brackets are more powerful but can be more cumbersome to work with, so when possible, use dot notation.

## Property value shorthand

In real code we often use existing variables are values for property names. For instance:

```javascript
function makeUser(name, age) {
  return {
    name: name,
    age: age,
    // ...other properties
  };
}
```

When making a property from a variable from the same name, there exists a shortcut:

```javascript
function makeUser(name, age) {
  return {
    name, // same as name: name
    age, // same as age: age
  };
}
```

## Property Names Limitations

Property names (keys) must be either strings or symbols (a special type for identifiers, to be covered later.)

Other types are automatically converted to strings.

For instance, a number `0` becomes a string `"0"` when used as a property key.

### Reserved words are allowed as property names.

For variables in JavaScript you can't use language reserved names like `for`, `let`, `return` etc. but for object properties, you can use those names.

The only exception to the reserved properties is `__proto__`, which is used for prototypal inheritance.

## Property Existence Test, "in" Operator

A notable feature for objects is that it's possible to access any property. There will be no error if the property doesn't exist! Accessing a non-existing property just returns `undefined`. It provides a very common way to test whether to get it and compare vs undefined.

```javascript
let user = {};

alert(user.noSuchProperty === undefined); // true means the property doesn't exist!
```

There also exists a special operator `in` to check for the existence of a property. The syntax is:

```javascript
"key" in object;
```

For instance:

```javascript
let user = { name: "John", age: 30 };

alert("age" in user); // true, user.age exists
alert("blabla" in user); // false user.blabla doesn't exist.
```

Note that on the left side of the `in` operatore there must be a property name. That's usually a quoted string.

If we omit quotes, that would mean a variable containing the actual name will be tested. For Instance:

```javascript
let user = { age: 30 };

let key = "age";
alert(key in user); // true, takes the name from the variable key "age"
```

### The undefined edge case:

If a property does exist but the developer has assigned it to be `undefined` then the `=== undefined` trick will say that the key doesn't exist. The `in` operator howevevr will return true..

## The `for...in` loop

To walk over all keys of an obejct, there exists a special form of the loop `for...in`. This is a completely different thing from the `for(;;)` construct.

The syntax:

```javascript
for (key in object) {
  // executes the body for each key among object properties
}
```

For instacne:

```javascript
let user = {
  name: "John",
  age: 30,
  isAdmin: true,
};

for (let key in user) {
  // keys
  alert(key); // name, age, isAdmin
  // values for keys
  alert(user[key]); // John, 30, true
}
```

### Order of object properties

The order of object's properties works like this: integer properties are sorted, others appear in creation order. (integer property means that it can be converted to and from an integer without change)

## Copy by Reference

One of the fundamental differences of objects vs primitives is that they are stored and copied "by reference".

Primitive values: strings, numbers, booleans - are assigned/copied "as a whole value"

For instance:

```javascript
let messsage = "Hello!";
let phrase = message;
```

As a result we have two independent variables, each one is storing the string "Hello!".

Object's are not like that! A variables stores not the object itself but it's address in memory, in other words a reference to it.

Object's aren't duplicated, only referenced.

for instance:

```javascript
let user = { name: "John" };

let admin = user; // copy the reference
```

Now, we have two variables, `user` and `admin` both referencing the same object. We can use any variable to access the object and modify it's contents.

```javascript
let user = { name: "John" };

let admin = user;

admin.name = "Pete";

alert(user.name); //'Pete'
```

Again, we only have 1 object, but multiple variables referencing it.

### Comparison by reference

The equality `==` and strict equality `===` operators for objects work exactly the same.

**Two objects are equal only if they are the same object**
For instacne, if two variables reference the same object, they are equal.

2 independent objects, even if their contents are the same are never equal.

### Const object

An object declared as `const` can be changed.

For instance:

```javascript
const user = {
  name: "John",
};

user.age = 25;

alert(user.age); // 25
```

It might seem that assigning `age` might cause a problem but it doesn't. This is because `user` stores a reference to the same object, messing around with the objects parameters don't affect the reference.
Trying to assign the variable to another object or something else however would throw an error, like this:

```javascript
const user = {
  name: "John",
};

user = {
  // ERROR (can't reassign user)
  name: "Pete",
};
```

## Cloning and Merging, Object.assign

Copying an object variable creates one more reference to the same object, but there also exist 2 way to actually clone them.

1. The first way is to run a `for...in` and duplicate items from one object into another.
2. The second way is to use `Object.assign`

The syntax is:

```javascript
Object.assign(dest, [src1, src2, src3]);
```

- Arugments `dest` and `src, ..., srcN` (can be as many as needed) are objects.
- It copries the properties of all objects: `src, ..., srcN` and returns `dest`

If the receiving object `dest` already has the same name property, it will be overwritten.

### Properties as Object

Until now we assumed that all properties of `user` are primitive. But properties can be references to other objects. What to do with them?

Like this:

```javascript
let user = {
  name: "John",
  size: {
    height: 182,
    weight: 50,
  },
};

alert(user.size.height); //182
```
