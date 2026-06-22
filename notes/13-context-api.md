# Lecture 13 - Context API

## Problem - Prop Drilling
When data needs to reach a component far down the tree,
it has to "pass through" every component in between -
even if they don't need that data.

```jsx
App -> <Page name="Rimsha" />
Page -> <Header name={name} />
Header -> <UserProfile name={name} />
```
Page and Header didn't need the name, they were just
carrying it along.

## Solution - Context API
Makes data "globally available" - it reaches directly to
the component that needs it, without going through every
component in between.

## 3 Steps

### 1. Create a Context
```js
import { createContext } from "react"
const UserContext = createContext()
export default UserContext
```
This just creates an empty "box/address".

### 2. Create a Provider - make the data available
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
- created state that will store the data
- made that data "available" through the Provider
- children = whatever components get wrapped inside this

### 3. Use useContext to get the data (wherever needed)
```jsx
import { useContext } from "react"
import UserContext from "../context/UserContext"

const { user, setUser } = useContext(UserContext)
```

## What is the children prop?
A special prop - whatever JSX is written INSIDE a
component automatically becomes its "children".

```jsx
<UserContextProvider>
  <App />   {/* this is children */}
</UserContextProvider>
```

## The full flow, with an example
```jsx
// App.jsx - wrapped everything with the Provider
<UserContextProvider>
  <Login />
  <Profile />
</UserContextProvider>

// Login.jsx - SETS the data
const { setUser } = useContext(UserContext)
setUser({ username, password })

// Profile.jsx - USES the data
const { user } = useContext(UserContext)
<h2>Welcome, {user.username}</h2>
```
Login and Profile aren't directly connected to each other
- they both just talk to UserContext.

## My takeaway
Context works like shared storage where any component
(inside the Provider) can put data in or take data out -
without passing props. The children prop is used to build
wrapper components.
