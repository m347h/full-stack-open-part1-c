 
# full-stack-open-part1-c

# Component state, event handlers

new example, compoenent helper function, add another method so that we can guess the year of birth of the person being greeted. 
 ```
const Hello = (props) => {
const bornYear = () => {
const yearNow = newDate().getFullYear() 
return yearNow - props.age
}

return (
<div>
  <p>hello {props.name} you are {props.age} years old </p>
  <p>you are born in {bornYear()}</p>
</div>
)
}
 ```

we seperate the year of birth into a function of its own when component is rendered.
age does not have to B passed as you can access all props with props.age 

in JS, defining a fucntion within a function is a very common technique. unlike in JAVa, we dont do it. 

## Destructuring ##

this allows us to destructure values from objects and arrays upon assignment. 

instead of using {props.age} and {props.name} in the return(), you could isntead jsut define them constants! and use the name and age.
 ```
const name = props.name 
const age = props.age

return (
<div>
  <p>hello {name} you are {age}years old </p>
</div> 
)
 ```
also these 2 equiv! 
 ```
const bornYear = () => new Date().getFullYear() - age

const bornYear = () => {
  return new Date().getFullYear() - age
}
 ```

in addition, you may also do it this way: 

 ```
const Hello = (props) => {
  const { name, age } = props
  const bornYear = () => new Date().getFullYear() - age
 ```

"const { name, age } = props"

INSTEAD OF: 

"const name = props.name 
const age = props.age"

 ```
const Hello = ({ name, age }) => { 
  const bornYear = () => new Date().getFullYear() - age
 ```
the props that are passed to the component are now directly destructured into varaiables: name & age. 


## Page re-rendering## 

page re-rendering 

What if we wanted to create a counter where the value increased as a function of time or at the click of a button?

setIntercal() makes rendering more interesting!
 ```
setIntercal(() => {
refresh()
counter += 1 
}, 1000) 
}

 ```

##Stateful component##

all components have been simple that they have not contained any state that could change during lifecycle of the component
next, let's add state to our application's App w react's ##state hook##

index.js still the old few lines: 

 ```
import React from 'react'
import ReactDOM from 'react-dom/client'

import App from './App'

ReactDOM.createRoot(document.getElementById('root')).render(<App />)copy

 ```

App.js is changed to the following: 

 ```
import {useState} from 'React'

const App = () => {
const [counter, setCounter ] = useState(0)

setTimeout(
() => setCounter(counter+1),
1000
)

return (
<div>{counter}</div>
)
}
 ```


## Event handling##


event handlers are called when a specific event occur a few times . A user's interaction with the different elements of a web page can cause a collection of various kinds of events to be triggered.


Let's change the application so that increasing the counter happens when a user clicks a button, which is implemented with the button element.


In React, registering an event handler function to the click event happens like this:
```
const App = () => {

  const [ counter, setCounter ] = useState(0)


 const handleClick = () => {
    console.log('clicked')
  }


return (
    <div>
      <div>{counter}</div>
      <button onClick={handleClick}>
        plus
      </button>
    </div>
  )


}
```
We set the value of the button's onClick attribute to be a reference to the handleClick function defined in the code.

Now every click of the plus button causes the handleClick function to be called, meaning that every click event will log a clicked message to the browser console.

```
      <button onClick={() => console.log('clicked')}>

```
Let's also add a button for resetting the counter:

```
  <button onClick={() => setCounter(0)}> 
        zero
      </button>
```



