---
layout: post
title: "Constructor, Prototype 4 exercises"
summary: "constructor, prototype 4 exercises"
author: ge5rg2
date: "2023-03-16 17:30:22 +0900"
category: javascript
thumbnail: /assets/img/posts/jsquiz.png
keywords: javascript
permalink: /blog/constructor-prototype-3q
usemathjax: true
---

[Reference](https://codingapple.com/)

<br/>
<span style="color: red"></span>

### **0. I want to create multiple object data.**

Hardcoding is what I do best, so I hardcoded it.

<br/>

```jsx
var student1 = { name: "Kim", age: 20 };
var student2 = { name: "Park", age: 21 };
var student3 = { name: "Lee", age: 22 };
```

I made three by hardcoding, but I'm thinking of making a `constructor` because I think there will be more things to make in the future.

**Use the `constructor` syntax to draw 3 objects identical to the ones above.**

- Here Add a `sayHi()` function inside the `constructor` so that when you use `student1.sayHi()`, “Hello I am Kim” is displayed in the console window.

<br/>

### 0. Answer

<br/>

```jsx
function Student(n, a) {
  this.name = n;
  this.age = a;
  this.sayHi = function () {
    console.log("Hello I am " + this.name);
  };
}

var student1 = new Student("Kim", 20);
var student2 = new Student("Park", 21);
var student3 = new Student("Lee", 22);
```

You can do this. No big deal.

Adding the `sayHi` function to `prototype` seems to be no problem at all.

<br/>

### **1. What will be the output of the following code?**

<br/>

```jsx
function Parent() {
  this.name = "Kim";
}
var a = new Parent();

a.**proto**.name = "Park";
console.log(a.name);

```

<br/>

### 1. Answer

It is `'Kim'`.

By the first 4 lines, `a = { name : 'Kim' }`

`a.__proto__.name = 'Park';` means add `{ name : 'Park' }` to the parent `prototype`.

So now when I use `a.name`

First of all, I print `{ name : 'Kim' }` that I have.

<br/>

### **2. function doesn't work**

<br/>

In question 0 above, you said to add a function called `sayHi` to the parent named `Student`, right?

So, I added a function to `prototype` that outputs my name as `"Hello I am ~~"` when using `sayHi()`.

I made it like the bottom, but the name is not output as intended.

What could be the cause?

<br/>

```jsx
function Student(n, a) {
  this.name = n;
  this.age = a;
}

Student.prototype.sayHi = () => {
  console.log("Hello I am " + this.name);
};
var student1 = new Student("Kim", 20);

student1.sayHi(); //Why this code's output is not intended?
```

<br/>

### 2. Answer

I used the `arrow function` when adding a function called `sayHi()` to `prototype`.

To conclude, `arrow function` is not just a regular `function` replacement.

I said that `arrow function` is a function used when you want to use `this` outside `this` as it is.

By the way, when creating the `sayHi()` function, use the `arrow function`

The value 'this' inside was strange.

```jsx
Student.prototype.sayHi = () => {
  console.log(this);
};
```

If you just print 'this' to the `sayHi' function, it will output something like `window'. (`undefined` in strict mode)

According to the previous lecture, if you use the `arrow function`, you just get a value from anywhere outside and use it.

Outer **`this` value is `window`**,

This is because the `window` was applied to the inside of the function as it is.

So, it was a problem because `this` was strange.

<br/>

Let's review `this` for a second

Within a function, the meaning of the `this` keyword is redefined each time.

I said that `this` in the function contained in `object` becomes the `object` that called the function.

However, in the case of `arrow function`, the meaning of this is not redefined inside the function and `this` outside is used.

```jsx
var obj = {
  sayHi: () => {
    console.log(this);
  },
};
obj.sayHi();
```

▲ So this in the above code is

It's not an object, but a `window`.

The example in the question is similar to this one.

<br/>

### **3. How can I create my own new function that can be applied to any `array`?**

<br/>

can be attached to any `array`,

I want to create a useful function that removes the value of 3 in `array`.

```jsx
var arr = [1, 2, 3];
arr.remove3();

console.log(arr); //[1,2]
```

Just appending it to the end of `array` like this deletes all numeric data such as `3` in `array`.

Let's call it `remove3()`, nicely.

How and where to create a `remove3()` function so that it can be used on all `array`s?

<br/>

### 3. Answer

<br/>

Do you remember why we can attach functions like `pop()`, `sort()`, `push()` to every `array`?

All `array` datatypes are created by `new Array()` from their parent `Array`

This is because functions in the parent `prototype` of `Array` can be freely used.

Then, shouldn't we add a function called `remove3` to `prototype` of `Array`?

you're right.

<br/>

```jsx
Array.prototype.remove3 = function () {
  // plz find 3 and remove on this
};
```

You could write a code like this.

The keyword `this` in the code above means the `object` (`array` in this case) that currently triggers the function `remove3`.

So how do I write code to remove '3' from 'array' called 'this'?

If there are 100 ways to use one of them...

I wrote a loop to print out the data in the `this` array one by one and compare it with `3`.

<br/>

```jsx
Array.prototype.remove3 = function () {
  for (var i = 0; i < this.length; i++) {
    if (this[i] === 3) {
      this.splice(i, 1);
    }
  }
};

var arr = [1, 2, 3, 4];
arr.remove3();

console.log(arr); //[1,2,4]
```

It's not just difficult, the `remove3()` function

1. It runs a loop as long as the length of the `array` called `this`. In the process of running it, write `this[i]` and print out all the data in `this`.

2. if `this[i]` is `3`

3. Remove the `i`th element from the `array` named `this`

wrote. (The `splice` function is sometimes used to remove something from an `array`.)

<br/>
