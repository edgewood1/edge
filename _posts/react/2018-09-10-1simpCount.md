---
layout: post
published: true
categories: react
title:   Simple Click
---

Begin with the 3 parts a component class: 
1. import
2. class
3. export 

```javascript
import React, {Component} from "react";
 
class UNC1 extends Component {
   ... body...     
}
export default UNC1;
```

In the class body, define state: 

```javascript
    state = {
        count: 0
    };
```
Define a click method for our future click button.  
This uses the method "setState" to increase the state.count
You must return this

```javascript
    click = () => { 
        // set state is a function
        this.setState({count: this.state.count+1})
        return this.state.count
    }
```

Define a reset method that will set count back to 0

```javascript
    reset = () => {
        this.setState({count: 0})       
        return this.state.count;
    }
``` 
Finally, our render method which returns JSX.
The first button calls the click method and displays the count
The second button calls the reset method.

```javascript
    render() {
        return(
        <div>
            <button onClick={() => this.click()}>
               {this.state.count}
            </button>
            <button onClick={() => this.reset()}>
               reset!
            </button>
        </div>
        )
    }
```
