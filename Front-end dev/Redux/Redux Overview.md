---
banner: "https://dd.engineering/blog/a-practical-introduction-to-using-redux-with-react/banner.png"
---
# Redux overview 
### Action 
- It's just a plain JS object that há a `type` field 
- *Think of it as an event that describes sth that happened in the application*
###### Action Creators
- It's a function that creates and returns an action object.
### Reducers
- It's a function that receives the current `state` and `action` to decides how to update the state if necessary and returns the new state
- *Think of it as an event listener which handles events based on received action*
### Store 
- Current Redux application state lives in an object called store
- It's created by passing in a reducer
**EXP**
```javascript 
import { configureStore } from '@reduxjs/toolkit'

const store = configureStore({ reducer: counterReducer })

console.log(store.getState())
// {value: 0}
```
- How to create store => configureStore(*required reducer*)
##### Slice 
- It's collection of Redux reducer logic and actions for a single feature in the app
### Dispatch 
- It's a method that is the only way to update the state (pass and action object and called `dispatch()`)

### Selectors 
- There are functions that know how to extract specific pieces of information from a store state value.