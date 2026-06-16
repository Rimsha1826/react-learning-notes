# Lecture 8 - State Batching & Callback Updates
callback ..function k under function 
## Problem kya tha?
```jsx
const addValue = () => {
  setCounter(counter + 1)
  setCounter(counter + 1)
  setCounter(counter + 1)
  // Expected: 3 baar add ho
  // Actual: sirf 1 baar add hota hai!
}
```
Kyunki React saari updates ek saath bhejta hai — batching!

## Solution — Callback Function
```jsx
const addValue = () => {
  setCounter(prev => prev + 1)
  setCounter(prev => prev + 1)
  setCounter(prev => prev + 1)
  // Ab sahi — 3 baar add hoga!
}
```

## prev kya hai?
- React khud pichli value deta hai
- Hum uss pe kaam karte hain
- Har update sahi sequence mein hota hai

## Normal vs Callback farq
```jsx
// Normal — direct value
setCounter(counter + 1)

// Callback — previous value se
setCounter((prev) => prev + 1)
```

## JS Concept — Callback Function
- Ek function jo doosre function ke andar pass hota hai
```js
setCounter((prev) => prev + 1)
//          ^^^^^^^^^^^^^^^^^ — yeh callback hai
```

## Mujhe kya samjha
Jab ek saath multiple state updates karni hon —
hamesha callback form use karo taake
sahi sequence mein update ho!
