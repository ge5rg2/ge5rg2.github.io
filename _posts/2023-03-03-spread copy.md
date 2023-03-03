---
layout: post
title: "How to use Spread Operator 2"
summary: "How to use Spread Operator 2"
author: ge5rg2
date: "2023-03-03 12:32:10 +0900"
category: javascript
thumbnail: /assets/img/posts/es6.png
keywords: javascript
permalink: /blog/spread-operator2/
usemathjax: true
---

[Reference](https://codingapple.com/)

<br/>

### **Where to use this 3. It is used when you want to put an `array` in the form of a parameter.**

<br/>

To give an example, let's create a function.

```jsx
function plus(a, b, c) {
  console.log(a + b + c);
}
plus(1, 2, 3);
```

I made a function called `plus` that takes three parameters and adds them all together.

But here **When inserting parameters**

Instead of directly writing `1,2,3`

What if you want to insert internal data from an already existing `array`?

So, for example...

<br/>

```jsx
function plus(a, b, c) {
  console.log(a + b + c);
}

var arr = [10, 20, 30];
```

**How can I put all the numbers `10,20,30`** in `arr` as parameters of `plus()` function?

<br/>

```jsx
plus(10, 20, 30);
```

Write it by hand or

<br/>

```jsx
plus(arr[0], arr[1], arr[2]);
```

Should I do this or something?

But if that bothers you, you can use the `spread` operator.

<br/>

```jsx
function plus(a, b, c) {
  console.log(a + b + c);
}

var arr = [10, 20, 30];
plus(...arr);
```

Then, when printed, the result of adding 10, 20, and 30 is printed well.
