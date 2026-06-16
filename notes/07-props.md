# Lecture 7 - Props & Tailwind CSS

## Props kya hai?
- Parent component se child component ko data bhejne ka tarika
- Props = Properties

## Props use karna
```jsx
// Parent — data bhejta hai
function App() {
  return <Card name="Rimsha" age="22" city="Jauharabad"/>
}

// Child — data receive karta hai
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

## Props Destructuring — clean tarika
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

## Default Props — agar data na mile
```jsx
function Card({ name = "Guest", age = "N/A" }) {
  return <h2>{name} - {age}</h2>
}
```

## JS Concept — Object Destructuring
```js
// Purana tarika
const name = person.name
const age = person.age

// Shortcut
const { name, age } = person
```

## Tailwind CSS
- Utility classes use karte hain styling ke liye
- Alag CSS file likhne ki zaroorat nahi
```jsx
<div className="bg-green-400 rounded-xl p-4">
  Hello
</div>
```

## Mujhe kya samjha
Props se components reusable bante hain — ek hi 
component alag alag data ke saath use kar sakte hain!
