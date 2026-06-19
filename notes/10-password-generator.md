# Lecture 10 - Password Generator Project

## Project kya hai?
User settings (length, numbers, special characters) ke
hisaab se random password generate karna, aur "Copy"
button se clipboard mein copy karna.

## 3 Naye Hooks Seekhe

### 1. useCallback
Function ko memoize karta hai — sirf dependency change
hone par naya function banta hai, warna purana reuse
hota hai. Performance better hoti hai.
```jsx
const generatePassword = useCallback(() => {
  // logic
}, [length, numberAllowed, charAllowed])
```

### 2. useEffect
Automatically code chalata hai jab page load ho ya
dependency array mein diye values change hon.
```jsx
useEffect(() => {
  generatePassword()
}, [length, numberAllowed, charAllowed, generatePassword])
```

### 3. useRef
Kisi HTML element ka direct reference/address banata hai
— bina re-render kiye. Input box ko select karne ke liye
use kiya.
```jsx
const passwordRef = useRef(null)
<input ref={passwordRef} />
```

## Password Generate Logic
```jsx
let pass = ''
let str = 'abc...XYZ'

if (numberAllowed) str += '0123456789'
if (charAllowed) str += '!@#$%^&*()_+'

for (let i = 1; i <= length; i++) {
  let char = Math.floor(Math.random() * str.length)
  pass += str.charAt(char)
}
setPassword(pass)
```
- Saare allowed characters ek `str` mein mix kiye
- Loop se random position choose ki, character nikala
- Har baar `pass` mein add kiya

## Copy to Clipboard Logic
```jsx
passwordRef.current?.select()
window.navigator.clipboard.writeText(password)
```
- `select()` — input ka text highlight karta hai
- `clipboard.writeText()` — actual clipboard mein copy karta hai

## JS Concepts use hue
- `Math.random()` — random decimal number (0-1)
- `Math.floor()` — decimal ko round down karta hai
- `for loop` — repeat karne ke liye
- `+=` — purani value mein naya add karna
- `?.` — optional chaining (safety check)

## Mujhe kya samjha
useCallback function ko yaad rakhta hai, useEffect
automatically kaam karta hai jab settings change hon,
aur useRef directly element ka address deta hai bina
re-render kiye.
