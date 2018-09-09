---
layout: post
published: true
categories: react
title:   Eleven ways to Render
---


How do you render via React? 

Below are 11 ways.  After setting up the environment, add the following imports to . your index.js:

```
import React from 'react';
import ReactDOM from 'react-dom';
```

Method 1:  JSX variables or “elements”

JSX is a preprocessor step that adds XML syntax (self-descriptive markup) to JavaScript.
A React element is a variable that contains JSX.  It is the “smallest building block of React apps”.
Elements make up components, but they are not themselves components.
Below, we create an element that defines a tag, and we pass it to render():

```
const element = <h1> Damn! </h1>

ReactDOM.render(element, document.getElementById('root'));

``` 

Method 2:  Component Functions w/o Arguments

There are two kinds of components:

“component” functions, or  “stateless components” (below)
class components

1.  Below, we write a component function that returns a JSX
2.  We reference this component as the first argument in our render method: <Element />

represent components via a capital initial enclosed in a self-closing tag.


```
function Element() {
    return (<h1> Damn! </h1>)
}

ReactDOM.render(<Element />, document.getElementById('root'));

```

or rewriting the previous function for ES6:

```
var Element = () => {
     return (<h1> Damn! </h1>)
}
```

Method 3:  Component Functions w/ Argument

1. Below,  we create our component function that accepts a props object and returns it as part of the JSX.
Props objects must be in curly brackets, which JSX uses to evaluates JS expressions (any code resolving into a value: variables, functions, and objects).
2.  Define an element (the variable now) that contains:
contains the component function
defines the property (name) to the props object.
3. Pass the element to the render():


```
var Element = (props) => {
    return (<h1> Damn! {props.name}</h1>)
}

const now = <Element name="Jack" />;

ReactDOM.render(now, document.getElementById('root'));
```

Method 4:  Nested Component Functions w/ Argument

Below we write two component functions: Welcome and App.  App embeds Welcome four times, assigning a new property definition  (name) each time.

Because App contains Welcome, App is the parent and Welcome is the child component.

Here, the child defines the actual tag whereas the parent represents it and assigns value to its prop.


```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}

ReactDOM.render( <App />, document.getElementById('root'));
```

Method 5:  Component Classes

Below, the class “copies” the properties and methods of React.Component module and adds a few more details: namely, the rendering of some JSX.

```
class Welcome extends React.Component {
   render() {
      return <h1>Hello </h1>;
   }
}
  
ReactDOM.render( <Welcome />, document.getElementById('root'));
```

Method 6:  Parent passes Props to Child class

The Child class returns JSX that relies on a property definition.

The Parent class returns:

The Child component
the property definition its (example = “foo” /)

```
class Parent extends React.Component {
   render() {
      return (
         <Child example="foo"/>
      )
   }
}

class Child extends React.Component {
   render() {
      return (
         <h1>{this.props.example}</h1>
      )
   }
}

ReactDOM.render(<Parent/>, document.getElementById('root'));
```

Method 7:  State passed to a class

Unlike component functions, component classes allows input of a private internal “state”.

State is an object, which can be changed, and when it does, the component auto re-renders to show the new state value.

Props cannot be changed

But like props, we can define state in our class and display it in our JSX:

```
class Parent extends React.Component {
  state= {
     count: 0,
     saying: "Damn"
   }

  render() {
    return (
      <h1>{this.state.saying}, I have {this.state.count} points </h1>
    )
  }
}

ReactDOM.render( <Parent />, document.getElementById('root'));
```

Method 8:   Props and States in Child class –

All variable references occur in curly braces.

In the Child, we:

create / assign a state.object
render this state object and the props object.

In the Parent, we:

render the Child and assign the prop property:

```
class Parent extends React.Component {
   render() {
      return (
         <Child example="foo"/>
      )
   }
}

class Child extends React.Component {
   state= {
      saying: "Damn!"
   }
  render() {
    return (
        <div>
            <h1>Inherited from Parent: {this.props.example}</h1>
            <h1>Defined by Child: {this.state.saying}</h1>
        </div>
    );
  }
}

ReactDOM.render(<Parent />, document.getElementById("root"));
```

Method 9:  Changing the Child state via a button click

setState() – used to change the state
onClick – the eventListener:
Child does the following:

assigns the state (state.count = 0)
creates a new function (event handler) that adds 1 to state.count
returns a button, which, when clicked, will fire the now function and display the current count
The parent renders the Child, passing in the props.title value

 
```
class Parent extends React.Component {

   render() {
      return (
         <Child title="Welcome" />
      ) 
   }
}

class Child extends React.Component {
   state= {
      count: 0
   }

   now= () => {
      this.setState({count: this.state.count +1})
   }

   render() {
        return (
            <div>
                <h1> Title: {this.props.title} </h1>
                <h1> Counter: {this.state.count} </h1>
            </div>
        )
    }
}

ReactDOM.render(<Parent/>, document.getElementById('root'));
```

method 10: using constructor()

method 11: passing from Child to Parent (reverse of the norm) using a callback:
class Parent extends React.Component {
    
    myCallback = (dataFromChild) => {
        console.log(dataFromChild)
    }

    render() {
        return (
             <Child callbackFromParent={this.myCallback}/>
        );
    }
}

class Child extends React.Component{
    state = { 
        value: ''
    }

    someFn = (e) => {
        e.preventDefault();  
        var newInput = e.target.value
        this.setState({
            value: newInput
        })      

        this.props.callbackFromParent(this.state.value);
    }

    some = (e) => {
        this.setState({value: e.target.value})
    }

    render() {
        return(
            <form onSubmit={this.someFn}>
            <label>
                Name:
                <input type="text" value={this.state.value} onChange={this.some} />
            </label>
            <input type="submit" value="Submit" />
            </form>
        )
    }
};

ReactDOM.render(<Parent />, document.getElementById('root'));

Process
  Parent calls child, passing a callback in callbackFromParent
  Child renders form whose value is this.state.value or “” (and is thus controlled)
  on Change, this.state.value becomes whatever is entered
  on Submit, this.state.value is sent to callback via SomeFn().  This callback had been stored in this.props.callbackFromParent.  It will console.log the submitted text.