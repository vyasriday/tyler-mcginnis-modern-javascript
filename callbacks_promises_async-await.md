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
Depending upon the state of promise, fulfilled or rejected, a promise can be consumed in a `.then` or in a `.catch` and ultimately irrespective of state (fulfilled or rejected) `.finally` gets invoked.
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
