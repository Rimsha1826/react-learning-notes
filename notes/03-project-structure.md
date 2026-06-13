# Lecture 3 - Project Structure & React Flow

## Browser kya samajhta hai?
- Sirf HTML aur JavaScript
- React ko explicitly HTML mein inject karna parta hai

## Single Page Application (SPA) kya hai?
- Sirf EK index.html hoti hai poori app mein
- React DOM ko dynamically update karta hai
- Multiple pages load nahi hote — sirf ek page pe sab kuch hota hai

## React ka lifecycle (flow)
1. `index.html` — ek div hoti hai `id="root"`
2. `main.jsx` — createRoot() us div ko pakadta hai
3. React apni components us div mein inject karta hai

## Virtual DOM kya hai?
- React apna ek copy banata hai DOM ka — memory mein
- Jab kuch change hota hai — pehle Virtual DOM update hota hai
- Phir actual DOM se compare karta hai
- Sirf jo change hua woh update karta hai — fast hota hai

## CRA vs Vite
- CRA: react-scripts automatically inject karta hai — heavy
- Vite: manually aur directly — fast aur lightweight

## Component banane ke rules
- File naam Capital se shuru ho — `Chai.jsx`
- Extension `.jsx` use karo `.js` nahi
- Component naam Capital hona chahiye — `function Chai()`
- Multiple elements return karne ho toh Fragment use karo:
```jsx
return (
  <>
    <h1>Hello</h1>
    <p>World</p>
  </>
)
```

## Mujhe kya samjha
React ek div ke andar inject hota hai — poori app usi ek 
div mein chalti hai. Virtual DOM ki wajah se React fast hai.
