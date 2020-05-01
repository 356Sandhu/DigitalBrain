# Garbage Collection

Memory management in JavaScript is performed automatically and behind the scenes. How doesthe JavaScript engine discover what we don't need anymore and clean it up?

## Reachability

The main concept of memory management in JavaScript is reachability.

"Reachable" values are those that are accessible and usable. They are garunteed to be stored in memory.

1. There's a base set of inherently reachable values that cannot be deleted for obbvious reasons:

- Local variables and parameters of the current function
- Variables and parameters for other functions on the current chain of nested calls.
- Global variables.
- (there are other internal ones as well)
  These values are called `roots`

2.  Any other value is considered reachable from a root by a reference or by a chain of references. For instance, if there's an object in a local variable and that object has a property referencing another object, that object is considered reachable. And those that it references are also reachable.

There's a background process in the JavaScript engine that is called `garbage collector`. It monitors all objects and removes those that have become unreachable.

## Simple Example:

```javascript
let user = {
  // Object is created, and User references the object
  name: "John",
};

user = null;
// The user object doesn't reference the previous object anymore, so the garbage collector deems the object unreachable and deletes it.
```

## Interlinked Objects

In the case of objects that reference one another, it goes as follows. As long as there are incoming references from reachable objects/variables, the object will remain in memory. Once there are no incoming references, it is removed by the garbage collector.

## Unreachable Island

It is possible that a large amount of of objects can be deemed unreachable. In the case you have a parent object, with multiple children, if the parent is unreachable, then all the children are deemed unreachable too.

## Internal Algorithm

The basic garbage collection is called "mark-and-sweep".

The following garbage collection steps are regularly performed:

- The garbage collector takes roots and 'marks'(remembers) them
- Then it visits and 'marks' all references from them.
- The it visits marked objects and marks their references. All visited objects are remembered, so as not to visit the same object twice in the future.
- ...And so on until every reachable (from the roots) references are visited.
- All objects except marked ones are removed.

JavaScript engines may apply many optimizations to make it run faster and not affect the execution.

Some of the optimizations:

- **Generational Collection**: Objects are split into two sets: "old ones" and "new ones". Many objects appear, do their job and die fast, they can be cleaned up aggressively. Those that survive for long enough, become "old" and are examined less often.
  -- **Incremental Collection**: If there are many objects, and we try to walk and mark the whole object set at one, it may take some time and introduce visible delays in the execution. So the engine tries to split the garbage collection into many pieces. Then the peices are executed one by one, seperately. That requires some extra bookkeeping between them to track changes, but we have many tiny delays instead of a big one.
- **Idle-Time Collection**: The garbage collector tries to run only while the CPU is idle, to reduce the possible effect on the execution

There are many other optimizations and flavours of garbage collection.
