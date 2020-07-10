// 🤔 since console.log returns undefined we get props returned as well as console.log too
const arr = (props) => console.log(props) || props

#### arrow functions have no `this` keyword of their own, they find it lexically just like any other variable.
