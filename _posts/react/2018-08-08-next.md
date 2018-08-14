---
layout: post
published: true
categories: react
title: Conditional Lists
---

Add this array to our state object: 

```javascript
   tags: ["tag1", "tag2", "tag3"]
```

Then loop through this array with a map function in the JSX. If this is placed in the render() method, it will create <ul> tags.  Then within this it will create, for each array item, an <1i> tag that has the array item as a unique id (key) and as its content:  

```javascript 
<ul>{this.state.tags.map(tag => <li key = {tag}> {tag} </li>)}
</ul>
 ```

CONDITIONAL RENDERING

Unlike angular, jsx is not a templating engine.  if-else statements don't work inside JSX. This is because JSX is just syntactic sugar for function calls and object construction.

Instead use a ternary expression.  If a ternary expression isn't robust enough, you can use if statements outside of your JSX to determine which components should be used:

So below, we place the if in a special method.  If the array is empty, a <p> line will be returned.  The next line shows what will be returned otherwise: our tag loop:  

```javascript
    renderTags() {
        if (this.state.tags.length === 0) 
            return <p> There are no tags </p>;
        return <ul>{this.state.tags.map(
            tag => <li key={tag}> {tag} </li>
        )}</ul>;
    }
```

Then, save the render() for this production: 

```javascript
  render() {
    return (
      <React.Fragment>
        {this.renderTags()}
      </React.Fragment>
    );
  }
```

One last strategy - the logical operator && will evaluate true && true as true - it prints out the last operand.  Likewise, below, x.length == 0 && "hello" will print "hello" if x is empty.  Therefore, this could be another means of presenting a conditional:  


```javascript 
    {this.state.tags.length === 0 && 
        "Please create new tag"}
    {this.state.tags.length >0 && 
        <ul>{this.state.tags.map(tag => 
            <li key={tag}> {tag} </li>)
    }</ul>}
```


