# Basic Info

JavaScript was developed to allow developers to add life to web pages (interactivity, animations, etc.)

Programs are called 'scripts'

JavaScript can execute on browsers, server's or any device with a JavaScript engine.

The most popular javascript engines are:

- V8 (used in Chrome)
- SpiderMonkey (used in FireFox)
- JavascriptCore (used in Safar)

### How do engines work?

1. Engine reads (parses) the script
2. Converts (compiles) the script to machine langauge
3. Runs machine code

Javascript engines apply many optimizations to the machine to make it run faster.

## What can in-browser JavaScript do?

It's considered to be a safe langauge, meaning that it doesn't allow low level access
to memory or CPU, as it was developed to be used in browsers.

JavaScripts capabilites greatly depend on the environment that it's running in:

- Node.js: supports reading/writing arbritray files, performing network requests and etc.
- Browsers: Can do all types of webpage manipulations, interaction with user and webserver/
  - add new html pages, change existing content, modify styles
  - react to user actions, run on events like mouse clicks, movements, key-presses and etc.
  - Send requests over the network to remote servers, download and upload files (AJAX, Fetch)
  - Get and set cookies, ask questions to the user and show messages
  - Store data on the client's machine (local storage)

## What can't in-browser JS do?

Javascript in the browser is restricted in it's abilities to protect the user from malicious websites.

Examples of restrictions:

- no reading or writing arbritrary files on hard disk, files can only be provided if the user performs certain actions (dragging and dropping a file, or selecting via an input tag).
- Camera, Microphone and other sensor input is allowed by modern browsers but require the user to explicitly provide permission.
- JavaScript in one tab or window can't access pages opened in others. "Same Origin Policy" exists in order to only allow communication between sites if both of them agree to it.
- JavaScript in a page can easily communicate with the server that it came from, but it's ability to communicate with other pages is crippled and requries explicit agreement (http headers) from the remote server.

## What makes JS unique?

1. Full integration with HTML/CSS
2. Simple things are done simply (developer friendly)
3. Support from all major browsers and it's enabled by default

## Other Popular Flavours of JS

These are compiled into JavaScript, but written in their own syntax.

- CoffeeScript: syntactical sugar in shorter syntax allowing clearer and more precise code. Ruby developers enjoy it.
- TypeScript: concentrated on adding strict data typing to simply development and support of complex systems. Made by Microsoft
- Flow: also adds data typing but in a different way. Made by Facebook.
- Dart: standalone language with it's own engine that runs in non-browser environments (mobile apps), can be transpiled to JavaScript.

#### Credit: https://javascript.info/intro
