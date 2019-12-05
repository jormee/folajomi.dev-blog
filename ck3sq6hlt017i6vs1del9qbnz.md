## Props and Conditional Rendering

React allows us to build dynamic web applications which facilitates interaction between the app and users. In order to achieve this, different react components need to interact with each other to properly display app responsiveness to user interactions. This is achieved by the ability of react components to pass data to one another and re-render them based on changes to these data. In this article, we are going to learn about how to pass data from one component to another using _Props_. 

### Data Flow in React

> The flow of data in a react application is unidirectional  and flows from top to bottom on the component tree.

To understand this concept better, lets take a look at the picture of our todo app below:

![todo application highlighting all its components](https://thepracticaldev.s3.amazonaws.com/i/iifsne9t8daryjb30yqt.png)

In the app above, we indicate the different components in coloured boxes/rectangles. The unidirectional data flow concept simply means that data can only be passed from the parent to the child component and not the other way round. For example, in the todo app, data cannot be passed from the TodoList component (blue square) to the entire application's state, rather the application passes data to the TodoList component.

I know this might be a lot to take in, but this is the TL;DR version:
> Data can only be passed from a parent component to a child component.

Now let's talk about how data is passed from the parent to the child.

### Props

> Props are basically arguments to our react components that allows us to pass data from one component to another on the component tree.

Props are passed from the parent to the child as follows:
```js
// In the parent component

<ChildComponent data={data} />
```

This data can be accessed in ChildComponent via the props like so:

```js

// ChildComponent

const ChildComponent = (props) => {
    console.log(props.data); //returns the data passed from the parent component
}
```

In the case of our todo app, we write the following in our text editor

```js
const App = () => {
  const todos=['install react','create-react-app']
  return (
    <div className="App">
      <h1>Todos</h1>
      <TodoList todos={todos} />
    </div>
  );
}

const TodoList = (props) => {
  return(
    <ul>
      {
        props.todos.map(todo => <li key={props.todos.indexOf(todo)}>{todo}</li>)
      }
    </ul>
  )
}
```

In the code above the App component is the parent which defines the data and passes it down to the TodoList component. This data is then accessed in the TodoList component via props.

Now we can see a list of our todos

![Sbx1.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1575370433077/248KO5j5m.jpeg)

### Conditional Rendering

Now we have an (ugly) app that displays all our todos (as a list) :), but it renders a list of hard-coded todo. What happens if we delete all the dummy data in the todos array, leaving only an empty list? Excluding the Todo h1 element, we get a blank page that offers nothing to the user on what to do. We do not want our users staring at a blank page if they have not added a todo yet. Rather we want to display an instruction on how they can add a todo and remove this instruction once they have added one todo. This is a perfect job for an if statement, right? This operation is simply what Conditional Rendering is.

In react, conditional rendering is done the same we use conditionals in JavaScript using the if statement or the ternary operator ( ? : ). This is because...**Drumroll**... REACT is JS.

Let's see how we can solve our todo problem in code.

```js
const TodoList = (props) => {

  if(props.todos.length){

    return(
      <ul>
        {
          props.todos.map(todo => <li key={props.todos.indexOf(todo)}>{todo}</li>)
        }
      </ul>
    )
  }

  return <h3>No todo(s) yet, Use the form to create new todos</h3>
```
This can also be done using the ternary operator
```
const TodoList = (props) => {

  return props.todos.length?
    <ul>
      {
        props.todos.map(todo => <li key={props.todos.indexOf(todo)}>{todo}</li>)
      }
    </ul>
  : <h3>No todo(s) yet, Use the form to create new todos</h3>
}
```

If either of the TodoList Components above is used, we still get the same result shown in the image above. However, if we delete all the todos in our list, leaving only an empty array, we get this:


![Todo5.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1575549845230/eqy9phqsl.jpeg)

Now, when we add todos, the instruction disappears and gives way for our todo items. We'll look at how to add todos in our app later.

You can also edit the code and experiment on the code in [this sandbox](https://codesandbox.io/s/planned-rms6l)
You can also read more about [props](https://reactjs.org/docs/components-and-props.html) and [conditonal](https://reactjs.org/docs/conditional-rendering.html) rendering in the React docs.

> Please leave comments if you find any part of this post confusing or error or typos.