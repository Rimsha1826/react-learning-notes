# Lecture 6 - Virtual DOM, Reconciliation & React Fiber

## What is the Virtual DOM?
- React creates a copy of the actual DOM in memory
- When something changes - the Virtual DOM updates first
- Then it's compared with the actual DOM
- Only the changed part gets updated
- The whole page doesn't repaint - this makes it fast!

## What is Reconciliation?
- This is React's diffing algorithm
- It compares the Virtual DOM and the actual DOM
- Finds out - what has changed?
- Only updates that part

## What is React Fiber?
- React's modern reconciliation engine
- Gives better performance for animations and layout
- Does 2 things:
  - Incremental Rendering - breaks work into small chunks
  - Task Prioritization - does urgent work first, rest later

## Why are keys important?
- When rendering a list, we give each item a unique key
- This helps Fiber know which item changed
- Improves performance
```jsx
// ❌ Wrong - no key
items.map(item => <li>{item}</li>)

// ✅ Correct - has key
items.map(item => <li key={item.id}>{item}</li>)
```

## What is declarative thinking?
- In React, we think about "what the UI should look like"
- React itself handles "how to update it"
- We don't manually manipulate the DOM

## My takeaway
Virtual DOM → Reconciliation → Fiber - these three work
together to make React fast. Keys optimize performance
when rendering lists.
