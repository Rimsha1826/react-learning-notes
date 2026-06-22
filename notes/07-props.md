# Lecture 7 - Props & Tailwind CSS

## What is Props?
- A way to pass data from a parent component to a child component
- Props = Properties

## Using Props
```jsx
// Parent - sends data
function App() {
  return <Card name="Rimsha" age="22" city="Jauharabad"/>
}

// Child - receives data
function Card(props) {
  return (
    <>
      <h2>{props.name}</h2>
      <p>{props.age}</p>
      <p>{props.city}</p>
    </>
  )
}
```

## Props Destructuring - cleaner way
```jsx
function Card({ name, age, city }) {
  return (
    <>
      <h2>{name}</h2>
      <p>{age}</p>
      <p>{city}</p>
    </>
  )
}
```

## Default Props - in case data is missing
```jsx
function Card({ name = "Guest", age = "N/A" }) {
  return <h2>{name} - {age}</h2>
}
```

## JS Concept - Object Destructuring
```js
// Old way
const name = person.name
const age = person.age

// Shortcut
const { name, age } = person
```

## Tailwind CSS
- Uses utility classes for styling
- No need to write a separate CSS file
```jsx
<div className="bg-green-400 rounded-xl p-4">
  Hello
</div>
```

## My takeaway
Props make components reusable - the same component can
be used with different data in different places!
