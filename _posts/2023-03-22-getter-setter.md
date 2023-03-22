---
layout: post
title: "Find out why getters and setters are used instead"
summary: "Let's look at the JavaScript getter and setter syntax that many people wonder why they use it."
author: ge5rg2
date: "2023-03-22 18:28:30 +0900"
category: javascript
thumbnail: /assets/img/posts/getset.png
keywords: javascript
permalink: /blog/getter-setter
usemathjax: true
---

[Reference](https://codingapple.com/)

<br/>
<span style="color: red"></span>

To put it shallowly, it is a keyword that allows functions in objects to be used without parentheses.

If you go deeper, you can think of it as a keyword used to preserve the integrity of data.

<br/>

When modifying or outputting data, the trend is to indirectly handle it with functions rather than directly touching the original data.

You can see it as a kind of coding technique that fits there.

To understand this, you need to know about the methodology of handling `object` data.

<br/>

### How to retrieve `object` data with a function

<br/>

```jsx
var man = {
  name: "Kim",
  age: 30,
};
```

What if you want to print out your next year's age?

`man.age + 1` Can I do this?

you're right. However, developers who think about the future <span style="color: red">create and use a function that outputs the age of the next year</span>

<br/>

```jsx
var man = {
  name: "Kim",
  age: 30,
  nextAge() {
    return this.age + 1;
  },
};
```

If you create a function like this

If you use `man.nextAge()` like this, the next year's age will be output, right? It should print '31'.

This method of extracting and using data like this is in vogue these days.

<br/>

Why are you doing this

- The more complex the data in `object` is, the easier it is to create a function to retrieve the data.
- It is safe to prevent mistakes by not touching the `name` and `age` variables inside.

Especially when you want to extract only a few of the data you want inside a very long `object`.

If you create a function like this in advance, you don't have to develop the function every time.

<br/>

(reference)

In other languages, code works in `class` units.

Sometimes inside a `class` we have variables that we want to protect from the outside world.

In that case, I make a lot of functions like that and use them. It can be seen that such a coding style is applied to JavaScript as it is.

(Protection means just to prevent accidental modification)

<br/>

### How to modify `object` data with functions

<br/>

This time we want to modify the `age` data in `object`.

I want to change it to '40'. What should I do?

`man.age = 40`

However, forward-thinking developers <span style="color: red">create and use functions to modify data.</span>

```jsx
var man = {
  name: "Kim",
  age: 30,
  setAge(a) {
    this.age = a;
  },
};
```

Added a function called `setAge()` inside the object.

And this function can input one parameter, and it plays the role of inserting that parameter into `this.age` as it is.

Then, if you write `man.setAge(40)` like this, you can freely change the age.

<br/>

`man.age = 40` Not so easy

Why does `man.setAge(40)` do this?

- You can prevent mistakes by not directly touching the `name` and `age` variables inside.

Think of it as creating a single layer of safety.

<br/>
What is a safety device?

```jsx
man.setAge("40");
```

▲ I need to insert a number for my age, but what if I accidentally insert the character `'40'` like this?

**It stores just fine.** Data is polluted.

It can also cause an error later when you want to add `1` to the age.

<br/>

However, if you use a function that modifies data, you can add a little bit of safety.

```jsx
var man = {
  name: "Kim",
  age: 30,
  setAge(a) {
    this.age = parseInt(a);
  },
};

man.setAge("200"); //The number 200 is saved even though a character is entered
```

▲ Did you add a function in the `setAge()` function?

The `parseInt()` function is a nice JavaScript built-in function that converts a character like `'40'` into the number `40`.

**Safety devices** that convert text into numbers can also be easily developed.

So I think I can understand a little bit of crazy people who bother to make a function and modify the data.

<br/>

### If writing a function is complicated, add `get/set` keywords

<br/>

Are there any downsides to writing a function?

`setAge(40)` You have to write parentheses like this, and it becomes too complicated to insert data.

If so, just add the `get/set` keywords next to the function.

<br/>

```jsx
var man = {
   name : 'Kim',
   age: 30;
   set setAge(a){
     this.age = parseInt(a)
   }
}

man.setAge = 40;//If you add the set keyword, you can use the function like this
```

▲ When creating the `setAge()` function, add the keyword `set` to the left.

You can now enter or type data with an equal sign.

It's easy to see and intuitive, right?

That's why we use `set`. And functions with `set` are called `setters`. (meaning a function that `set` (modifies) data)

<br/>

```jsx
var man = {
  name: "Kim",
  age: 30,
  get nextAge() {
    return this.age + 1;
  },
};

console.log(man.nextAge); //get You can use the function like this by adding keywords
```

▲ When creating a function called `nextAge()`, you can use the `get` keyword.

Then we can now retrieve the data using `nextAge` without parentheses.

It's easy to see and intuitive, right?

So we use `get`. And functions with `get` prefix are called `getters`. (meaning a function that `get` data)

<br/>

### The criteria for using `get/set` are

<br/>

You can just use `get' for functions that pull out, bring in, or `get' data.

You can use `set` for functions that input, modify, or `set` data.

And there are rules too.

The `set` function is a function that inputs and modifies data, so there must be one parameter.

A `get` function must not have parameters and must have a `return` within the function.

<br/>

If you use it wrong, it tells you the error, so there's nothing to memorize

Usually, functions that feel like `get` are not too difficult if you add `get`.

<br/>

### `get/set` used in `class`

<br/>

When creating a function within a `class`, you can use the `get/set` keywords to create a `getter/setter` function.

```jsx
class man {
  constructor() {
    this.name = "Park";
    this.age = 20;
  }
  get nextAge() {
    return this.age + 1;
  }
  set setAge(a) {
    this.age = a;
  }
}

var man1 = new man();
```

If you want to use functions in `class` as `getter/setter`, you can do this.

Now the newly drawn `object`, `man1`

`man1.nextAge**;**`

`man1.setAge = 50**;**`

You can use it like this.

<br/>

The usage of `getter/setter` in `class` is the same as described above.

It is used to conveniently modify the contents of newly drawn objects.

It doesn't matter if you don't have `get/set` keywords.
