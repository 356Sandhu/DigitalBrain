# Data Types

There are 8 basic data types in javascript.

- number: for numbers of any kind: integer or floating point. Integers are limited by ±2^53
- bigint: is for integer numbers of arbritrary length
- string: for strings. Can be one or many characters long, as JS doesn't have a type for 'chars'
- boolean: true or false
- null: for unknown values - a standalone type that has a single value null
- undefined: for unassigned values - a standalone type that has a single value undefined.
- object: for more complex data structures
- symbol: for unique identifiers

#### typeof

Allows us to see which type is stored in a variable.

```javascript
// has two forms
typeof x;
typeof x;
```

both types return a string with the data type: 'String'

- for null returns "object" - this is an error on the part of the language, it's not actually an object.
