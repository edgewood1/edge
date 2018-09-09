---
layout: post
published: true
categories: react
title:  Passing Event Arguments
---

What if we want to pass arguments with events? 

We can't do this: 

```javascript

render() {
    ...
    onClick={this.handleIncrement(1)}
    ...
}

```

So we create a new method that will handle the passing of an argument.  This will pass a product object with the id of 1: 

```javascript
doHandleIncrement = () => {
    this.handleIncrement({id: 1})
}
```

Then, in our event handler, we capture the object with the product variable, and console.log it:

```javascript
handleIncrement = (product) => {
    console.log(product);
    this.setState({count: this.state.count +1})
}

```
Then our eventListener could be altered from 

```javascript
render() {
    ...
    onClick={this.handleIncrement}
    ...
}
```
to this

```javascript
render() {
    ...
    onClick={this.doHandleIncrement}
    ...
}
```

An easier way: 

```javascript
render() {
    ...
    onClick={ () => this.handleIncrement({id:1})}
    ...
}
```
or? instead of hardcoding, product will be passed a figure from the frontline: 

```javascript
 
render() {
    ...
    onClick={ () => this.handleIncrement({product})}
    ...
}

```