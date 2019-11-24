## Building React Components I: Functional Components

Now that our react application is all set up, we can now start building components for our web page!!! 

![yay](https://media.giphy.com/media/11sBLVxNs7v6WA/giphy.gif)

We all know what react components are. If we don't or we've forgotten, let's have a little refresher in [this blog post](https://jormee.hashnode.dev/react-an-introduction-ck20hsam1001bnys1uakvgop7).

React components are of two types:

1. Functional Components

2. Class Components

We would be covering functional components in this post.

### What Are Functional Components?

> Fuctional components are the basic building blocks of React, they are the simplest components that can be created in react

How simple are they, really?

Functional  components are basically, JavaScript functions. They accept a single props (short for properties) argument and returns React elements. Let's take a look at how they really work:

```
const Hello = () => {
  return(
    <h1>Hello React</>
  )
}
```

As little as it is, the piece of code above is a valid react component which renders "Hello React" to the screen. However, this is not the full picture.

To get the full picture, lets create a new react app called bookstore by running

```
npx create-react-app bookstore
```

in the terminal and `cd` into the created bookstore project file at the end of the `create-react-app` process, then run:

```
npm start
```

to start our development server.

In our code editor, let's edit the App.js file, located in the src folder. Let's change the code so we have:

```
import React from 'react';

function App() {
  return (
    <div className="App">
      <h1>Welcome to the ReactJS Bookstore</h1>
      <p>It's nice to have you here</p>
    </div>
  );
}

export default App;
```

Let's go over our code one line at a time,

+ Line 1: The first line imports the React component from the react library, which gives us the ability to write JSX in our code.

+ Lines 3-10 define the function which returns our JSX. 

> It is very important to understand the naming convention for our react components. When creating a new react component, it is important to start our component name with an uppercase letter. This will be explained in detail along the line.

> Notice that we wrap our JSX in a div tag, this is because react functions can only return one component, therefore it does not support having adjacent elements without them being wrapped by another element. This way, the function only returns the `div` element

> Also, notice the `className` attribute on the div tag in line 5. This is the JSX equivalent of the html `class` attribute. This is written like this because class is a reserved keyword in JavaScript and since our react app is a JavaScript file, we cannot use the class keyword, hence the className attribute. 

+ The last line (10) in our little code exports the App component we created so it can be used in another file. Remember that our App.js file is actually imported and rendered in the index.js file.

The code above returns the following:

![welcome to our the react bookstore landing page](https://cdn.hashnode.com/res/hashnode/image/upload/v1574545106015/5GjbLVEz4.png)

Now we may be thinking, why go through all these hassle when I can actually recreate all we've done in pure html?

![be patient](https://media.giphy.com/media/3o7TKBjqwOlQYMirle/giphy.gif)

You'll appreciate react more when we cover rendering dynamic components. When? NOW!!!

### Rendering Dynamic Components

Now let's add a list of books we have in our bookstore to the page. How do we do these?
We could manually create a list and hard code all of the books in our store database into the JSX (and it would work). However, what happens if we have like 10,000 different books in our database, then we would type out `<li>bookname</li>` 10,000 times? Not efficient.

What we should do as developers is find a way to loop over the contents of the database and dynamically render each book in the database on our page, right? Luckily for us, react is JavaScript and JavaScript (ES6) provides the `map` function for us.

Let's do this in code:

![let's do this](https://media.giphy.com/media/3o72F03RnbPTvKtR7y/giphy.gif)

First, lets add the following array to our code to imitate our database. We could put it anywhere before the return statement, so let's put it on line 5, just before the return statement.

```
const books = ["Odd Thomas", "Harry Potter",  "The DaVinci Code", "The Lost Symbol", "Forever Odd", "Angels and Demons"]
```

Now we have six books in our database that we want to render in our react app. To do this, we will add the following code to line 11 of our code:

```
<ul>
    {
      books.map(book => <li key={books.indexOf(book)}>{book}</li>)
    }
</ul>
```

Let's go over the code:

The first line opens up a `ul` tag which indicates that an unordered list is coming next. The curly braces on the second line is to signify to react that what comes next is JavaScript i.e. if you want to write JavaScript code in the middle of JSX, it should be wrapped in curly braces.

The main code is written on the third line and it maps over the database and returns an `li` element that contains the name of each book in the database.

 You would notice, however, the `key` attribute specified on the `li` tag. This is a way for react to keep track of all the items/elements in a list so it would know which element is where in case we need to delete or edit a book. 

_The key for each element must be unique to the element and should not change. Generally, it is bad practice to use the index of the item as it's key because it may change and lead to inconsistencies in our app. Rather it is better to use an id library such as **[uuid](https://www.npmjs.com/package/uuid)** to create unique identifiers for each element in a list._

The code above returns the following:


![React app showing list of books](https://cdn.hashnode.com/res/hashnode/image/upload/v1574549649833/XZqtbyOKi.png)

I have separated the code onto separate lines to make sure that they are visible and easy to understand, but it could all fit in one line and read meaningfully, which would mean that in one line of code, we have extracted all the books in the database and rendered it in our application.

This was a long one, and I hope we take our times to fully understand the concepts introduced in this page. To further improve our knowledge, here is a [link to the official react documentation on functional components](https://reactjs.org/docs/components-and-props.html).

We will cover class components in the next blog post.