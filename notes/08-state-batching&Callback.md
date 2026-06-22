# Lecture 8 - State Batching & Callback Updates

## What was the problem?
```jsx
const addValue = () => {
  setCounter(counter + 1)
  setCounter(counter + 1)
  setCounter(counter + 1)
  // Expected: increments 3 times
  // Actual: only increments once!
}
```
This happens because React batches all updates together.

## Solution - Callback Function
```jsx
const addValue = () => {
  setCounter(prev => prev + 1)
  setCounter(prev => prev + 1)
  setCounter(prev => prev + 1)
  // Now correct - increments 3 times!
}
```

## What is `prev`?
- React itself provides the previous (most recent) value
- We work on top of that value
- Each update happens in the correct sequence

## Normal vs Callback difference
```jsx
// Normal - direct value
setCounter(counter + 1)

// Callback - based on previous value
setCounter((prev) => prev + 1)
```

## JS Concept - Callback Function
- A function that is passed inside another function
```js
setCounter((prev) => prev + 1)
//          ^^^^^^^^^^^^^^^^^ - this is the callback
```

## My takeaway
When you need to perform multiple state updates at once,
always use the callback form so updates happen in the
correct sequence!
