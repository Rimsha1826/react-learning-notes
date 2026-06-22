# Lecture 4 - React Behind the Scenes

## React isn't magic!
- It's just a structured JavaScript library
- We can even build a mini React ourselves

## What is a React Element?
A simple JavaScript object with 3 things:
- `type` - which HTML element (div, h1, etc)
- `props` - attributes (class, id, etc)
- `children` - the content inside

## customRender function (mini React)
```js
function customRender(reactElement, container) {
  const domElement = document.createElement(reactElement.type)
  domElement.innerHTML = reactElement.children
  domElement.setAttribute('href', reactElement.props.href)
  domElement.setAttribute('target', reactElement.props.target)
  container.appendChild(domElement)
}
```

## What is JSX actually?
- JSX is just a function call behind the scenes
- Babel converts JSX into `React.createElement()`
- This:
```jsx
<h1>Hello</h1>
```
- Is actually this:
```js
React.createElement('h1', null, 'Hello')
```

## What do curly braces {} do?
- Inside JSX, `{}` is used to write JavaScript expressions
- Like displaying a variable's value:
```jsx
const name = "Rimsha"
return <h1>Hello {name}</h1>
```

## Why is React.createElement better?
- Manual implementation requires handling all props manually
- React.createElement handles everything automatically
- Complex optimizations are already built in

## My takeaway
React is not magic - it's JavaScript objects that get
injected into the DOM. JSX is just a shortcut for
writing React.createElement.
