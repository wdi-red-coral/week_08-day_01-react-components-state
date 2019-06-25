[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# React Component State

## Objectives

By the end of this, developers should be able to:

-  Identify when a component needs to have internal state.
-  Set an initial state of a component in the constructor.
-  Alter the state of a component through invoking setState.

## State in React Components

At this point, we know that we can pass data into a React component by providing
props. This allows data to flow "downwards", from parent component to child
component. Where does this data originate from, though? What if we need to
frequently update that data?

So far, that data has just been an array or object in the global scope of
`App.js`. This is not ideal for dynamic data -- if the data changes, every
component needs to know that, so that it can decide whether it needs to
re-render anything that's changed. To achieve this, React components keep track
of data in an object called "state".

## State vs. Props

`state` and `props` have a lot in common:

-  Both are POJOs.
-  Changes to a component's props or state cause the component's `render`
   method to be called.
-  Neither should be modified directly. (e.g. no `this.props.foo = 'bar'`)
-  Both are optional. A React component doesn't need props or state to render
   markup to the DOM (it wouldn't be very useful with neither, though).

They are also different in a few key ways:

-  Props are passed into a component from its parent. State is determined
   _within_ a component.
-  Props are initalized by adding attributes in JSX, e.g. `<MyComponent coolProp="radical!" />`. State is declared in a component's [`constructor`](https://reactjs.org/docs/react-component.html#constructor) method.
-  Props can only be modified in the parent component. State is modified in
   the component itself, with a call to `this.setState`.


## Demo: A stateful component

Let's take a look at an example of a React component that keeps
track of its own state. 

```js
class Header extends Component {
  state = {
      text: 'Welcome to React!'
  }

  render () {
    return (
      <div>
        <h1>{this.state.text}</h1>
      </div>
    )
  }
}
```

The example doesn't quite highlight why state is useful, but we will eventually see how that data could come from an API or be altered by the user's input.

### Update State with Events

State should not be data that is static.  It should be data that changes and alters what our component should render.  Sometimes state is updated based on an API call and the response from an API will update the state with new data.  Another way to update the state of a component is based on user input or actions.

We can create a click event that alters the state of our application.
```js
class Header extends Component {
  state = {
      text: 'Welcome to React!'
  }

  changeHeading = () => {
    this.setState({ text: "I am the new welcome message!"})
  }
  render () {
    return (
      <div>
        <h1 onClick={this.changeHeading}>{this.state.text}</h1>
      </div>
    )
  }
}
```

Anytime we run the `setState` method, our component will update it's state and then re-run the `render` method.

## Code-Along: Add option to "Like" a movie

Now that we know how to update state in a component, let's modify our `Movie`
component to allow us to "like" a movie and keep track of our opinions.

To add this functionality, we'll need to do the following:

- Give our `Movie` component `state`. The component should store just one property in its state: a boolean
   named `liked`.  It should default to `false`.
- Create a function that changes that `liked` property to `true`
- Render a "like" button with an `onClick`.
- Give some visual indication when a `Movie` is liked.

## Code-Along: Add option to "Like" or "Unlike" a movie

- Update your function to toggle the liked property on the state object between true and false.
- Give some visual indication when a Movie is liked or not liked.

## Lab: Toggle Actors Display

For some practice with state, add another method to our `Movie` component that
toggles a `hideActors` boolean on the state object. Only display information
about actors when the `hideActors` boolean is true.

**HINT:** You can use ternaries or `if` statements in JSX to display different
markup depending on whether a variable or expression is truthy.

## Code Along: Delete Movies

- Add the movies array to the state of the `App` component.
- Create a function in the `App` component that will remove a movie from the state based on its ID
- Pass that function as a prop to the `Movie` component
- Add a delete button in the `Movie` component that will use the delete movie function passed in as a prop

## Lab: Remove Actor

- Create a function in the `App` component that will remove an actor from the state based on the Movie ID and actor name.
- Pass that function as a prop to the `Movie` component
- Add a delete button in the `Movie` component that will use the delete actor function passed in as a prop

## Additional Resources

-   [React Docs - State and Lifecycle](https://reactjs.org/docs/state-and-lifecycle.html)
-   [CSS Tricks - React State From the Ground Up](https://css-tricks.com/react-state-from-the-ground-up/)

## [License](LICENSE)

1.  All content is licensed under a CC­BY­NC­SA 4.0 license.
1.  All software code is licensed under GNU GPLv3. For commercial use or
    alternative licensing, please contact legal@ga.co.
