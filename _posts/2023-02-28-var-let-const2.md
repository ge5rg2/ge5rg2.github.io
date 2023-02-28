---
layout: post
title: "Hoisting, global variable, reference"
summary: "Summary of variable new syntax pt.2"
author: ge5rg2
date: "2023-02-28 14:20:10 +0900"
category: javascript
thumbnail: /assets/img/posts/var_let_const.png
keywords: javascript
permalink: /blog/var-let-const/
usemathjax: true
---

[Reference](https://codingapple.com/)

<br/>

### **Hoisting of JavaScript variables and functions**

<br/>

`Hoisting` occurs when you declare a variable or function in JavaScript.

JavaScript forces the declaration of a variable or function to the top of the variable's scope and resolves it first.

That's Hoisting.

<br/>

Let's take an example.

```jsx
function fn() {
  console.log("hello");
  var name = "Kim";
}
```

Let's say you create a variable inside a function like this.

However, the order in which JavaScript interprets this code is as follows.

<br/>

```jsx
function fn() {
  var name;
  console.log("hello");
  name = "Kim";
}
```

Forces the variable's **declaration** part to the top of the variable's scope to be interpreted and passed.

It is invisible to our eyes, but the order of JavaScript code operation is like this.

Anyway, this is a `Hoisting` phenomenon.

It's the same if you make a function, and it's the same if you make a variable 'let' or 'const'.

<br/>

So what will be the result of running this code?

```jsx
<script>console.log(name); var name = 'Kim'; console.log(name);</script>
```

<br/>

First, `undefined` is printed in the console window,

Second, `Kim` is printed.

Because of `Hoisting`

```jsx
var name;
console.log(name);
name = "Kim";
console.log(name);
```

The code runs in this order.

<br/>

`undefined` means that `undefined` is displayed when a variable is declared but no value is assigned to it.

It's kind of like a data type, but you can just think of it as **undefined value**.

However, in the case of `let` and `const` variables, `Hoisting` occurs, but in a slightly strange way.

<br/>

### **Making multiple variables convenient**

<br/>

You can create multiple variables at the same time by separating them with commas.

```jsx
var name, age, height;
```

This will create 3 variables. You don't have to use the `var` keyword 3 times, so the code is slightly reduced.

<br/>

```jsx
var name = "Kim",
  age,
  height;
```

If you want to assign at the same time as declaration, you can just do this.

It just has the advantage of not having to use the `var` `let` `const` keywords multiple times.

<br/>

```jsx
var name, age, height;
```

I also write like this.

<br/>

### **Global Variables and Variable References**

<br/>

Variables have this property.

**Outside variables can be freely used inside**.

This is referred to as referable in professional developer terms, but in JavaScript, there is another word for this phenomenon.

This is called a `closure`.

For example, what is inside and outside?

```jsx
var age = 20;

function fn() {
  console.log(age);
}

fn();
```

Now, from the inside of `fn(){}` to the outside, you can use a variable called **age**.

If there is a variable definition called **age** inside `fn(){}`, it will be used.

If not, it naturally uses an external variable. (refer to)

<br/>

In programming, there is something called a **global variable**.

A common useful variable that can be used (referenced) in any function or inside `if` or `for`.

If you want to create and use a global variable, just open `script` and create a variable.

<br/>

```jsx
<script>var age = 20; function fn(){console.log(age)}</script>
```

Then, you can use the `age` variable in all `function`, `for`, `if`, etc. below.

Global variable complete!

However, global variables have a strange characteristic.

<br/>

Previously, we learned that there is an object called `window`.

We learned that `window` is a large object that holds JavaScript basic functions.

`alert`, `getElementById`, `console.log` These functions are all included.

To test if it's true

<br/>

Try using `window.alert()`, `window.document.getElementById()` like when dealing with JavaScript basic functions like objects.

Since these alerts are also stored in the window, `window.alert('Hello')` is fine.

This is the role of the `window` object.

<br/>

But if you **create a global variable, it will be stored in `window` as well. (just the keyword `var`, not `let`)**

```jsx
<script>var age = 20; console.log(age); console.log(window.age);</script>
```

If we create a global variable called `age`

Because **automatically stored in the window object**

Curiously, using `window.age` also outputs it.

(Global functions are automatically stored in `window` as well)

<br/>

So, if you want to manage or classify global variables more strictly,

Try using `window` when creating and using global variables.

```jsx
<script>
  window.age = 20;//makeGlobalconsole.log(window.age);//useGlobalwindow.age =
  30;//editGlobal
</script>
```

You can also use it like this.

(In the `node.js` environment, there is an object called `global` which is a replacement for `window`)

<br/>

What will appear in the console window when you run the following code?

<br/>

```jsx
<script>

  if (true) {
    let a = 1;
    var b = 2;
    if (true) {
      let b = 3;
    }
    console.log(b);
  }

</script>
```

The value `b` is 2.
`let b = 3;` This part exists only within the inner if, so it has nothing to do with the outer `console.log(b)`.
