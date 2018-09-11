---
layout: post
published: true
categories: react
title:  Passing from Child to Parent
---

When the child state changes, we will: 
1. display the Child state
2. send to the Parent
3. have the Parent use it to change its own state
4. display this new Parent state
 
To begin, set the state in the Parent:  


```javascript
import React, {Component} from "react";
import Child from './child.jsx'

class Parent extends React.Component{
    state = { 
        clicks: 0
    }

```
Then, create a 'Parent interface ' method.

This will accept a value from the child and multiply it by 2.  

We will pass this function to the child so that the child can use it. 

```javascript
    setParent = (newCount) => {
        this.setState(
            {clicks: newCount*2} 
        )
    }
```

Here we render a few things: 
1. The child component, to which we pass the Parent interface as a callback
2. The results of setParent component

```javascript
    render() {
        return(
            <div>
                <Child setParent={this.setParent} />
                <p>In parent, multiplied by 2: 
                    {this.state.clicks}</p>
            </div>
        )
    }
};

export default Parent;

```

The Child component will begin in a similar way


```javascript
import React, {Component} from "react";

class Child extends React.Component {
    state = {
        click: 0
    }

```
The Child 'interface' method will change the Child state.
It will then send this new value to the setParent callback
Notice that second function is set to fire ONLY after the first is finished; 
otherwise, the callback might fire before the state has been reset. 

```javascript
    handleClick = () => {
        this.setState({
            click: this.state.click+1
        }, () => {
            this.props.setParent(this.state.click);
        })  
    }

```
Here, we render our button.  When it is pressed, it calls our Child interface, and displays the results. 

```javascript
    render() {
        return(
            <button onClick={this.handleClick}>
                {this.state.click}
            </button>
        )
    }
}

export default Child;
```