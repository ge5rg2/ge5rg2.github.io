---
layout: post
title: "Object-Oriented 1"
summary: "Object-Oriented 1. Let's create and use a constructor, which is an object creation machine."
author: ge5rg2
date: "2023-03-10 11:22:10 +0900"
category: javascript
thumbnail: /assets/img/posts/obj.png
keywords: javascript
permalink: /blog/object-oriented/1
usemathjax: true
---

[Reference](https://codingapple.com/)

<br/>

In this lesson, let's learn a syntax called `constructor` that can make many copies of `object` safely.

<br/>

### **Create Student Attendance Sheet with JavaScript**

<br/>

I need to create a list of students with JavaScript.

```jsx
var student1 = { name : 'Kim', age : 15 };
var student2 = { name : 'Park', age : 15 };
...
```

You should make 30 people like this. What's the fastest way to do it?

Of course, rather than hardcoding 30 objects by directly bracketing them

Since they are similar objects, it would be better to copy them.

But if you copy `var student2 = student1` using `=` equal sign, it will be a big deal.

Let's try using the new syntax to copy and stamp an object.

<br/>

```jsx
//var student1 = { name : 'Kim', age : 15 };
function machine() {
  this.name = "Kim";
  this.age = 15;
}
```

When creating an `object` data copying machine, you can borrow and use the keyword `function` to create a function.

Just create a `function` and put `this.name` and `this.age` in it.

This is an object creation machine.

`this` refers to the newly created object. (That's called an instance in fancy development jargon.)

<br/>

Now, if you want to pull a new object from the machine, you can follow this.

```jsx
//var student1 = { name : 'Kim', age : 15 };
function machine() {
  this.name = "Kim";
  this.age = 15;
}

var student1 = new machine();
var student2 = new machine();
```

If you write the keyword `new` and then write the name `machine(constructor)` on the right

A new object can be extracted from the machine.

And if you store it in a variable, you can now freely pull out and use the object.

<br/>

Reduces the amount of code when creating multiple similar + independent `object` data.

So that's the syntax you use.

In particular, try using it when there are many complicated contents in the object.

<br/>

### **If an object must contain a function**

<br/>

You can even add functions to objects, right?

So, for example, let's say we need to add a function called `sayHi()` inside every student object.

If you use `student1.sayHi()`, it should output **a greeting with your name, "Hello, this is 'Kim'"** to the console window.

How can I code it?

<br/>

```jsx
var student1 = {
    name : 'Kim',
    age : 15
    sayHi : function(){
        console.log('Hello' + this.name);
    }
};

student1.sayHi();
```

However, it is not hard-coded only in `student1`.

What if we want to make `sayHi()` available to all students in the future?

Of course, you can add it to the object creation machine, right?

<br/>

Let's add `sayHi()` to the machine.

<br/>

```jsx
function machine() {
  this.name = "Kim";
  this.age = 15;
  this.sayHi = function () {
    console.log("Hello" + this.name);
  };
}
var student1 = new machine();
var student2 = new machine();

student2.sayHi();
```

If you add `this.sayHi` to the machine like that, all students created from the machine will now have `sayHi()`.

Then both `student1 and student2` can use `sayHi()`.

You can also put functions inside `object` data, so it just makes sense.

<br/>

### **If you want to assign different name and age values to each student object**

<br/>

There is a problem with the objects pulled so far.

`student1` and `student2` both have the same `name`, which seems impractical.

So, what if we want to pull out the actual `name` property differently?

Just remember that you can add parameters to functions.

<br/>

```jsx
function machine(n) {
  this.name = n;
  this.age = 15;
  this.sayHi = function () {
    console.log("Hello" + this.name);
  };
}
var student1 = new machine("Park");
var student2 = new machine("Kim");
```

If you add a parameter to the function, every time you use a function called machine in the future

It can be executed by putting some data in the place of the parameter.

▲ So, if you look at the last line, I put data when using `machine()`.

<br/>

The `'Park'` data is put into the parameter position and the function is executed.

Then the `name` property of the newly created object will be `'Park'`. `(this.name = 'Park')`

Now

student1 is `{ name: 'Park', age: 15 }`

student2 is `{ name: 'Kim', age: 15 }`

It might output like this.

If you want to assign different values to each created object, use the function parameters like this.

If you want to change the age as well, you can add one more parameter.

<br/>
