# Lecture 12 - React Router Basics

## Why do we need React Router?
React is an SPA (single HTML page) - Router gives the
feel of multiple pages, without an actual page reload.

## Link vs normal <a> tag
```jsx
// Normal tag - causes a page reload
<a href="/about">About</a>

// Link - no page reload
<Link to="/about">About</Link>
```

## NavLink - highlights the active page
```jsx
<NavLink
  to="/about"
  className={({ isActive }) => (isActive ? "text-yellow-400" : "text-white")}
>
  About
</NavLink>
```
isActive automatically becomes true if the user is on that page.

## Outlet - placeholder for changing content
The Layout (Header+Footer) stays fixed, only the content
in place of Outlet changes per page.
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

## createBrowserRouter - the routes map
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
- path - what the URL should be
- element - which component to show
- children - what appears in place of Outlet depending on the URL

## RouterProvider
```jsx
<RouterProvider router={router} />
```
Tells the entire app to follow this router (map).

## useParams - getting a dynamic value from the URL
When part of the URL is "variable", like a User ID.

```jsx
// Defining a dynamic path in the route
{ path: 'user/:userid', element: <User /> }

// Capturing that value inside the component
import { useParams } from 'react-router-dom'

function User() {
  const { userid } = useParams()
  return <h1>User ID: {userid}</h1>
}
```
`:userid` is a placeholder - it matches whatever value is
in the URL (like /user/Rimsha or /user/42).

## loader & useLoaderData - fetching data in advance
Fetches API data before the page renders, improving
performance and avoiding loading delays.

```jsx
// In the component file - creating a loader function
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
// Connecting the loader in the route
import Github, { githubInfoLoader } from './components/Github/Github'

{
  path: 'github',
  element: <Github />,
  loader: githubInfoLoader,
}
```

### What is async/await?
- `async` - tells the function "this will take time" (network call)
- `await` - "wait here until the response arrives, then continue"

```js
const githubInfoLoader = async () => {
  const response = await fetch('url')   // waits here
  return response.json()
}
```

### Normal useEffect vs Loader - the difference
**useEffect approach:**
```
Page loads -> Component shows (no data yet) ->
useEffect runs -> API call -> Data arrives -> Then it shows
```
The user sees a brief "loading" state.

**Loader approach:**
```
User clicks the link -> Loader fetches data first ->
Once data is ready -> Page shows (with the data)
```
A complete page with data shows right away.

## My takeaway
The Layout stays fixed (Header/Footer), only the Outlet's
content changes based on the URL. The Router is a map
that says what to show for which URL. useParams lets you
use dynamic parts of a URL in code. loader improves
performance because data is ready before the component
even renders.
