---
layout: post
title: "ES6 default parameter/arguments"
summary: "The default parameter function of the function upgraded from ES6, ES5 syntax arguments."
author: ge5rg2
date: "2023-03-06 16:32:50 +0900"
category: javascript
thumbnail: /assets/img/posts/jsfn.jpg
keywords: javascript
permalink: /blog/parameter-arguments/
usemathjax: true
---

[Reference](https://codingapple.com/)

<br/>

### **Input default parameters of functions**

<br/>

When creating a function, if the parameter value is not entered by mistake

You can give default values to parameters.

You can use it like this.

<br/>

```jsx
function plus(a, b = 10) {
  console.log(a + b);
}

plus(1);
```

When I run the above code, 11 is displayed in the console window.

Now the `plus()` function can take two parameters.

However, perhaps by mistake, I only used one parameter called 1.

In that case, `**b = 10**`, the default parameter value of 10 declared is assigned to b.

That's why `a + b` outputs `11` in the console window.

<br/>

If you want to give a default parameter, you can enter it with an equal sign when declaring the parameter like that.

Then the value to the right of the equals sign fires when the parameter is undefined.

Anything can be entered as a default parameter.

<br/>

```jsx
function plus( (a, b = 2 * 5){
  console.log(a + b)
}

plus((1);
```

Math operators are also available. If there is no parameter in b, it assigns a value of `2 * 5`.

<br/>

```jsx
function plus( (a, b = 2 * a){
  console.log(a + b)
}

plus((3);
```

Other parameters and calculations are also possible. If you run the above code, what will be printed in the console window?

<br/>

A. 9 is output.

Because it runs `console.log(3 + 6)`.

<br/>

Even **function input** is possible for the default parameter.

```jsx
function fn() {
  return 10;
}

function plus(a, b = fn()) {
  console.log(a + b);
}

plus(3);
```

If you run the above code, what will be printed in the console window?

<br/>

A. 13 is output.

If no parameter is entered in the b position, the value of executing `fn()` is assigned to the b parameter.

Running `fn()` leaves 10 in its place.

(return 10 is what it means)

So run `console.log(3 + 10)`.

<br/>

### **arguments of the function**

<br/>

There are times when you want to wrap **all the parameters** of a function all at once.

In that case, you can use the keyword arguments.

These are predefined keywords or variables that can be used inside a function.

Let's try it out.

<br/>

```jsx
function fn(a, b, c) {
  console.log(arguments);
}

fn(2, 3, 4);
```

This will output data similar to an `array` containing `[2,3,4]` to the console window.

arguments was a thankful keyword that put all input parameters in [ ].

Now, you can use it often when you want to deal with parameters at once.

An example would be something like this.

<br/>

If you want to output all parameters one by one in the console window

```jsx
function fn(a, b, c) {
  console.log(arguments[0]);
  console.log(arguments[1]);
  console.log(arguments[2]);
}

fn(2, 3, 4);
```

However, if you write a loop with a little more extensibility

<br/>

```jsx
function fn(a, b, c) {
  for (var i = 0; i < arguments.length; i++) {
    console.log(arguments[i]);
  }
}

fn(2, 3, 4);
```

It should be like this.

It was a syntax that could handle parameters a bit conveniently.

However, starting with `ES6`, a syntax called `rest parameter` appears that can handle parameters more easily.

Let's find out about that next time.
