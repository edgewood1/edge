---
layout: post
published: true
categories: react
title: Extends 
---

After importing our React module, we create a component class, which will inherit various properties from the Component method of the React module.  

The keyword *extend* allows us to inherit these properties.  So below, the class "Contacts" will inherit from "React.Component":

```javascript
import React from 'react';

class Contacts extends React.Component 
    { ... our class body ... };
```

If the return method has more than 1 JSX expression, embed in  *<div>*

```javascript
return (
    <div>
        <h1> Hello World </h1>
        <button>Increment</button>
    </div>
);
```

An alternative is <React.Fragment>, which doesn't show in the console.  

```javascript
return (
    <React.Fragment>
        <h1> Hello World </h1>
        <button>Increment</button>
    </React.Fragment>
);

```




