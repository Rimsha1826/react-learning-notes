# Lecture 6 - Virtual DOM, Reconciliation & React Fiber

## Virtual DOM kya hai?
- React memory mein ek copy banata hai actual DOM ki
- Jab kuch change hota hai — pehle Virtual DOM update hota hai
- Phir actual DOM se compare karta hai
- Sirf jo part change hua — wahi update hota hai
- Poora page re-paint nahi hota — fast hota hai!

## Reconciliation kya hai?
- Yeh React ka diffing algorithm hai
- Virtual DOM aur actual DOM ko compare karta hai
- Dhundhta hai — kya kya change hua?
- Sirf wahi update karta hai

## React Fiber kya hai?
- React ka modern reconciliation engine hai
- Animations aur layout ke liye better performance deta hai
- 2 kaam karta hai:
  - Incremental Rendering — kaam ko chhote chunks mein tode hai
  - Task Prioritization — zaroori kaam pehle karta hai, baaki baad mein

## Keys kyun zaroori hain?
- List render karte waqt har item ko unique key dete hain
- Fiber ko pata chalta hai — kaunsa item change hua
- Performance better hoti hai
```jsx
// ❌ Galat — key nahi
items.map(item => <li>{item}</li>)

// ✅ Sahi — key hai
items.map(item => <li key={item.id}>{item}</li>)
```

## Declarative thinking kya hai?
- React mein hum sochte hain — "UI kaisi dikhni chahiye"
- React khud handle karta hai — "kaise update karna hai"
- Hum DOM manually manipulate nahi karte

## Mujhe kya samjha
Virtual DOM → Reconciliation → Fiber — yeh teeno milke
React ko fast banate hain. Keys list mein performance
optimize karti hain.     

## React mein exactly yahi hota hai:
User ne button click kiya
        ↓
Virtual DOM mein change hua (rough copy)
        ↓
Reconciliation ne compare kiya (kya badla?)
        ↓
Fiber ne smart tarike se sirf wahi update kiya
        ↓
Screen update ho gayi!
