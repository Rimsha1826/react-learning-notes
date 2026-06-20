# Lecture 12 - React Router Basics

## React Router kyun chahiye?
React SPA hai (single HTML page) — Router fake multiple
pages ka feel deta hai, bina actual page reload kiye.

## Link vs normal <a> tag
```jsx
// Normal tag — page reload hota hai
<a href="/about">About</a>

// Link — page reload nahi hota
<Link to="/about">About</Link>
```

## NavLink — active page highlight karta hai
```jsx
<NavLink
  to="/about"
  className={({ isActive }) => (isActive ? "text-yellow-400" : "text-white")}
>
  About
</NavLink>
```
isActive automatically true hota hai agar user usi page pe hai.

## Outlet — placeholder for changing content
Layout (Header+Footer) fix rehta hai, Outlet ki jagah
har page ka content change hota hai.
```jsx
function Layout() {
  return (
    <div>
      <Header />
      <Outlet />
      <Footer />
    </div>
  )
}
```

## createBrowserRouter — Routes ka naqsha
```jsx
const router = createBrowserRouter([
  {
    path: '/',
    element: <Layout />,
    children: [
      { path: '', element: <Home /> },
      { path: 'about', element: <About /> },
      { path: 'contact', element: <Contact /> },
    ],
  },
])
```
- path — URL kya hona chahiye
- element — konsa component dikhana hai
- children — Outlet ki jagah kya aayega depend karta hai URL pe

## RouterProvider
```jsx
<RouterProvider router={router} />
```
Poori app ko batata hai ke yeh router (naqsha) follow karo.

## useParams — URL se dynamic value lena
Jab URL ka koi part "variable" ho, jaise User ID.

```jsx
// Route mein dynamic path define karna
{ path: 'user/:userid', element: <User /> }

// Component mein woh value pakadna
import { useParams } from 'react-router-dom'

function User() {
  const { userid } = useParams()
  return <h1>User ID: {userid}</h1>
}
```
`:userid` ek placeholder hai — URL mein jo bhi value ho
(jaise /user/Rimsha ya /user/42), usi se match ho jata hai.

## loader & useLoaderData — Pehle se data fetch karna
Page render hone se pehle hi API data fetch kar leta hai,
performance better hoti hai, loading delay nahi dikhta.

```jsx
// Component file mein — loader function banate hain
export const githubInfoLoader = async () => {
  const response = await fetch('https://api.github.com/users/hiteshchoudhary')
  return response.json()
}

function Github() {
  const data = useLoaderData()
  return (
    <div>
      <img src={data.avatar_url} alt="user" />
      <p>Followers: {data.followers}</p>
      <p>Public Repos: {data.public_repos}</p>
    </div>
  )
}

export default Github
```

```jsx
// Route mein loader ko connect karna
import Github, { githubInfoLoader } from './components/Github/Github'

{
  path: 'github',
  element: <Github />,
  loader: githubInfoLoader,
}
```

### async/await kya hai?
- `async` — function ko batata hai "yeh time lega" (network call hai)
- `await` — "yahan ruko jab tak response na aaye, phir aage badho"

```js
const githubInfoLoader = async () => {
  const response = await fetch('url')   // yahan rukega
  return response.json()
}
```


### Normal useEffect vs Loader
- useEffect: Page dikhta hai → phir data aata hai (loading dikhta hai)
- loader: Data pehle aata hai → phir page dikhta hai (seedha complete page)

## Mujhe kya samjha
loader performance better karta hai kyunki data
component render hone se pehle hi ready hota hai.
useParams URL ke dynamic parts ko code mein use
karne deta hai.
