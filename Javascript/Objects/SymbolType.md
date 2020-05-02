# Symbol Type

By Specification, object property keys may be either of string type, or of symbol type. Not numbers, not booleans, only strings or symbols, these two types.

## Symbols

A `Symbol` represents a unique identifier.

A value of this type can be created using `Symbol():`

```javascript
// id is a new symbol
let id = Symbol();
```

Upon creation, we can give symbol a description (also called symbol name), mostly used for debugging purposes:

```javascript
// id is a symbol with the description "id"
let id = Symbol("id");
```

Symbols are guarunteed to be unique. Even if we create many symbols with the same description, they are different values. The description is just a label that doesn't affect anything.

For instance, here are two symbols with the same description - they are not equal:

```javascript
let id1 = Symbol("id");
let id2 = Symbol("id");

alert(id1 == id2); // false
```

### Symbols don't auto-convert to string!

Most values in JavaScript support implicit conversion to a string, symbols don't auto-convert. You must do `id.toString()` if you're trying to print `id = Symbol("id")`. However you can easily get the description via `id.description`.

## Hidden Properties

Symbols allow us to create "hidden" properties of an object, that no other part of the code can accidentally access or overwrite.

For instance, if we're working with `user` objects, that belong to a third party code. We'd like to add identifiers to them.

Let's use a symbol key for it:

```javascript
let user = {
  name: "John",
};

let id = Symbol("id");

user[id] = 1;

alert(user[id]); // We can access the data using the symbol as the key
```

The benefit of doing this is because when working with third party code, you don't just want to add your own fields, as it's dangerous and could conflict and jumble up code. A symbol won't be accessed by any of the third party code, so it's safe to work with.

### Symbols in a literal

```javascript
let id = Symbol("id");

let user = {
  name: "John",
  [id]: 123, // not "id: 123"
};
```

### Symbols are skipped by `for...in`

Symbolic properties do not participate in `for...in` loop. `Object.keys()` also ignores them. That's a part of the general "hiding symbolic properties" principle.

In contrast `Object.assign` copies both string and symbol properties. As when cloning or merging, we usually want everything as it was.

## Global Symbols

As we've seen, usually all symbols are different, even if they have the same name. But sometimes we want same-named symbols to be entities. For instance different parts of our application want to access symbol "id" meaning the same property.

To achieve that there exists a global symbol registry. We can create symbols in it and access them later, and it guarantees that reapeated accesses by the same name return exactly the same symbol.

In order to read (create if absent) a symbol from the registry, use `Symbol.for(key)`.

That call checks the global registery, and if there's a symbol described as `key`, then returns it, otherwise creates a new symbole `Symbol(key)` and stores it in the registry by the given key.

For instance:

```javascript
// read from the global registry
let id = Symbol.for("id");

// read it again (maybe from another part of the code)
let idAgain = Symbol.for("id");

// the same symbol
alert(id === idAgain); // true
```

Symbols inside the registry are called global symbols. If we want an application-wide symbol, accessible everywhere in the code - that's what they are for.

### Symbol.keyFor

For global symbols, not only `Symbol.for(key)` returns a symbol by name, but there's a reverse call: `Symbol.keyFor(sym)`, that does the reverse: returns a name by a global symbol. For instance:

```javascript
// get symbol by name
let sym = Symbol.for("name");
let sym2 = Symbol.for("id");

// get name by symbol
alert(Symbol.keyFor(sym)); //name
alert(Symbol.keyFor(sym2)); // id
```

The `Symbol.keyFor` internally uses the global symbol registry to look up the key for the symbol. So it doesn't work for non-global symbols. If the symbol is not global, it won't be able to find it and returns `undefined`.

## System Symbols

There exist many "system" symbols that JavaScript uses internally, and we can use them to fine-tune various aspects of our objects.

They are listed in specification in the 'Well-Known Symbols' table:

- `Symbol.hasInstance`
- `Symbol.isConcatSpreadable`
- `Symbol.iterator`
- `Symbol.toPrimitive`
- ... and so on.

For instance `Symbol.toPrimitive` allows us to describe object to primitive conversion.
