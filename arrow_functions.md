// 🤔 since console.log returns undefined we get props returned as well as console.log too
const arr = (props) => console.log(props) || props

#### arrow functions have no `this` keyword of their own, they find it lexically until the parent is a normal function. If it's arrow function then they again go one level up.

* Eg 1 

```javascript
function sayHello() {
  return function() {console.log(this)}
}

sayHello()() // Window object
```

* Eg 2

```javascript
function sayHello() {
  retun () => console.log(this)
}

sayHello() // Window as the value of `this` in the parent is Window
``

* Eg 3

```javascript
function sayHello() {
  return () => console.log(this)
}

sayHello.call({})() // {} since in the parent value of this is {}
```

* Eg 4

```javascript
function parent() {
  function sayHello() {
    return function() {console.log(this)}
  }
  
  return sayHello()
}
parent()() // window

```

* Eg 4

```javascript
function parent() {
  sayHello = () =>  {
    return () =>  {console.log(this)}
  }
  
  return sayHello()
}

parent()() // Window
parent.call({})() // {}
```



