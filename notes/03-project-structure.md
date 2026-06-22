# Lecture 3 - Project Structure & React Flow

## What does a browser understand?
- Only HTML and JavaScript
- React must be explicitly injected into the DOM

## What is a Single Page Application (SPA)?
- There is only ONE index.html for the entire app
- React dynamically updates the DOM
- No multiple pages load - everything happens on a single page

## React's lifecycle (flow)
1. `index.html` - has a div with `id="root"`
2. `main.jsx` - uses createRoot() to grab that div
3. React injects its components into that div

## What is the Virtual DOM?
- React creates its own copy of the DOM - in memory
- When something changes - the Virtual DOM updates first
- Then it compares with the actual DOM
- Only updates what has changed - this makes it fast

## CRA vs Vite
- CRA: react-scripts injects automatically - heavy
- Vite: manual and direct - fast and lightweight

## Component creation rules
- File name should start with a capital letter - `Chai.jsx`
- Use `.jsx` extension, not `.js`
- Component name should be capitalized - `function Chai()`
- Use Fragment when returning multiple elements:
```jsx
return (
  <>
    <h1>Hello</h1>
    <p>World</p>
  </>
)
```

## My takeaway
React gets injected into a single div - the entire app runs
inside that one div. React is fast because of the Virtual DOM.
