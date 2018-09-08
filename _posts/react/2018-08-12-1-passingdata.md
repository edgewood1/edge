---
layout: post
published: true
categories: react
title:  Props - Passing Data to Components
---

To recap:

The parent component does little more than loop through the child 4 times, using its state to assign each iteration a unique id, counter setting, and value. 

In the child, we design the look and functionality of each button.  Currently, its state is hardwired to count: 0. 

--------

In the child, the initial counters are set via state.count.  They are hardwired to 0.  So, each button will render with an initial count of 0

But since in the parent, we've assigned each iteration of the button with a value attribute, we can set state.count to this value.  

How to set a child value so that it reflects a property in the parent component? We could use this.props

So we switch count: 0 to count: this.props.value

```javascript
class Child extends Component {
  state = {
    count: this.props.value
  };
  ```

This variable will read the parent's state.counters[...].value

Is this.props another way of saying parent's state.counters ?  

Not really... 

```javascript
  console.log('props', this.props);
```

If in the child comp, we console.log(this.props) under render (yet before return), we will see 4 objects represented, one for each object in our parent's state.counters array: 

```javascript
props {value: 4, selected: true}
props {value: 3, selected: true}
props {value: 2, selected: true}
props {value: 0, selected: true}
```

In the above, props will not show key because that is just the id

What is the props property? it's from react Component import.  It is an object that lists all the attributes in the current component. 

Yet does it only show shared properties? 

We have the console.log in the child component, yet it is reading the parent's state... so?? 

We could assume that this.prop refers to the parent's properties. 

 

 