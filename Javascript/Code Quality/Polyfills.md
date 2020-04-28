# Polyfills

The JavaScript language steadily evolves. New proposals appear regularly, and if they're considered worthy, they start making their way towards becoming a standard.

The teams behind major JavaScript engines have their own ideas about what to implement first. They may decide to implement proposals that are in draft and postpone things that are already in spec, because they are less interesting or harder to do.

So it's very common for JavaScript engines to only implement part of the standard.

## Babel

When we use modern features of JavaScript, some engines may fail to support such code. Just as said, not all features are implemented everywhere.

Here Babel comes to the recuse.

Babel is a transpiler. It rewrites modern JavaScript code into the previous standard.

## Two Parts in Babel

1. The Transpiler which rewrites the code: The developer runs it on their own computer, it rewrites the code into the older standard. And then the code is devliered to the website for users. Modern project build systems like `webpack` provide means to run transpiler automatically on every single code change, so that it's very easy to integrate into development process.
2. Second, the polyfill: New langauge features may include new built-in functions and syntax constructs. The transpiler rewrites the code, transforming syntax constructs into older ones. But as for new built-in functions, we need to implement them. JavaScript is a highly dynamic language, scripts may add/modify any functions, so that they bheave according to the modern standard.

   A script that updates/adds new functions is called 'polyfill'. It 'fills in' the gap and adds missing implementations.

   #### 2 Interesting Polyfills Are:

   - `core js` that supports alot, allows to include only needed features.
   - `polyfill.io` service that provides a script with polyfills, depending on the features and the user's browser.

So, if we're going to use modern language features, a transpiler and a polyfill are necessary.
