---
layout: post
title: "Javascript Destructuring syntax"
summary: "How to use Obj destructuring in JS"
author: ge5rg2
date: "2023-02-17 17:14:40 +0900"
category: javascript
thumbnail: /assets/img/posts/dest.png
keywords: javascript
permalink: /blog/destructuring-syntax/
usemathjax: true
---

The destructuring syntax makes it easy to create variables by extracting multiple data from Array and Object data types.

<br/>

### **How to put data in an array into a variable**

I have an array of `[2,3,4]`,

What if I want to take out all three data inside here and put them in a variable?

```jsx
var array = [2, 3, 4];
var a = array[0];
var b = array[1];
```

what could be like this.

<br/>

But there is an easier way to do it.

```jsx
var [a, b, c] = [2, 3, 4];
```

You can declare a variable in a shape similar to the data `[2,3,4]`.
Then three variables a,b,c are created, each with data 2,3,4.

<br/>

**A default value can also be given.**

Naturally, if the left and right numbers are different, the variable is not created properly.

```jsx
var [a, b, c] = [2, 3];
```

Variables that take no value can be made to have default values.

```jsx
var [a, b, c = 5] = [2, 3];
```

Then `c` assigns a default value of `5` if no value is entered.

<br/>

### How to put data in object into variable

If you align the left and right of the `object` the same, a variable is created.

```jsx
var { name: a, age: b } = { name: "Kim", age: 28 };
```

When matching the variable name with the key name in the `object`, you can just use it like this.

```jsx
var { name, age } = { name: "Kim", age: 28 };
```

name: You can omit the name with one name like this.

- The same as `array`, the default value can also be applied with an equal sign.

<br/>

### This time, if you want to put a variable into an `object`

```jsx
var name = "Kim";
var age = 28;

var obj = { name: name, age: age };
```

If you want to put a variable into the `object` data type, you can use it like this, right?

However, with the destructuring syntax, this is also possible.

```jsx
var name = "Kim";
var age = 28;

var obj = { name, age };
```

`name : name` If the key value and the value value are the same like this

`name` You can omit one like this.

<br/>

### The same can be applied when creating function parameter variables.

There is one function, this function can take two parameters.

What if you want to input Kim and age data in the object here?

```jsx
function fn(name, age) {
  console.log(name);
  console.log(age);
}

var obj = { name: "Kim", age: 28 };
fn(obj.name, obj.age);
```

Maybe `obj.name` and put this in directly?

Or you can use destructuring syntax.

```jsx
function fn({ name, age }) {
  console.log(name);
  console.log(age);
}

var obj = { name: "Kim", age: 28 };
fn(obj);
```

Because of parameterization is the same behavior as creating a variable.
You can apply the same syntax for creating variables.

when entering parameters

`{name, age} = { name : 'Kim', age : 20 }`

It's the same as what I did.

<br/>

**Q1.**

```jsx
var [number, address] = [30, "seoul"];
var { address: a, number = 20 } = { address, number };
```

What values do the variables `a`, `address`, and `number` each have?

Let's change the second line a bit to make it easier to see.

```jsx
var { address: a, number = 20 } = { address: "seoul", number: 30 };
```

So `a` is `'seoul'`

`number` is `30`

The `address` is modified in the first line and ends, so it is `'seoul'`.

<br/>

**Q2.**

```jsx
let info = {
  body: {
    height: 180,
    weight: 70,
  },
  size: ["Large", "30in"],
};
```

Here, I would like to create four variables by extracting **Height, Weight, Top Size, and Bottom Size** information respectively.

How can i make it?

<br/>

```jsx
let info = {
  body: {
    height: 180,
    weight: 70,
  },
  size: ["Large", "30in"],
};

let {
  body: { height, weight },
  size: [top, bottom],
} = info;
```

If you look closely, I used an equal sign to align the left and right sides the same.

And on the left, I wrote the variable name.
