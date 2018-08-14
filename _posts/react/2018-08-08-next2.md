---
layout: post
published: true
categories: react
title:  Events
---

React has its own event handling system which is called Synthetic Events. Synthetic Events is a cross-browser wrapper of the browser’s native event. 

There are several standard DOM events, such as onClick, onKey, onDoubleClick, etc

In the render() method, we might have an onClick event: 

```javascript
    render(){
        ...
    
    <button onClick={this.handleIncrement} 
        className="btn btn-secondary btn-sm">
            Increment</button>
        ...
    }
```

which refers to a method of our own making for handling this event: 

```javascript
    handleIncrement() {
        console.log('Increment Clicked' , 
            this.state.count)
    }
```

Remember that 'this.state.count' refers to the state object in our class Counter: 

```javascript
  state = {
    count: 0,
  };
```

This would work fine if it weren't for the use of 'this' in that last method, which returns undefined. 

render() is considered a lifecycle method, along with others like componentWillMount, etc already define 'this' and so React knows which object to call on (in our case - 'Counter').

render() is called outside the component context so all this.functionName inside render method will refer to the window object.

Other methods, like event handlers, are treated differently.  These must bind their 'this' to the a specified object.  

We bind to 'this' to 'this' because 'this refers to the object context (whatever it is) from which the method call is derived.  so in a sense, we are re-defining 'this' anew because the keyword 'this' has lost its ability in this context. 

There are many ways of binding 'this'.  Cory House describes 5 approaches for handling ‘this’: https://medium.freecodecamp.org/react-binding-patterns-5-approaches-for-handling-this-92c651b5af56

Below are two ways. 

1) The easy way - use an arrow function in class property: 

```javascript
    handleIncrement = () => {
        console.log("increment clicked", 
            this.state.count)
    }
 ```

Apparently, these arrow functions lexically binds the this value for us. Arrow methods have the extra power of already inheriting 'this'.  Cory says: This technique relies upon the proposed class property feature. To use this approach, you must enable transform-class-properties or enable stage-2 in Babel.

2) A longer way is to bind in the constructor.  Here, we would leave the handleIncrement method as it was, and add a constructor: 


```javascript
    constructor() {
        super();
        this.handleIncrement = 
            this.handleIncrement.bind(this);
    }
```

So above, we return (to this.handleIncrement) a function call in which handleIncrement() is bound to the constructor's object context (the class Counter, Counter being an object).  This will do the job.  
 
On a side note, and as a 'bind' refresher: in Node, we would get undefined here: 

```javascript
var obj = {
    a:2
}

var a=3

function test() {
    console.log(this.a)
}

test()
```

But if we bound the test() call, we'd console.log '2': 


```javascript
var test = test.bind(obj)
```

If in node, we were able to use 'this' to refer to the global object...

```javascript
var test = test.bind(this)
```

We'd likely console.log '3'


Below are a few links on the topic: 

http://reactkungfu.com/2015/07/why-and-how-to-bind-methods-in-your-react-component-classes/


https://medium.freecodecamp.org/this-is-why-we-need-to-bind-event-handlers-in-class-components-in-react-f7ea1a6f93eb


https://www.google.com/search?q=why+does+this+work+in+render()+and+not+in+other+methods&rlz=1C5CHFA_enUS743US743&oq=why+does+this+work+in+render()+and+not+in+other+methods&aqs=chrome..69i57.9430j0j7&sourceid=chrome&ie=UTF-8



 

 