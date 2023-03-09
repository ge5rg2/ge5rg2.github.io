---
layout: post
title: "ES6 REST parameters"
summary: "Let's look at the 3 dot rest parameters used in functions"
author: ge5rg2
date: "2023-03-08 15:31:20 +0900"
category: javascript
thumbnail: /assets/img/posts/rest.jpeg
keywords: javascript
permalink: /blog/rest/
usemathjax: true
---

[Reference](https://codingapple.com/)

<br/>

### **Rest parameter**

When creating a function, you can add the symbol '...' to the left of the parameter.

Then something strange happens.

```jsx
function fn2(...parameter) {
  console.log(parameter);
}

fn2(1, 2, 3, 4, 5, 6, 7);
```

If you run the above code, it will output a variable called `parameters`.

A variable called `parameters` contains all `parameters` in a `[] array`.

This is a rest parameter that can be used in the `ES6` environment.

Add `...` to the left of the desired parameter

**It means "parameters enclosed in [] curly braces around all the parameters that come in this place"**.

<br/>

So if you print it out, `[1,2,3,4,5,6,7]` comes out.

Rest parameters are all parameters `(1,2,3,4,5,6,7)` wrapped in braces.

<br/>

### **If `...` is used elsewhere**

<br/>

If you said to wrap the parameter in its place in `[]`

What if I put it somewhere else?

<br/>

```jsx
function fn2(a, b, ...parameters) {
  console.log(parameters);
}

fn2(1, 2, 3, 4, 5, 6, 7);
```

If you run the above code, it will output `[3,4,5,6,7]`.

The first two parameters are written as `a, b`.

**All parameters after `a,b` are wrapped in curly braces to become an array called `parameters`**

When there are many types of parameters, it is easier to handle and simpler than the arguments syntax, so it is often used.

<br/>

### **Notes before writing**

<br/>

`Rest(remaining)` As the parameter means, it can be used only in the rest part.

So, if there are always multiple parameters, rest should always be put as the last parameter.

<br/>

```jsx
function fn2(a, ...parameters, b){
  console.log(parameters)
}
```

You're getting an error if you use it like this.

<br/>

```jsx
function fn2(a, ...parameters, ...parameters2){
  console.log(parameters)
}
```

this also doesn't work. You cannot use more than 2.

<br/>

### **Simple exercises**

<br/>

I want to create a function that outputs all the parameters one by one to the console window.

What should I do?

It's easy, so let me give you the answer.

```jsx
function fn(a, b, c) {
  console.log(a);
  console.log(b);
  console.log(c);
}

fn(1, 2, 3);
```

However, if 4 or 5 parameters were entered incorrectly, a stupid function that did not run properly was completed.

**How can I create a function that performs the same function without limiting the number of parameters**?

<br/>

A.

```jsx
function fn(...rest){
  console.log(rest[0]);
  console.log(rest[1]);
  console.log(rest[2]);
  (...)
}

fn(1,2,3);
```

can't you do it like this But since I don't know how many parameters

The `console.log()` part can be made simpler by using a loop.

```jsx
function fn(...rest) {
  for (var i = 0; i < rest.length; i++) {
    console.log(rest[i]);
  }
}

fn(1, 2, 3, 4, 5, 6, 7, 8);
```

Because `rest` is a variable that puts all parameters in `[]` and makes it like an array.

You can turn the loop like that.

Then, no matter how many parameters you put in the function, you can continue to output to the `console window`.
