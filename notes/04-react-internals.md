# Lecture 4 - React Behind the Scenes

## React magical nahi hai!
- Yeh ek structured JavaScript library hai
- Hum khud bhi mini React bana sakte hain

## React Element kya hota hai?
Ek simple JavaScript object hota hai jisme 3 cheezein hoti hain:
- `type` — kaunsa HTML element hai (div, h1 etc)
- `props` — attributes (class, id etc)
- `children` — andar ka content

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

## JSX kya hai actually?
- JSX sirf ek function call hai behind the scenes
- Babel JSX ko `React.createElement()` mein convert karta hai
- Yeh:
```jsx
<h1>Hello</h1>
```
- Asliyat mein yeh hota hai:
```js
React.createElement('h1', null, 'Hello')
```

## Curly braces {} ka kaam
- JSX mein `{}` ke andar JavaScript expression likhte hain
- Jaise variable ki value dikhana:
```jsx
const name = "Rimsha"
return <h1>Hello {name}</h1>
```

## React.createElement kyun better hai?
- Manual implementation mein sab props manually handle karne padte hain
- React.createElement automatically sab kuch handle karta hai
- Complex optimizations already built in hain

## Mujhe kya samjha
React koi magic nahi — yeh JavaScript objects hain jo 
DOM mein inject hote hain. JSX sirf shortcut hai 
React.createElement likhne ka.
