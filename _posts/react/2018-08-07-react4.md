---
layout: post
published: true
categories: react
title: Style 
---


After the state property, you could add a styles property: 

```javascript
    styles = {
        fontSize: "10px",
        fontWeight: "bold"
    };
```

You can add a class attribute to a tag, but you have to use the keyword *className* rather than *class*.   The following JSX shows the style property, the class attribute, and a method working together:  

```javascript
    <span style={this.styles} 
        className="badge badge-primary m-2">
            {this.formatCount()}
    </span>
```

For in-line style, try: 

```javascript
    <span style={{ fontSize: 10 }} ...
```

A class can be rendered dynamically so that the className will be one thing if count is 0, an danother if it is not: 

We could put this calculation in its own method: 

```javascript
    getBadgeClasses() {
        let classes = "badge m-2 badge-";
        classes += this.state.count === 0 
            ? "warning" : "primary";
        return classes;
    }
```

And call it in the className:  

```javascript
    <span className={this.getBadgeClasses()}>
        {this.formatCount()}
    </span>
```