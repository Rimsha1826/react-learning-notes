# Lecture 11 - Currency Converter Project

## Project kya hai?
API se live currency rates fetch karke ek currency
ko doosri mein convert karna, saath mein swap feature.

## Naya Concept — Custom Hook
Apna khud ka reusable hook banana — naam `use` se start
hota hai. Common logic ek jagah rakhte hain.

```js
function useCurrencyInfo(currency) {
  const [data, setData] = useState({})

  useEffect(() => {
    fetch(`api-url/${currency}.json`)
      .then((res) => res.json())
      .then((res) => setData(res[currency]))
  }, [currency])

  return data
}
```

## API kya hai?
Do systems ke beech data exchange karne ka tarika.
- REST API — modern, JSON format, lightweight
- SOAP API — purana, XML format, complex

## fetch() aur .then()
```js
fetch('url')
  .then((res) => res.json())      // response ko JSON banao
  .then((res) => setData(res))    // data save karo
```
- fetch() request bhejta hai
- .then() "jab response aaye tab yeh karo"

## useId Hook (naya)
Unique ID generate karta hai — jab component multiple
baar use ho (jaise InputBox From aur To dono ke liye),
har ek ko alag unique id milti hai.

```jsx
const amountInputId = useId()
<label htmlFor={amountInputId}>...</label>
<input id={amountInputId} />
```

## Object.keys()
Object ki saari keys (names) ko array mein nikalta hai.
```js
let obj = {usd: 1, pkr: 278}
Object.keys(obj)  // ["usd", "pkr"]
```

## Reusable Component — InputBox
Ek hi component "From" aur "To" dono fields ke liye
use kiya — props se data alag-alag pass kiya.

## Mujhe kya samjha
Custom hooks se code reusable banta hai. API se data
fetch karna useEffect + fetch + .then() se hota hai.
useId multiple same components mein unique IDs deta hai.
