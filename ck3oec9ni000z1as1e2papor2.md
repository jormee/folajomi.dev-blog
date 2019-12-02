## Building React Components II: Class Components

In the [previous blog post](https://jormee.hashnode.dev/building-react-components-i-functional-components-ck3dm7mac00uno4s16y73oc3l), we said react components are of two types, and we talked about functional components.

This blog post will focus on the other type of react components - _class components_.

### What are class components?

> Class components are react components that are defined using ES6 classes.

We can create simple components (and complex ones too) using classes, by simply defining them in an ES6 class, as follows:

```js
class Hi extends React.Component {
    render() {
        return(<h1>Welcome to the React BookStore</h1>)
    }
}
```

This is the simplest form of a class component, and should return an `h1` saying "Welcome to the React BookStore". Everything in this component is very similar to our functional component except the `render()` method.

The render method is used to render DOM nodes and  is the only required* method in the class component. The class component may also contain other built-in methods called _Lifecycle Methods_, however these are optional. We will take a look at some important lifecycle methods in details later. First we look at State.

### State
The class component gives us access to state, which functional components did not (until the introduction of hooks in react 16.8). The state property of a component helps us track the  state of our components and enables us make appropriate changes to the application based on its state.

To use state in our react application, we define the property within the constructor function of our component class.

```js
class BookStore extends React.Component {
    constructor(props) {
        super(props);
        this.state={
            bookId: "",
            books: [],
            bookDetails: "",
        }
    }
    render(){
        return(
            <h1>Welcome to the React BookStore</h1>
        )
    }
}
```
> Note that the constructor function is also a *Lifecycle method* and should only be used when initializing state or binding methods. 

When using the constructor function, the `super(props)` should be called, else `this.props` will return undefined and may cause bugs in the app.

#### setState
This is a function that allows us to update the state of a react application. It is bad practice to reassign or edit the state of your app directly and this may cause bugs/inconsistencies in your app.
To update the state of a component, we call setState as follows:
```js
this.setState({bookId: "123"})
```
It is also important to avoid carrying out destructive operations (i.e. operations that directly mutate the state) such as `splice()` on the state object.

### What are Lifecycle Methods
> React Lifecycle methods are basically functions that we want to run at specific times in the life of our applications.

The following are some of the most important lifecycle methods react gives us access to:

#### 1. componentDidMount Method 

The `componentDidMount` method defines a function that we want to run when the component first mounts (i.e. the first time the component is rendered on the DOM). Let's say we want to fetch a list of books from our books database, we would like to define the function in the componentDidMount method, which fetches the required data once the component is mounted on the DOM.
In code, a call to fetch a list of pictures for our books would look like this:

```js
class BookStore extends React.Component {
    constructor(props) {
        super(props);
        this.state={
            bookId: "",
            books: [],
            bookDetails: "",
        }
    }
    componentDidMount(
        fetch('https://bookdatabase.com/photos')
           .then(response => response.json())
               .then(json => this.setState({books: [...json]}))
    )
     render(){
        return(
            <h1>Welcome to the React BookStore</h1>
        )
    }
```
This fetches all the pictures we need once the component mounts (renders for the first time)

#### 2. componentDidUpdate Method
This method is called when a component's state changes, i.e. the component has changed based on user input/interaction with the app. It takes the prevState(previous state) and/or prevProps(previous props) as arguments and runs makes appropriate changes to the DOM.

> It is important to note that you must use a conditional statement to setState within the componentDidUpdate method, else you will create an infinite loop.

This method can be used to make changes to the DOM to reflect user-input. For example, if you want to get details about a book that  a user selects. In code, this would look like:
```js
class BookStore extends React.Component {
    constructor(props) {
        super(props);
        this.state={
            bookId: "",
            books: [],
            bookDetails: "",
        }
    }
    componentDidMount(
        fetch('https://bookdatabase.com/photos')
           .then(response => response.json())
               .then(json => this.setState({books: [...json]}))
    )
    componentDidUpdate(prevState) {
    if(this.state.bookId !== prevState.bookId){
        fetch(`https://bookdatabase.com/books/${this.state.bookId}`)
            .then(response => response.json())
                .then(json => this.setState({bookDetails: json.details}))
    }
     render(){
        return(
            <h1>Welcome to the React BookStore</h1>
        )
    }
}
```
This code sets the book details to the details gotten from the network request only if there has been a change in the bookId. This is to ensure that no request is made when there is no change in the bookId which will cause an infinite loop.

#### 3. componentWillUnmount Method
The componentWillUnmount method is called when before a component is removed from the DOM. It is used to perform cleanups in our app, such as canceling network requests or subscriptions to services.

You can get more information about React Lifecycle methods in the [React docs]

[React docs]: (https://reactjs.org/docs/react-component.html)