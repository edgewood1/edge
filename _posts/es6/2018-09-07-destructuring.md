---
layout: post
published: true
categories: es6
title: Destructuring
---

Here, we assign object keys to variables: 

var list = {
    x: 1,
    y: 2, 
    z: 3
}; 

var x = list.x; 
console.log(x) // 1

const {x, y, z} = list;

Now, 

console.log(x) // 1

https://www.youtube.com/watch?v=-vR3a11Wzt0