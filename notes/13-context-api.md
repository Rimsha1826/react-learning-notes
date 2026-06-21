# Lecture 13 - Context API

## Problem — Prop Drilling
Jab data ek component se bohot neeche wale component
tak pahunchana ho, har beech wale component se "guzarna"
padta hai — chahe unhe data ki zaroorat na ho.

```jsx
App → <Page name="Rimsha" />
Page → <Header name={name} />
Header → <UserProfile name={name} />
```
Page aur Header ko name ki zaroorat nahi thi, sirf carry
kar rahe the.

## Solution — Context API
Data ko "globally available" banata hai — direct us
component tak pahunchta hai jisko zaroorat hai, beech
walon ko involve kiye bina.

## 3 Steps

### 1. Context banao
```js
import { createContext } from "react"
const UserContext = createContext()
export default UserContext
```
Yeh sirf ek khaali "box/address" banata hai.

### 2. Provider banao — data ko available karo
```jsx
import { useState } from "react"
import UserContext from "./UserContext"

const UserContextProvider = ({ children }) => {
  const [user, setUser] = useState(null)

  return (
    <UserContext.Provider value={{ user, setUser }}>
      {children}
    </UserContext.Provider>
  )
}

export default UserContextProvider
```
- state banaya jo data store karega
- Provider se woh data "available" kiya
- children = jo bhi components iske andar wrap honge

### 3. useContext se data lo (jahan zaroorat ho)
```jsx
import { useContext } from "react"
import UserContext from "../context/UserContext"

const { user, setUser } = useContext(UserContext)
```

## children prop kya hai?
Special prop — jo bhi JSX kisi component ke ANDAR likha
ho, woh automatically "children" mein aa jata hai.

```jsx
<UserContextProvider>
  <App />   {/* yeh hai children */}
</UserContextProvider>
```

## Poora flow ek example se
```jsx
// App.jsx — Provider se sab wrap kiya
<UserContextProvider>
  <Login />
  <Profile />
</UserContextProvider>

// Login.jsx — data SET karta hai
const { setUser } = useContext(UserContext)
setUser({ username, password })

// Profile.jsx — data USE karta hai
const { user } = useContext(UserContext)
<h2>Welcome, {user.username}</h2>
```
Login aur Profile ek doosre se directly connected nahi
hain — dono sirf UserContext se baat karte hain!

## Mujhe kya samjha
Context ek shared storage jaisa hai jahan koi bhi
component (jo Provider ke andar hai) data daal sakta hai
ya nikal sakta hai — bina props pass kiye. children
prop wrapper components banane ke liye use hota hai.
