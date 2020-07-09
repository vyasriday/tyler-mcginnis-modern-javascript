#### In ES5 Objects we can use `[]` notation to use expression to set the property names


```javascript
const property = "name"
const object = {}
object[property] = "Hridayesh"

object.name // Hridayesh

object['age' + 'value'] = 21
object.agevalue // 21
```

#### Using Computed Property Names in ES6

* We can use the bracket notation in the object literal itself.
```javascript
const property = "name"
const object = {
  [property] : "Hridayesh",
  ['age' + 'value']: 21
}
```
