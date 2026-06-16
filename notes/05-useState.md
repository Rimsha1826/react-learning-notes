# Lecture 5 - useState Hook

## Problem kya tha?
Normal JavaScript variable UI update nahi karta:
```js
let counter = 0
counter = counter + 1  // value change hoti hai
// lekin screen pe kuch nahi badlta!
```

## Solution — useState Hook
```jsx
import { useState } from 'react'

const [counter, setCounter] = useState(0)
```
- `counter` — current value
- `setCounter` — value change karne ka function
- `0` — starting value (jo bhi starting value chahiye woh likhو)

## useState mein kya kya likh sakte hain?
```js
useState(0)       // Number
useState("")      // String
useState(false)   // Boolean
useState([])      // Array
useState({})      // Object
```

## Kaise kaam karta hai?
1. `setCounter()` call karo
2. React automatically re-render karta hai
3. Screen pe updated value dikh jaati hai

## Counter App Example
```jsx
import { useState } from 'react'

function Counter() {
  const [counter, setCounter] = useState(0)

  const addValue = () => {
    if(counter < 20) setCounter(counter + 1)
  }

  const decreaseValue = () => {
    if(counter > 0) setCounter(counter - 1)
  }

  return (
    <>
      <h2>Counter: {counter}</h2>
      <button onClick={addValue}>Add Value</button>
      <button onClick={decreaseValue}>Decrease Value</button>
    </>
  )
}
```

## JS Concepts jo is lecture mein use hue

### 1. Array Destructuring
```js
// useState array return karta hai
const [counter, setCounter] = useState(0)
// counter = value
// setCounter = function
```

### 2. Arrow Functions
```js
const addValue = () => {
  setCounter(counter + 1)
}
```

## Mujhe kya samjha
useState ek hook (function) hai jo React ko batata hai
ke value badli hai — screen update karo!
Normal variable se yeh kaam nahi hota.
