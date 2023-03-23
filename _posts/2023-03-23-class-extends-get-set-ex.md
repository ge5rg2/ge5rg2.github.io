---
layout: post
title: "class, extends, getter, setter exercises"
summary: "class, extends, getter, setter exercises"
author: ge5rg2
date: "2023-03-23 14:19:20 +0900"
category: javascript
thumbnail: /assets/img/posts/getset.png
keywords: javascript
permalink: /blog/getter-setter
usemathjax: true
---

[Reference](https://codingapple.com/)

<br/>
<span style="color: red"></span>

### **1. Creating your own `class` structure**

<br/>

Suddenly, I wanted to create a dog SNS, so I was coding hard with JavaScript.

I'm trying to make a few similar object data types containing various dog information as a test.

<br/>

```jsx
var puppy1 = { type: "adog", color: "white" };
var puppy2 = { type: "bdog", color: "brown" };
```

I want to make a lot like this, but I don't want to hardcode it, so I want to create a `class` to pull out puppy objects.

So how should I make a `class`?

<br/>

### A.

<br/>

```jsx
class Dog {
  constructor(tp, co) {
    this.type = tp;
    this.color = co;
  }
}
var puppy1 = new Dog("dog", "black");
```

<br/>

### **2. This time I want to create `objects` related to cats.**

This time, I want to select several cat objects using `class`.

<br/>

```jsx
var cat1 = { type: "a-cat", color: "white", age: 5 };
var cat2 = { type: "b-cat", color: "brown", age: 2 };
```

The `type` and `color` are similar to the puppy `object` created earlier.

I want to add one more property called `age`, which is special for cats. How can I create a `class`?

It would be good to use the syntax `extends` because it is similar to the puppy `class` created in Problem 1.

<br/>

### A.

<br/>

To use the `Dog` I created above,

Use the `extends` syntax.

<br/>

```jsx
class Dog {
  constructor(tp, co) {
    this.type = tp;
    this.color = co;
  }
}

class Cat extends Dog {
  constructor(tp, co, a) {
    super(tp, co);
    this.age = a;
  }
}

var cat1 = new Cat("c-cat", "white", 5);
```

Now you can easily extract cat objects.

If you are curious about how to use parameters

All you need to do now is list all the parameters needed for the cat object in `constructor()`.

Parameters required for properties inherited from `Dog` can be put in `super()` as they are.

Or even if you think that `super()` function uses `constructor()` of `Dog` as it is.

You can easily figure out how to use it.

<br/>

### **3. I want to add a function to cat and dog `objects`.**

<br/>

**All cats and dogs** `object` can use `.getOneYearsOld()` function.

**(1)** If the `getOneYearsOld` function is used by an object created from a dog `class`, an error should be output to the console window.

**(2)** If the `getOneYearsOld` function is used by an object created from a cat `class`, it should execute a function that adds `1` to the current `age` attribute.

<br/>

### A.

<br/>

First, we added the `getOneYearsOld()` function to Dog. Because both Cat and Dog must be available.

Well, you can do this separately for Dog and Cat separately, but I did this.

So cats and dogs can all use `getOneYearsOld()`.

```jsx
class Dog {
  constructor(tp, co) {
    this.type = tp;
    this.color = co;
  }
  getOneYearsOld() {
    if (this instanceof Cat) {
      this.age++;
    }
  }
}

class Cat extends Dog {
  constructor(tp, co, a) {
    super(tp, co);
    this.age = a;
  }
}
```

Now, when cats use `getOneYearsOld()`, their age is added by 1 year.

An error should be output when dogs use it, but I added an if statement in the function to distinguish it.

<br/>

JavaScript has a nice operator called `instanceof`.

If you write `a instanceof b` like this, it is an operator that tells whether `a` is an object created from `b` or not with `true/false`.

So, I created a function called `getOneYearsOld()` and added a function that does `this.age++`, and added an `if` statement to execute this function only when `this` is `instanceof Cat`.

Now, only objects created from Cat can use `getOneYearsOld()` internal function.

<br/>

### **4. Let's use `get/set`**

I want to create a `class` that draws objects with simple game functions in JavaScript.

Create a `class` according to the following conditions. Let the `class` name be `Unit`.

<br/>

**(1)** All instances of `Unit` have **attack power, stamina** properties, and the base attack power should be set to `5` and the base stamina set to `100`.

**(2)** Every instance of `Unit` has a `getter` called `battlePoint` that measures combat strength.

`console.log( instance.battlePoint )` If you use it like this, you should output the current **Attack power plus HP** to the console window.

**(3)** Every instance of `Unit` has a `setter` called `heal`.

`instance.heal = 50` This should **increase the health attribute by 50**.

<br/>

- **Instance means an object newly created from a class.**

<br/>

### A.

<br/>

```jsx
class Unit {
  constructor() {
    this.health = 100;
    this.op = 5;
  }
  get battlePoint() {
    return this.health + this.op;
  }
  set heal(a) {
    this.health = this.health + a;
  }
}

var man = new Unit();

console.log(man.battlePoint);
man.heal = 50;
```

<br/>

1. I created a `class` called `Unit` and gave basic health and attack power to `constructor`.

2. I created a function called `battlePoint()` and it created a function that outputs the sum of health and attack power.

Added `get` to make it available without parentheses.

3. I created a function called `heal()`, and if you enter a number as a parameter, your health will increase by that amount.

Added `set` to make it available without parentheses.
