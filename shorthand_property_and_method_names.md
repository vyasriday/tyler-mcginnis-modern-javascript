const name = "Hridayesh"
const place = "Jaipur"

#### using ES5 Object literals to add properties and methods to an object
const object = {
  name: name,
  place: place,
  save: function() {
    // save data
  }
}

// using ES6 shorthand property syntax

const object = {
  name, 
  place,
  save() {
   // save data
  }
}
