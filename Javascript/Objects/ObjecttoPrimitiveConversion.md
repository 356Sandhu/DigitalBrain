# Object to Primitive Conversion

What happens when objects are added `obj1 + obj2`, subtracted `obj1 - obj2` or printed using `alert(obj)`?

In that case, objects are auto-converted to primitives, and then the operation is carried out.

Here's how they behave:

1. All objects are `true` in a boolean context. There are only numberic and string conversions.
2. The numeric conversion happens when we subtract objects or apply mathematical functions. For instance `Data` objects can be subtracted, and the result `date1 - date2` is the time difference between the two dates.
3. As for string conversion - usually it happens when we output an object like `alert(obj)` and in similar contexts.

## ToPrimitive
