 
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
