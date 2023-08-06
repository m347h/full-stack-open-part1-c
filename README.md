 
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

## Stateful component 

This kind of important concept. 

all components have been simple that they have not contained any state that could change during lifecycle of the component
next, let's add state to our application's App w react's STATE HOOK 🪝

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
const [counter, setCounter ] = useState(0) // i think for state hooks 🪝, this line essential... 

setTimeout(
() => setCounter(counter+1),
1000
)

return (
<div>{counter}</div>
)
}
 ```


## Event handling ##


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
## An event handler is a function

we define the event handler for our button where we declare their onClick attributes:
```
<button onClick = {() => setCounter(counter+1)}>
plus 
</button>
```

but, this would not work. 
```
<button onClick={setCounter(counter + 1)}> 
  plus
</button>
```

and that would break the application. let's seperate the event handlers into seperate functions anway. 

SO, now as a problem to solve, you could implement 2 buttons, one that adds by 1 adn one that goes to 0 in const App..., while using the setCounter ... 

``` 

const App = () => {
const [ counter, setCounter] = useState(0)

const increaseBy1 = () => setCounter(counter+1)    // these are functions, thats why "= () => "

const zero = () => setCounter(0) // these are functions

return (
<div>

<button onClick = {increaseBy1}>
one
</button>

<button onClick = {zero}>
zero
</button>

</div>
)
}
 
```


## Passing state - to child components


recommended tow rite small and reusable componenets in React. so, let us refactor our application so that its composed of 3 small componenets. 

1-> displaying counter 

1-> displaying button1

1-> displaying button2



Let's first implement a Display component that's responsible for displaying the value of the counter.
```
const Display = (props) => {
return (
<div> {props.counter} </div>
)
}
```

hwo do u use it in the Apps function? in the return section, you would have: 

```
return(
<div>
<Display counter = {counter} />
</div>
)
```

everything still wokrks, when the buttons r clicked and he App gets re-rendered, all of its children including Display are re-rendered. 

now, let;s make a button component for the buttons of our application. We have to pass the event handler and the title of the button thru the componenet;s props. 

```
const Button = (props) => {
return (
<button onClick = {props.handleClick}>
{props.text}
</button>
)
}
```

we have to do that... and now, our App componenet looks like this: 

```
const App = () => {
  const [ counter, setCounter ] = useState(0)

  const increaseByOne = () => setCounter(counter + 1)

  const decreaseByOne = () => setCounter(counter - 1)
  const setToZero = () => setCounter(0)

  return (
    <div>
      <Display counter={counter}/>

      <Button
        handleClick={increaseByOne}
        text='plus'
      />
      <Button
        handleClick={setToZero}
        text='zero'
      />     
      <Button
        handleClick={decreaseByOne}
        text='minus'
      />           
    </div>
  )
}
```


## Changes in state cause rerendering

how does changes in state cause re-rendering. 
when application starts, the code in App is executed, then this code uses a useState hook to create applicaiton state, setting an initial val of the varaible counter. 

This component contains the Display component - which displays the counter's value, 0 - and three Button components.

 The buttons all have event handlers, which are used to change the state of the counter.
When one of the buttons is clicked, the event handler is executed.


 The event handler changes the state of the App component with the setCounter function. Calling a function that changes the state causes the component to rerender.

 So, if a user clicks the plus button, the button's event handler changes the value of counter to 1, and the App component is rerendered. 

 Display receives the new value of the counter, 1, as props. 
 
 The Button components receive event handlers which can be used to change the state of the counter.

const App = () => {
const [ counter, setCounter ] = useState(0)
console.log()

const increaseByOne = () => {
console.log('decreasing, value before ', counter)
setCounter (counter + 1); 
console.log('increasing, value after ', counter)


}


const decreaseByOne = () => {
console.log('decreasing, value before ', counter)

setCounter (counter - 1); 
console.log('decreasing, value after ', counter)

}


const Zero = () => {
setCounter (0); 
console.log('setting value to 0', counter)
}


return (
<div>
<Display counter = {counter} />
<Button handleClick = {increaseByOne} text="plus" />
 <Button handleClick = {decreaseByOne} text="minus" />
 <Button handleClick = {Zero} text="zero" />

 
</div> 
)

}


##refractoring components

The component displaying the value of the counter is as follows:


```

const Display = (props) => {
  return (
    <div>{props.counter}</div>
  )
}


```

The component only uses the counter field of its props. This means we can simplify the component by using destructuring, like so:

```
const Display = ({ counter }) => {
  return (
    <div>{counter}</div>
  )
}

```

The function defining the component contains only the return statement, so we can define the function using the more compact form of arrow functions:

```
const Display = ({ counter }) => <div>{counter}</div>
```

We can simplify the Button component as well.


```
const Button = (props) => {
return (
<button onClick = {props.handleClick} >
{props.text}
</button> 

)
}
)
}
```

We can use destructuring to get only the required fields from props, and use the more compact form of arrow functions:

```
const Button = ({ handleClick, text }) => (
<button onClick = {handleClick}>
{text}
</button>
)
```

dont oversimplify. 

