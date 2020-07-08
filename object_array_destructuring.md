
### Object and Array Destructuring

#### Just like we add one value at a time and extract one value at a time, we can do so with multiple values
#### whenever there is an object on the RHS, we can destruct values out of it using object destructuring

#### Object Destructuring
```javascript
const object = {}
object.name = "Hridayesh"
object.value = 21

console.log(object.name, object.value)

// adding multiple values
const object = {
  name: 'Hridayesh',
  value: 21
}

// extrting multiple values in the same way
const {name, value} = object

// extracting nested object values

const object = {
  name: 'Hridayesh',
  address: {
    street: '',
    pin: 00000
  }  
}

const {name, address: {stret, pin}} = object
```

#### Array Destructuring
- In case of Arrays, destructuring works based on index as there are no named properties in arrays

```javascript

const array = ["one", "two", "three"]
const [one, two, three] = array
log(one, two, three) // "one", "two", "three"

// nested array values

const array = ["one", "two", ["three", "four"]]
const [one, two, [three, four]] = array

```

#### Use Cases for Destructuring

* Assigning different names to variables then the object property names
```javascript
const object = {
  n: "Hridayesh",
  c: 21
}

// Now we want to use different names rather than n and c
// const {original:new_name} = object
const {n: name, c: category} = object
log(name, category) // n is created as name and c as category
```

* Object Destructuring in function definition for function parameters
```javascript

// passing an object to the function
function takesObject(object) {
  const {name, place, value} = object
  // ....
}

takesObject({name: 'Hridayesh', place: 'Jaipur', value: 21})

// destructuring arguments in function parameters. takesObject takes an object as argument
function takesObject({name, place, value}) {

  // ....
}

takesObject({name: 'Hridayesh', place: 'Jaipur', value: 21})

// Assigning default values to parameters
function takesObject({name = "default", place = "Earth, value= 0}) {

  // ....
}

// using array destructuring in function definition

function takesArray([firstName, lastName]) {
  // ...
}

takesArray(["Hridayesh", "Sharma"])

```




