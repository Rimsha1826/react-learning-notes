# Lecture 9 - Background Color Changer Project

## Project kya hai?
Buttons click karke poori screen ka background color change karna

## Tech Stack
- React + Vite
- Tailwind CSS

## Core Logic
```jsx
const [color, setColor] = useState('olive')

<div style={{backgroundColor: color}}>
  <button onClick={() => setColor('red')}>Red</button>
</div>
```

## Important Concept — Callback zaroori kyun?
```jsx
// ❌ Galat — immediately execute hoga, click ka wait nahi karega
<button onClick={setColor('red')}>Red</button>

// ✅ Sahi — sirf click pe chalega
<button onClick={() => setColor('red')}>Red</button>
```

## Tailwind classes use hui
- `w-full h-screen` — full width/height
- `fixed` — position fixed rakhna
- `flex flex-wrap justify-center` — buttons center mein, wrap ho jayein
- `duration-200` — smooth color transition

## Mujhe kya samjha
State (color) change hote hi React automatically 
re-render karta hai aur naya background dikhata hai.
Callback function use karna zaroori hai onClick mein,
warna function page load hote hi chal jaata hai.
