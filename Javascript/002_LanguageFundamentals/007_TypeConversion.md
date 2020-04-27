# Type Conversions

Most of the time when we want to, operators and functions will implicitly convert the values given to them to the correct type.

- for example: 'alert' automatically converts any value to a string to show it.

However, there are cases where we need to explicitly convert a value to the expected type.

## String Conversion

Occurs when we output something. Can be performed with 'String(value)'. The conversion to string is usually obvious for primitives

## Number Conversion

Occurs in math operations. Can be performed with 'Number(value)'

The following rules apply to conversions

- undefined becomes NaN
- null becomes 0
- true / false becomes 1 / 0
- string: is read as is, whitespaces from both sides are removed. An empty string becomes 0 and an error returns NaN.

## Boolean Conversion

Occurs in logical operations. Can be performed with 'Boolean(value)'

The following rules apply:

- 0, null, undefined, NaN become false
- any other value becomes true

### Objects will be covered in later sections.
