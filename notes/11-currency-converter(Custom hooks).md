# Lecture 11 - Currency Converter Project

## What is the project?
Fetch live currency rates from an API and convert one
currency to another, along with a swap feature.

## New Concept - Custom Hook
Building your own reusable hook - the name starts with
`use`. Keeps common logic in one place.

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

## What is an API?
A way for two systems to exchange data.
- REST API - modern, JSON format, lightweight
- SOAP API - older, XML format, complex

## fetch() and .then()
```js
fetch('url')
  .then((res) => res.json())      // convert response to JSON
  .then((res) => setData(res))    // save the data
```
- fetch() sends the request
- .then() means "when the response arrives, do this"

## useId Hook (new)
Generates a unique ID - when a component is used multiple
times (like InputBox for both From and To), each instance
gets its own unique id.

```jsx
const amountInputId = useId()
<label htmlFor={amountInputId}>...</label>
<input id={amountInputId} />
```

## Object.keys()
Extracts all keys (names) of an object into an array.
```js
let obj = {usd: 1, pkr: 278}
Object.keys(obj)  // ["usd", "pkr"]
```

## Reusable Component - InputBox
Used the same component for both "From" and "To" fields -
passed different data through props.

## My takeaway
Custom hooks make code reusable. Fetching data from an
API happens through useEffect + fetch + .then(). useId
gives unique IDs when the same component is used multiple
times.
