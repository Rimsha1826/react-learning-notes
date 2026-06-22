# Lecture 9 - Background Color Changer Project

## What is the project?
Clicking buttons changes the entire screen's background color

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

## Important Concept - Why is a callback needed?
```jsx
// ❌ Wrong - executes immediately, doesn't wait for a click
<button onClick={setColor('red')}>Red</button>

// ✅ Correct - only runs on click
<button onClick={() => setColor('red')}>Red</button>
```

## Tailwind classes used
- `w-full h-screen` - full width/height
- `fixed` - keep position fixed
- `flex flex-wrap justify-center` - buttons centered, wrap if needed
- `duration-200` - smooth color transition

## My takeaway
When state (color) changes, React automatically
re-renders and shows the new background. A callback
function must be used in onClick, otherwise the function
runs immediately when the page loads.
