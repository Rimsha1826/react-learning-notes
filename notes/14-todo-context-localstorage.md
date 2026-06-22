# Lecture 14 - Todo App with Context API & Local Storage

## What is the project?
A Todo app where you can add, edit, delete, and mark
tasks as complete - using Context API for state
management and localStorage so data survives a refresh.

## TodoContext.js - Setting up the Context

```js
import { createContext, useContext } from "react"

export const TodoContext = createContext()

export const useTodo = () => {
  return useContext(TodoContext)
}

export const TodoProvider = TodoContext.Provider
```

- `TodoContext` - the "box" that holds shared data
- `useTodo` - a custom hook (shortcut) so we don't have
  to write `useContext(TodoContext)` everywhere
- `TodoProvider` - a shortcut for `TodoContext.Provider`

## Named export vs default export
```js
// default export - only ONE thing per file
export default TodoContext

// named export - MULTIPLE things from one file
export const TodoContext = createContext()
export const useTodo = () => {...}
```
Named exports need curly braces when importing:
```js
import { TodoContext, useTodo } from "./TodoContext"
```

## App.jsx - The 4 core functions

### addTodo - adding a new todo
```jsx
const addTodo = (todo) => {
  setTodo((prev) => [{id: Date.now(), ...todo}, ...prev])
}
```
- `Date.now()` generates a unique id (current timestamp)
- `...todo` (spread operator) copies all properties from
  the todo object passed in
- New todo goes at the start, old todos (`...prev`) follow

### updateTodo - editing an existing todo
```jsx
const updateTodo = (id, todo) => {
  setTodo((prev) => prev.map((prevTodo) => (prevTodo.id === id ? todo : prevTodo)))
}
```
- `.map()` loops through every todo
- Ternary operator: `condition ? (if true) : (if false)`
- If the id matches, replace with the new todo, otherwise
  keep the old one unchanged

### deleteTodo - removing a todo
```jsx
const deleteTodo = (id) => {
  setTodo((prev) => prev.filter((todo) => todo.id !== id))
}
```
- `.filter()` keeps only the items where the condition is
  true - so the matching id gets removed

### toggleComplete - marking complete/incomplete
```jsx
const toggleComplete = (id) => {
  setTodo((prev) => prev.map((prevTodo) => (prevTodo.id === id ? {...prevTodo, completed: !prevTodo.completed} : prevTodo)))
}
```
- `!prevTodo.completed` flips true to false or false to true
- `{...prevTodo, completed: ...}` keeps all other data the
  same, only changes `completed`

## Wrapping the app with the Provider
```jsx
<TodoProvider value={{todo, addTodo, updateTodo, deleteTodo, toggleComplete}}>
  {/* all components inside can access these */}
</TodoProvider>
```

## TodoForm.jsx - adding new todos
```jsx
const { addTodo } = useTodo()

const add = (e) => {
  e.preventDefault()
  if (!todo) return
  addTodo({ todo, completed: false })
  setTodo("")
}
```
- Gets `addTodo` directly from Context - no props needed
- `if (!todo) return` stops submission if input is empty

## TodoItem.jsx - displaying and editing a todo
```jsx
const { updateTodo, deleteTodo, toggleComplete } = useTodo()
```
- Pulls all 3 functions straight from Context
- Has its own local state to track if it's in edit mode
- Calls `updateTodo`, `deleteTodo`, `toggleComplete` when
  the relevant buttons are clicked

## localStorage - making data persistent

### Loading data when the page first loads
```jsx
useEffect(() => {
  const todos = JSON.parse(localStorage.getItem("todos"))
  if (todos && todos.length > 0) {
    setTodo(todos)
  }
}, [])
```
- Empty dependency array `[]` - runs only once, on load
- `localStorage.getItem()` returns a string
- `JSON.parse()` converts that string back into an array/object

### Saving data whenever todos change
```jsx
useEffect(() => {
  localStorage.setItem("todos", JSON.stringify(todo))
}, [todo])
```
- Runs every time `todo` state changes
- `JSON.stringify()` converts the array/object into a
  string (localStorage can only store strings)

## My takeaway
Context API lets multiple components (TodoForm, TodoItem)
share and update the same data without passing props
through every level. localStorage + useEffect makes data
survive a page refresh - stringify to save, parse to load.
