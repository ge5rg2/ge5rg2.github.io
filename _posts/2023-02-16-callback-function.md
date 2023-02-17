---
layout: post
title: "Sync/async processing and callback function"
summary: "Sync/async processing and Callback function neatly defined"
author: ge5rg2
date: "2023-02-16 14:26:12 +0900"
category: javascript
thumbnail: /assets/img/posts/javascript.png
keywords: javascript
permalink: /blog/callback-function/
usemathjax: true
---

### **Javascript works synchronously (synchronous)**

synchronous processing -> **Execute one line of code at a time**
A web browser that executes JavaScript has a code execution space called a stack.

From there, it executes the code line by line.

```jsx
<script>console.log(1); console.log(2); console.log(3);</script>
```

So, the following code outputs 1,2,3 in order.

This is because JavaScript processes code one line at a time. -> synchronous
Most programming languages have this feature.

### **Asynchronous processing is also possible.**

If you want specific code to run after 1 second...

```python
print(1)
time.sleep(1)
print(2)
```

This code is written in Python
time.sleep(1) means, please rest for 1 second.
<br/>

Then 1 is output / **1 second rest** / 2 is output.

To write code in JavaScript that pauses for one second and prints something

```jsx
console.log(1);
setTimeout(function () {}, 1000);
console.log(2);
```

You shouldn't write like this like a normal programming language.
<br/>

**1 and 2 are output to the console window at the same time**.

You can feel the weirdness of JavaScript here.

<!-- <img src="https://codingapple.com/wp-content/uploads/2020/04/271c176806330.jpeg" width="100%"  height="100%" title="meme" alt="meme" /> -->

JavaScript is a different way of thinking than most programming languages.

If you look closely at the function called setTimeout(), it is a function that takes a little time to execute, right?
It takes 1 second.

A web browser is a JavaScript execution machine.

When I see these **special pieces of code, I try to put them aside and run other codes first**.

That's why setTimeout() is put aside and the code called console.log(2) under it is executed first.
This type of processing is called **asynchronous**.
<br/>

Such code that takes a long time to execute is put on standby for a while,

It means a way to process code that can be executed immediately.
This is not a feature of the JavaScript language itself.

It can be done thanks to a **web browser** that helps you run JavaScript.
<br/>

### **Waiting room to set code aside for a moment**

There are pre-determined codes that can be deferred and set aside for a moment.
These are the setTimeout, addEventListener, and ajax related functions mentioned above.

setTimeout, addEventListener, and ajax-related functions are codes that do things like wait for 1 invitation and click.
<br/>

**A characteristic of these codes is that there is a difference between reading time and operation time.** (To put it simply, it takes a long time to operate.)
When Chrome, which executes and interprets JavaScript, encounters these special codes,

1. Leave it in the waiting room for a while 2. Run it again when it's ready.

```jsx
console.log(1);
setTimeout(function () {}, 1000);
console.log(2);
```

▲ When the browser reads the above code and encounters a setTimeout~ code, it moves to the Web API for a while and waits.

And when the waiting time of 1 second passes and setTimeout is completed, the code is taken out of the waiting room and the code is executed.
<br/>

This allows time-consuming code like setTimeout to be processed asynchronously.
So JavaScript is usually processed synchronously if there is nothing special.

It is a language that can be made to operate asynchronously by using functions such as setTimeout that support asynchronous.
<br/>

### **Sequential execution using callback function**

So back to our example, if you want to run code after 1 second in JavaScript...

```jsx
console.log(1);
setTimeout(function () {
  console.log(2);
}, 1000);
console.log(3);
```

You can write the code in the callback function inside setTimeout like this.
Then 1 and 3 appear quickly in the console window
Then, after **1 second**, the number 2 appears.  
<br/>

JavaScript actively utilizes callback functions when you want to execute codes **sequentially** in an asynchronous situation.  
<br/>

- **What is a callback function?**

  All functions that are nothing special and just go inside a function are called callback functions.

If you are curious how you did it, if you use a callback function, it will be executed sequentially.
<br/>

### **How to design a callback function**

For example, let's say you have two functions that you want to execute sequentially.

So can I code like this?

```jsx
function fn1() {
  console.log(1);
}

function fn2() {
  console.log(2);
}

fn1();
fn2();
```

If you code in Python, this is correct.

However, JavaScript does not guarantee that it will be executed sequentially because of its asynchronous nature.

(If the first function is a setTimeout or a code sent to the Web API waiting room, it can be executed later)

Then I think we should develop the same as this one.
Create a callback function **fn1(fn2);**  
<br/>

If you make it run like this, you can run it sequentially, right?

So how do you write code to put functions inside functions?

```jsx
function fn1(callBack) {
  console.log(1);
  callBack();
}

function fn2() {
  console.log(2);
}

fn1(fn2);
```

You just need to pass a parameter to the function.
And if you put parentheses around the parameter and say, “Execute it~”, you can put the function inside the function and execute it.  
<br/>

This is how to design a callback function.
You can insert a pre-made function like above

```jsx
fn1(function(){
  console.log(2)
}):
```

You can also insert function declarations directly like this.
There are some disadvantages to using multiple callback functions to execute sequentially.  
<br/>

The cord grows sideways.

```jsx
fn1(function(){
  fn2(function(){
    fn3(function(){
      and so on...
    });
  });
}):
```

This code executes fn1 fn2 fn3 in order like this.
This pattern is especially common when developing servers with JavaScript.
If you don't want to see this, you can create and use the ES6 newspaper law "Promise".  
<br/>

By applying the "Promise" design pattern, which can be used instead of callbacks,

```jsx
fn1().then(function(){
   the next one
}).then(function(){
   next one
});
```

It doesn't grow sideways, and thanks to the keyword then, it's easy to figure out what it's doing.

<br/>

[Reference](https://codingapple.com/)
