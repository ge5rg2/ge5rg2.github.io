---
layout: post
title: "Object-Oriented 2"
summary: "Object-Oriented 2. Understanding prototypes"
author: ge5rg2
date: "2023-03-13 10:22:20 +0900"
category: javascript
thumbnail: /assets/img/posts/obj.png
keywords: javascript
permalink: /blog/object-oriented/2
usemathjax: true
---

[Reference](https://codingapple.com/)

<br/>

What we learned last time is called **inheritance** in fancy object-oriented terminology.

It inherits the `name, age` properties of the `constructor` called machine and pulls out an object.

Well, it's called inheritance because it's similar to inheritance that inherits property.

(So what inherits is referred to as **parent**, and inherited objects are referred to as **children**.)

<br/>

However, there is one more device in JavaScript that can implement inheritance other than `constructor`.

It's called `prototype`, let's find out.

<br/>

### **When you build a machine, an item called `prototype` is secretly created inside the machine.**

<br/>

▲ If you want to check if the above fact is true, you can print it out.

Every machine you build secretly creates something called a `prototype` inside.

<br/>

```jsx
function machine() {
  this.name = "Kim";
  this.age = 15;
}
var student1 = new machine();
var student2 = new machine();

console.log(machine.prototype);
```

Then I don't know what it is, but something is output?

Why does the secret space called `prototype` that I suddenly found out exists and where is it used...

You can see this as a kind of secret space that acts as a parental gene.

<br/>

You can think of a `prototype` as a **gene** that children can inherit.

`machine.prototype` is the gene of `machine`.

If `machine**.prototype**` contains some variable or function

All new objects (children) created from the machine can inherit it and use it.

<br/>

For example:

Last time, let's add a line like `prototype` to the example code.

<br/>

```jsx
function machine() {
  this.name = "Kim";
  this.age = 15;
}

machine.prototype.gender = "boy";
var student1 = new machine();
var student2 = new machine();

console.log(student1.gender); //will print 'boy'
```

I stored a `key/value` pair named { `gender : 'boy'` } in a place called `prototype` on the machine.

(You can use `prototype` as if you were dealing with an object data type.)

<br/>

It is the addition of `gender: 'boy'` data to the machine's `prototype`, that is, its genes.

Now all children created from <span style="color: blue">machines such as `student1` and `student2` can use the `gender` attribute.</span>

<br/>

So the conclusion is that you can create the same inheritance function by using the secret space called `prototype`.

<br/>
(reference)

- You can assign multiple values to `prototype` and even include a function. Just treat it like `object` data.
- Data added to `prototype` are not directly owned by children, but only by parents.

<br/>

### How it Works?

<br/>

JavaScript has a check order <span style="color: blue">when extracting data from an object.</span>

<br/>

```jsx
function machine() {
  this.name = "Kim";
  this.age = 15;
}
machine.prototype.gender = "boy";
var student1 = new machine();

console.log(student1.gender);
```

▲ If you use `student1.gender`, `'boy'` is output, right? The reason is that..

<span style="color: red">When JavaScript outputs a value from an object</span>, it asks in this order.

(1) Is there a value called `gender` directly in `student1`?

(2) Then, is there a value of `gender` in the parent gene?

(3) Then, is there a value of `gender` in the parents' genes?

(4) Then in the parent's parent's parent's gene .. Is there that?

<br/>

JavaScript works with this algorithm.

Simply put, when extracting a value from an object

1. Check if I have it myself

2. If I don't have it, the parent genes are tested in turn.

You just have to remember that.

<br/>

So, the object named `student1` does not have the value `gender`, but

That's why you can print the 'gender' in the parent's gene ('machine.prototype').

<br/>

## **How it works 2: Why you can use the built-in JavaScript function `toString()`**

<br/>

JavaScript `array, object` has many built-in functions that can be attached.

`sort`, `push`, `toString`, `map`, `forEach`, etc. can be used by attaching them to `array`. Have you ever wondered why?

<br/>

```jsx
var arr = [1, 2, 3];
console.log(arr.toString()); // posiblle
```

The reason why I can append `arr.toString()` to my `array` like this is

Because the parent gene of the `array` I created has `toString()`. (or parents' parents)

<br/>

- **The `array` I created is not drawn from the parent machine. What are you talking about?**

Actually, when you create an `array` or `object` data type, there is a parent.

```jsx
var arr = [1, 2, 3];
var arr = new Array(1, 2, 3);
```

▲ The above two lines of code have exactly the same meaning.

The top is how humans make `arrays`, and the bottom is how computers make `arrays`.

People are cumbersome, so they just use square brackets with `[]` to make it **Internally, it always uses the `new` keyword like that to create `array/object`.**

<br/>

Then **`new Array()`** What does this mean?

Doesn't it mean "Pick a new child from the machine called `Array`?"

you're right.

<br/>

Therefore, children created from `Array` can freely use the functions and data given to the gene of `Array`.

To check if the gene of the machine called `Array` is real, you can print it in the console.

<br/>

```jsx
console.log(Array.prototype);
```

What do you get when you do this? Your usual `sort`, `map`, `push`, `forEach` will appear.

So all the children of `Array` could easily use these functions.

<br/>

Since the `Object` data type is created in the same way as `new Object()`, functions in the parent`s `prototype` can be freely used.

This was the secret of built-in functions.

<br/>

**Q. So what's the difference between inheriting with `prototype` and inheriting with `constructor`?**

A. If you want children to own the value directly, you can inherit it with `constructor`.

If you only have a parent and want to refer to it and use it, can you inherit it with `prototype`?

Usually, a lot of things like functions that can be inherited are made as `prototype`.
