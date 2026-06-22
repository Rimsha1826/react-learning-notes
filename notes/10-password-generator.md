# Lecture 10 - Password Generator Project

## What is the project?
Generate a random password based on user settings
(length, numbers, special characters), and copy it to
the clipboard with a "Copy" button.

## 3 New Hooks Learned

### 1. useCallback
Memoizes a function - it only creates a new function
when a dependency changes, otherwise the old one is
reused. Improves performance.
```jsx
const generatePassword = useCallback(() => {
  // logic
}, [length, numberAllowed, charAllowed])
```

### 2. useEffect
Automatically runs code when the page loads or when
values in the dependency array change.
```jsx
useEffect(() => {
  generatePassword()
}, [length, numberAllowed, charAllowed, generatePassword])
```

### 3. useRef
Creates a direct reference/address to an HTML element -
without causing a re-render. Used here to select the
input box.
```jsx
const passwordRef = useRef(null)
<input ref={passwordRef} />
```

## Password Generation Logic
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
- Mixed all allowed characters into one `str`
- Used a loop to pick a random position and character
- Added it to `pass` each time

## Copy to Clipboard Logic
```jsx
passwordRef.current?.select()
window.navigator.clipboard.writeText(password)
```
- `select()` - highlights the input's text
- `clipboard.writeText()` - actually copies to clipboard

## JS Concepts used
- `Math.random()` - random decimal number (0-1)
- `Math.floor()` - rounds a decimal down
- `for loop` - to repeat an action
- `+=` - add to an existing value
- `?.` - optional chaining (safety check)

## My takeaway
useCallback remembers a function, useEffect automatically
runs code when settings change, and useRef gives a direct
reference to an element without causing a re-render.
