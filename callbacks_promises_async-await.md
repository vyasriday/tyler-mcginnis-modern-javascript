### Callbacks, Promises and Async Await

#### Higher Order Function (HOF)

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
