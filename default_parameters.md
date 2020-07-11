#### default parameters are values we can set the function parameters to in case no value is passed for those variables. 

##### Doning Things ES5 way

```javascript

function(price, salesTax, discount) {
  salesTax = salesTax || 0.47
  discount = discount || 0
  // the problem here is if we pass 0 as values for sales and discount then too default values will be used. so let's make a change
  
  salesTax = typeof salesTax === 'undefined' ? 0.47: salesTax;
  discount = typeof discount === 'undefined' ? 0 : discount;
}

// So if the parameter values are undefined i.e no passed then we use default values we set ES5 way
NOTE: parameters for which we wish to have default values are moved to right side
```

##### Using ES6 default Parameters

```javascript
function func(price, salesTax=0.47, discount= 0) {
 console.log(price, salesTax, discount)
}

func(100) // 100, 0.47, 0
func(100, 1) // 100, 1, 0
func(100, 0.5, 5) // 100, 0.5, 0
func(100, undefined, undefined) // 100, 0.47, 0 

NOTE: default parametes are based on undefined values. whenever in a function a argument is not passed javascript sets it to undefined. So if we pass undefined values, still default values will be used
```

#### One Weird Case 😅 : Using a function as a default value to check if passed values is passed or not. Adding validation. 

```javascript

function isRequired(name) {
  throw new Error(name + ' is required')
}

function func(price = isRequired('price'), salesTax=0.47, discount= 0) {
 console.log(price, salesTax, discount)
}

func() // passing no arguments. An error is thrown

NOTE: if price is not passed then default value is the function invocation which throws an error

```


