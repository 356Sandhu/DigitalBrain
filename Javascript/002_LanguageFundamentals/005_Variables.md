# Variables

- named storage for data
- declared with the 'let' keyword

## Basics

### Declaration

### Single Variable

```javascript
let name = "Satvir";
console.log(name);
// Prints: Satvir
```

#### Multiple Variables

```javascript
let name = "Satvir",
  age = 22,
  country = "Canada";
// Prints: Satvir
```

### Other Assignments

You can assign variables to store more than just numbers and strings

```javascript
let name = "Satvir";
let author = name;
console.log(author);
// Prints: Satvir
```

### Assignment and 'use strict'

#### Without 'use strict'

```javascript
// no "use strict"
num = 5; // creates variable num
alert(num); // alerts '5'
```

#### With 'use strict'

```javascript
"use strict";
num = 5; // error: num is not defined
```

### Casing:

- Must contain only letters, digits, or the symbols \$ and \_
- The first character must not be a digit
- camelCase is the preffered style by many.
- Case matters. 'apple' and 'aPple' aren't the same.

## Constants

Constants are variables whose values cannot be reassigned.
They will throw and error if an attempt is made to reassing them.

### Example

```javascript
const name = "Satvir";
console.log(name);
```

### Uppercase Constants

Using all uppercase characters in the name of a constant is common practice if the values are already known and difficult to remember

```javascript
const COLOR_RED = "#F00";
const COLOR_BLUE = "#00F";
```

## Naming

- Name variables human readable, like 'userName' or 'shoppingCart'
- Avoid abbreviations
- Make names as descriptive as possible ('weatherData' over 'data')
- When working in teams, agree on names before hand to avoid compatability issues.

## Summary

- 'let' is the modern way to declare variables
- 'var' is the old school way, differences between itself and
  'let' will be discussed later.
- 'const' is like 'let' but the value of the variable can't change.
