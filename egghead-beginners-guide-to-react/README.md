# This repo is a beginner's exploration into React

This repo is a place for my personal notes while taking Kent Dodd's "The Beginner's Guide to React" course on Egghead.io at https://egghead.io/courses/the-beginner-s-guide-to-react

See Egghead's Github repo at https://github.com/eggheadio-projects/the-beginner-s-guide-to-reactjs

Each lesson's code can be run by opening the HTML file in the browser. React and other JS is in script tags.
~

## Lesson 1

React creates an element with props. props is important.
Props is a dict.

createElement is

1. element we want to create
2. props we want to provide

## Lesson 2

Let's do better than React.createElement.
JSX!
Build system (webpack and babel) to convert JSX to html

JSX lets you more easily define markup dynamically.

custom attributes and then {...props} means props applies last
{...props} and then custom attributes means custom applies last

## Lesson 3

JSX composes better than function calls.
JSX compiles down to React.createElement(...) calls.
createElement can take anything that renders to a div.
So, either a div directly or a function and an object of props
Capital letters tell babel variable and not string

Children prop is an HTML thing that allows JSX to see the children of the DOM.

## Lesson 4

Typing is good. Use flow or reason

In the following

```
SayHello.propTypes = {
  firstName: PropTypes.string,
  lastName: PropTypes.string,
}
```

Proptypes.string gets its arguments from the props and context

## Lesson 5

dynamic rendering based on input validation is possible!

```
function Message({message}) {
  return (
    <div>
      {message ? ( // null?
        <div>{message}</div>
      ) : (
        <div>No Message</div>
      )}
    </div>
  )
}
```

Remember, JSX is just React.createElement which is just Javascript.

`{}` must accept an expression and if statements are not expressions.

## Lesson 6

Rerender a component:
wrap the rendering in a function
setInterval on the function

This is cool because React isn't updating the whole DOM, but just the parts that matter AND it maintains focus (good UI UX).

## Lesson 7

Styling is how we make things pretty
There's some differences between HTNL attributes and React Styling props. Such as, className vs class, kebab-case versus camelCase.
React does styling through props.

Be careful about overwriting certain props. Instead, work on merging them.

Good API design!

For vendor prefixing, make sure to use a 3rd party tool like emotion, styled-components, or glamorous.

PERSONAL NOTE: Styled-components supports react native, so it seems the best tool.

## Lesson 8

state is component internal data!
React manages event delegation <3
setState triggers a rerender

## Lesson 9

You can pull props from state. Update the state by returning a new state, otherwise just call setState with an object
Stateful class components! Neat. But there's a memory leak?

## Lesson 10

The memory leak is that we don't always clean up the setInterval.
`componentWillUnmount` is a method called before React removes a component from the page.

## Lesson 11

This binding can be tricky. A few solutions:
Do this.handleClick = this.handleClick.bind(this) in the constructor
Make the binding public (outside of teh constructor)
_BUT_
Arrow functions pass lexical `this` context. Use them for event handlers. It binds it to the instance, not the prototype.

## Lesson 12

To directly manipulate the DOM, pass as ref to the element, not the component (that will give a `this` reference, not a DOM node reference).

`ref={node => (this.rootNode = node)}` and then manipulate the DOM with said reference

```
componentDidMount() {
  VanillaTilt.init(this.rootNode, {
    max: 25,
    speed: 400,
    glare: true,
    'max-glare': 0.5,
  })
}
```

## Lesson 13

Forms!

`ref={node => (this.inputNode = node)}` on the input enables:

```
handleSubmit = event => {
    event.preventDefault() // stops the page refresh
    console.log(this.inputNode.value) // react only
  }
```

## Lesson 14

On a form, use onChange and an error state to have a dynamic form.

## Lesson 15

The goal is to sync multiple forms. We need to control the state of value of each input and update state.

A value prop on an input or textarea stops accepting user input. Thus onChange _has_ to be used. Use setState to update the state to rerender the form with the new value.

user input => state => render

## Lesson 16

All arrays need a key as an index (use an id). An array of objects of ids and values is best.
[
{id: ?, value: ??},
{id: ?, value: ??},
{id: ?, value: ??},
]

## Lesson 17

Async requests should happen in componentDidMount
