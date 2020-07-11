## Callbacks, Promises and Async Await

### Higher Order Function (HOF)

A HOF is a function that takes another function (callback) as an argment.

```javascript
function HOC (x, callback) {
  return callback(5, x)
}

function add(x,y) {
  return x+y;
}

const addFiveToTen = HOC(10, add)
```

### Callback Pattern

* Callback pattern is basically passing a function to another function so that it can invoke our function based on certain conditions later on

Example 
```javascript
window.addEventListener('click', () => alert('clicked!!!'))

// addEventListener is HOF that takes another function as a callback and calls it when someone clicks anywhere in window
```

* callback hell is basically drilling down the callbacks 

Example
```javascript
function getUser(uid, getUserLocation) {
  const user = getUserAPICall(uid)
  getUserLocation(user.pin, getUserLocationWeather)
}

function getUserLocation(pin, getUserLocationWeather) {
  const location  = getUserLocationAPICall(pin)
  getUserLocationWeather()
}

function getUserLocationWeather() {
  console.log("Weather is Good!!!")
}

getUser(121, getUserLocation)
```

### Promises

#### Three States of a Promise 
* Pending (default, initial state)
* Fulfilled (Promise is Successful)
* Rejected (Promise is Rejected)

##### Creating a Promise

* A promise can be created using `Promise` constructor.
* A Promise constructor takes a callback and invokes it with `resolve`, and `reject` methods.
* Whatever data resolve is invoked with inside the callback, gets passed to the callback inside `.then` callback.

```javascript
const promise = new Promise((resolve, reject) => {
  /**
  * resolve(data) // when resolve is invoked the status of promise is fulfilled
  * reject(err) //  when reject is invoked the status of promise is rejected
  */ 
  
})

console.log(promise) // an object with methods like then, catch, finally etc available on it's prototype
```


##### Consuming a Promise
* Depending upon the state of promise, fulfilled or rejected, a promise can be consumed in a `.then` or in a `.catch` and ultimately irrespective of state (fulfilled or rejected) `.finally` gets invoked.
* `.catch` gets invoked whenever we a promise is rejected using `reject` method or an error is thrown from previous `.then` or a `.catch` 
```javascript
promise
  .then(response => fulfilled state goes here)
  .catch(err => rejected state goes here)
  .finally(() => anyway call me)
```
NOTE: 
  1. The return of `.then` is a promise with fulfilled state.
  2. The return of `.catch` is a promise with fulfilled state if no error is returned

```javascript
function getUser(uid) {
  return new Promise((resolve, reject) => {
    setTimeout(() => resolve(user), 1000)  
  })
}

function getUserLocation(pin) {
  return new Promise((resolve, reject) => {
    setTimeout(() => resolve(location), 1000)  
  })
}

function getUserLocationWeather() {
  console.log("Weather is Good!!!")
}

getUser(123)
  .then((user) => getUserLocation(user.pin))
  .then((location) => getUserWeather())
  
```

#### Promise Chaining

* Whenever we call a `.then` or a `.catch` the return value of of callback inside `.then` or `.catch` is wrapped inside a promise and that's how we can get the promise chaining
* Even though we don't return anything from a `.then`, still a promise is returned and can be used in next  `.then`. Since nothing is returned we don't get any data in next chainable `.then` callback. 

```javascript
function promise() {
    return Promise.resolve(1)
}

var p1 = promise().then(() => {}) // promise resolves to undefined value

var p2 = promise1.then(() => {}) // // promise resolves to undefined value
```

```javascript
function getUser(uid) {
  return new Promise((resolve, reject) => {
    setTimeout(() => resolve(user), 1000)  
  })
}

const userPromise = getUser(123)
const userPromiseReturn = userPromise.then((user) => user.id)
userPromiseReturn.then(id => console.log(id))

/**
  The above code is similar to following
  getUser(123)
    .then(user => user.id)
    .then(id => console.log(id))
*/
```

#### Example from Tyler
```javascript
function getPromise () {
  return new Promise((resolve) => {
    setTimeout(resolve, 2000)
  })
}

function logA () {
  console.log('A')
}

function logB () {
  console.log('B')
}

function logCAndThrow () {
  console.log('C')

  throw new Error()
}

function catchError () {
  console.log('Error!')
}

getPromise()
  .then(logA) // A
  .then(logB) // B
  .then(logCAndThrow) // C
  .catch(catchError) // Error!
```

### Async Await 

* Async Await basically is API in JavaScript to consume Promises in a better way.
* It's like writing our asynchronous code as if it is synchronous. 😲😲😲😲.
* Adding `async` keyword in front of a function does two things
  * function always returns a promise. Whatever is retuned from a `async` function gets wrapped in a Promise.
  * `await` can be used inside the function.
* The return value of an async function is always a promise 😮😮

```javascript
async function getPromise(){}
const promise = getPromise() 
console.log(promise) // Promise Object resolves to undefined

async function add(x,y) {
  return x+y // it is like resolve(x+y)
}

const result = add(1,2)
result.then(result => console.log(result)) // 3, I am totally blown here 😦😦

// async function add() {
  throw new Error(12) // it's like reject(12)
}

add().catch(e => console.log(e)) // 12

```

```javascript
function getUser(uid) {
  return new Promise((resolve, reject) => {
    setTimeout(() => resolve(user), 1000)  
  })
}

function getUserLocation(pin) {
  return new Promise((resolve, reject) => {
    setTimeout(() => resolve(location), 1000)  
  })
}

// browser sees `async` and realises there is going to be some asynchronous function call in here 
async function consumePromise() {
  const user = await getUser(123) // browser sees await and understands that it's not a normal function invocation. It's async code so it waits here until it gets the results.
  const location = await getUserLocation(user.id) // whatever is resolved from promise, gets in location
} 

```

#### Error Handling with `async-await`
1.
  * Wrap our await code in a `try catch` block.
  * Error handling is done inside the `catch` block.

```javascript
function getUser(uid) {
  return new Promise((resolve, reject) => {
    setTimeout(() => resolve(user), 1000)  
  })
}

async function consumePromise() {
  try {
     const user = await getUser(123)
     console.log(user)
  } catch (e) {
    // rejected promise goes here
  }
 
}

```

2. Since all `async` functions return a promise, we can use a `.catch` on it.
  * Use this method if the invocation of `async` function is in our hands.

```javascript
async function add() {
  return 3
} 
// 
add().catch(e => e)
```
