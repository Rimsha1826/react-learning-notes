# Lecture 5 - useState Hook

## What was the problem?
A normal JavaScript variable doesn't update the UI:
```js
let counter = 0
counter = counter + 1  // value changes
// but nothing changes on screen!
```

## Solution - useState Hook
```jsx
import { useState } from 'react'

const [counter, setCounter] = useState(0)
```
- `counter` - current value
- `setCounter` - function to change the value
- `0` - starting value (write whatever starting value you need)

## What can you write inside useState?
```js
useState(0)       // Number
useState("")      // String
useState(false)   // Boolean
useState([])      // Array
useState({})      // Object
```

## How does it work?
1. Call `setCounter()`
2. React automatically re-renders
3. The updated value shows on screen

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

## JS Concepts used in this lecture

### 1. Array Destructuring
```js
// useState returns an array
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

## full project counter-app (source code)
https://github.com/Rimsha1826/Counter-app

## My takeaway
useState is a hook (function) that tells React that a
value has changed - update the screen! A normal variable
can't do this.
