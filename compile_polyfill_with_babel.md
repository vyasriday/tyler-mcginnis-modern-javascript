* Babel only compiles ES6+ code ES5. fetch API is not part of ES6 or Javascript, it's a browser API and babel keeps it as it is. It needs to polyfilled.
* There are still some features babel does not compile back to ES5 and we need polyfill for such features. eg. promises.
* Compiling does not add anything new or new properties to our code. Not all ES6 features can be compiled to ES5 and for some polyfills are required.


#### Features that need to be compiled
* Arrow functions
* Async functions
* Async generator functions
* Block scoping
* Block scoped functions
* Classes
* Class properties
* Computed property names
* Constants
* Decorators
* Default parameters
* Destructuring
* Do expressions
* Exponentiation operator
* For-of
* Function bind
* Generators
* Modules
* Module export extensions
* New literals
* Object rest/spread
* Property method assignment
* Property name shorthand
* Rest parameters
* Spread
* Sticky regex
* Template literals
* Trailing function commas
* Type annotations
* Unicode regex
#### Features that need to be polyfilled
* ArrayBuffer
* Array.from
* Array.of
* Array#copyWithin
* Array#fill
* Array#find
* Array#findIndex
* Function#name
* Map
* Math.acosh
* Math.hypot
* Math.imul
* Number.isNaN
* Number.isInteger
* Object.assign
* Object.getOwnPropertyDescriptors
* Object.is
* Object.entries
* Object.values
* Object.setPrototypeOf
* Promise
* Reflect
* RegExp#flags
* Set
* String#codePointAt
* String#endsWith
* String.fromCodePoint
* String#includes
* String.raw
* String#repeat
* String#startsWith
* String#padStart
* String#padEnd
* Symbol
* WeakMap
* WeakSet

