# Lists and Keys

First, let’s review how you transform lists in JavaScript.

Given the code below, we use the map() function to take an array of numbers and double their values. We assign the new array returned by map() to the variable doubled and log it:

const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map((number) => number * 2);
console.log(doubled);
This code logs [2, 4, 6, 8, 10] to the console.

In React, transforming arrays into lists of elements is nearly identical.


## Rendering Multiple Components

Curly braces can be used to create collections of elements and include them in JSX.

Using the JavaScript map() function, we cycle through the numbers array below. For each item, we return a li> element. Finally, we assign listItems to the resulting array of elements:

const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li>{number}</li>
);

We include the entire listItems array inside a <ul> element, and render it to the DOM:

ReactDOM.render(
  <ul>{listItems}</ul>,
  document.getElementById('root')
);

## Basic List Component

Normally, lists would be rendered within a component.

The previous example can be refactored into a component that takes an array of integers and outputs a list of elements.

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li>{number}</li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);

When you run this code, you'll get a warning that a key for list items is required. When generating lists of elements, a "key" is a particular string attribute that must be included. In the next section, we'll go through why it's crucial.

Let's give our list items inside numbers a key.

Fix the missing key issue with map().

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li key={number.toString()}>
      {number}
    </li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);

## Keys
Keys help React identify which items have changed, are added, or are removed. Keys should be given to the elements inside the array to give the elements a stable identity:

const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li key={number.toString()}>
    {number}
  </li>
);
The best way to pick a key is to use a string that uniquely identifies a list item among its siblings. Most often you would use IDs from your data as keys:

const todoItems = todos.map((todo) =>
  <li key={todo.id}>
    {todo.text}
  </li>
);
When you don’t have stable IDs for rendered items, you may use the item index as a key as a last resort:

const todoItems = todos.map((todo, index) =>
  // Only do this if items have no stable IDs
  <li key={index}>
    {todo.text}
  </li>
);

If the order of items may change, we don't advocate utilizing indexes as keys. This can have a detrimental influence on performance and cause component state difficulties. For a detailed description of the drawbacks of using an index as a key, see Robin Pokorny's essay. If you don't set an explicit key to a list item, React will use indexes as the default key.

## Extracting Components with Keys
Keys only make sense in the context of the surrounding array.

For example, if you extract a ListItem component, you should keep the key on the <ListItem /> elements in the array rather than on the <li> element in the ListItem itself.

Example: Incorrect Key Usage

function ListItem(props) {
  const value = props.value;
  return (
    // Wrong! There is no need to specify the key here:
    <li key={value.toString()}>
      {value}
    </li>
  );
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // Wrong! The key should have been specified here:
    <ListItem value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
Example: Correct Key Usage

function ListItem(props) {
  // Correct! There is no need to specify the key here:
  return <li>{props.value}</li>;
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // Correct! Key should be specified inside the array.
    <ListItem key={number.toString()} value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);

## Keys Must Only Be Unique Among Siblings

Keys used within arrays should be unique among their siblings. However, they don’t need to be globally unique. We can use the same keys when we produce two different arrays:

function Blog(props) {
  const sidebar = (
    <ul>
      {props.posts.map((post) =>
        <li key={post.id}>
          {post.title}
        </li>
      )}
    </ul>
  );
  const content = props.posts.map((post) =>
    <div key={post.id}>
      <h3>{post.title}</h3>
      <p>{post.content}</p>
    </div>
  );
  return (
    <div>
      {sidebar}
      <hr />
      {content}
    </div>
  );
}

const posts = [
  {id: 1, title: 'Hello World', content: 'Welcome to learning React!'},
  {id: 2, title: 'Installation', content: 'You can install React from npm.'}
];
ReactDOM.render(
  <Blog posts={posts} />,
  document.getElementById('root')
);

Keys serve as a hint to React but they don’t get passed to your components. If you need the same value in your component, pass it explicitly as a prop with a different name:

const content = posts.map((post) =>
  <Post
    key={post.id}
    id={post.id}
    title={post.title} />
);

## Embedding map() in JSX

In the examples above we declared a separate listItems variable and included it in JSX:

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <ListItem key={number.toString()}
              value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}
JSX allows embedding any expression in curly braces so we could inline the map() result:

function NumberList(props) {
  const numbers = props.numbers;
  return (
    <ul>
      {numbers.map((number) =>
        <ListItem key={number.toString()}
                  value={number} />
      )}
    </ul>
  );
}

Sometimes this results in clearer code, but this style can also be abused. Like in JavaScript, it is up to you to decide whether it is worth extracting a variable for readability. Keep in mind that if the map() body is too nested, it might be a good time to extract a component.

-----------------------------------------------------------------

## spread operator

The spread operator is a convenient and fast way to add items to arrays, combine arrays or objects, and spread an array across a function's arguments.

What exactly is a spread operator?

Spread syntax in JavaScript refers to the usage of a three-dot ellipsis (...) to expand an iterable object into a list of parameters.
“The function call ‘expands' an iterable object arr into the list of arguments when...arr is used.
The spread operator, like the rest parameters, was added to JavaScript in ES6 (ES2015), with the same syntax: three magic dots....

### What is ... used for?

“To the rescue, a spread operator! It appears to be similar to rest parameters, as it likewise uses..., but it has the opposite effect.”

Take trying to find the largest number in an array with Math.max():

Math.max(1,3,5) // 5
Math.max([1,3,5]) // NaN

### What else can … do?

In JavaScript, the... spread operator is useful for a variety of purposes, including the following:

+ Array duplication
+ Combining or concatenating arrays
+ Making use of math functions
+ The use of an array as a set of arguments
+ Adding something to a list
+ In React, adding to a state
+ Objects being combined
+ NodeList to Array Conversion

The spread syntax expands an iterable object, often an array, but it can be used on any interable, even a string, in any case.

### Examples of using …

I explain copying an array, breaking a string into characters, and combining the properties of two JavaScript objects in a handful of basic examples of utilizing... in JavaScript:

[...["😋😛😜🤪😝"]] // Array [ "😋😛😜🤪😝" ]
[..."🙂🙃😉😊😇🥰😍🤩!"] // Array(9) [ "🙂", "🙃", "😉", "😊", "😇", "🥰", "😍", "🤩", "!" ]

const hello = {hello: "😋😛😜🤪😝"}
const world = {world: "🙂🙃😉😊😇🥰😍🤩!"}

const helloWorld = {...hello,...world}
console.log(helloWorld) // Object { hello: "😋😛😜🤪😝", world: "🙂🙃😉😊😇🥰😍🤩!" }

### Copying an array

It's simple to clone or combine arrays with the... spread operator, and it can even add additional items:

const fruits = ['🍏','🍊','🍌','🍉','🍍']
const moreFruits = [...fruits];
console.log(moreFruits) // Array(5) [ "🍏", "🍊", "🍌", "🍉", "🍍" ]
fruits[0] = '🍑'
console.log(...[...fruits,'...',...moreFruits]) //  🍑 🍊 🍌 🍉 🍍 ... 🍏 🍊 🍌 🍉 🍍

### Concatenating arrays

The spread operator, as seen in the previous example, can swiftly merge two arrays, a process known as array concatenation:

const myArray = [`🤪`,`🐻`,`🎌`]
const yourArray = [`🙂`,`🤗`,`🤩`]
const ourArray = [...myArray,...yourArray]
console.log(...ourArray) // 🤪 🐻 🎌 🙂 🤗 🤩

### Using Math functions

The set of functions in the Math object are a great example of using the spread operator as the lone argument to a function.

one of the best ways to understand the use of spread operator in JavaScript is to look at the the built-in functions Math.min() and Math.max(), which both expect a list of arguments, not an array.

const numbers = [37, -17, 7, 0]
console.log(Math.min(numbers)) // NaN
console.log(Math.min(...numbers)) // -17
console.log(Math.max(...numbers)) // 37

### Using an array as arguments

Since the spread operator “spreads” an array into different arguments, any functions that accepts multiple any number of arguments can benefit from use of the spread operator.

const fruitStand = ['🍏','🍊','🍌']
const sellFruit = (f1, f2, f3) => { console.log(`Fruits for sale: ${f1}, ${f2}, ${f3}`) }
sellFruit(...fruitStand) // Fruits for sale: 🍏, 🍊, 🍌
fruitStand.pop()
fruitStand.pop()
fruitStand.push('🍉')
fruitStand.push('🍍')
sellFruit(...fruitStand) // Fruits for sale: 🍏, 🍉, 🍍
fruitStand.pop()
fruitStand.pop()
sellFruit(...fruitStand,'🍋') // Fruits for sale: 🍏, 🍋, undefined

### Adding an item to a list

Asnoted in the last example, the spread operator can add an item to an another array with a natural, easy-to-understand syntax:

const fewFruit = ['🍏','🍊','🍌']
const fewMoreFruit = ['🍉', '🍍', ...fewFruit]
console.log(fewMoreFruit) //  Array(5) [ "🍉", "🍍", "🍏", "🍊", "🍌" ]

### Adding to state in React

Adding an item to an array in React state is easily accomplished using the spread operator. 

import React, { useState } from "react"
import ReactDOM from "react-dom"

import "./styles.css"

function App() {
  // React Hooks declarations
  const [searches, setSearches] = useState([])
  const [query, setQuery] = useState("")

  const handleClick = () => {
    // Add the search term to the list onClick of Search button
    // (Actually searching would require an API call here)

    // Save search term state to React Hooks
    setSearches(searches => [...searches, query])
  }
  
  // ...

### Combining objects

The spread syntax is useful for combining the properties and methods on objects into a new object:

const objectOne = {hello: "🤪"}
const objectTwo = {world: "🐻"}
const objectThree = {...objectOne, ...objectTwo, laugh: "😂"}
console.log(objectThree) // Object { hello: "🤪", world: "🐻", laugh: "😂" }
const objectFour = {...objectOne, ...objectTwo, laugh: () => {console.log("😂".repeat(5))}}
objectFour.laugh() // 😂😂😂😂😂
