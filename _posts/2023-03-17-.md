---
layout: post
title: "Inheritance function easily implemented in ES5 way"
summary: "If prototype, this, class, etc. are difficult, you can just do it the ES5 way."
author: ge5rg2
date: "2023-03-17 10:03:50 +0900"
category: javascript
thumbnail: /assets/img/posts/jsInheritance.jpg
keywords: javascript
permalink: /blog/inheritance-function
usemathjax: true
---

[Reference](https://codingapple.com/)

<br/>
<span style="color: red"></span>

There is a strange syntax called `Object.create()` that came out when ES5 was released.

If I want to create an object using inheritance, there is no easier syntax than this.

However, awareness is low due to `class` syntax.

<br/>

### **Using `Object.create()`**

<br/>

`Object.create(parent object);`

If you use it like this, one object data type is left in this place.

And the parent `object` written in parentheses becomes the gene `(prototype)`.

Let's take an example.

```jsx
var parent = { name: "Kim", age: 50 };
var child = Object.create(parent);

console.log(child.age); //50
```

That's how you write it.

Then, the child `object` will have its parent as `prototype`.

If you do `child.name`, `'Kim'` will be output, and if you `child.age`, `50` will be output.

Did the child successfully inherit parent properties?

This is the end of creating the inheritance function. It's very simple and easy.

<br/>

**So what if the child wants to change `age`?**

My son is not 50 years old, but he keeps saying that his age is 50.

Let's turn this into a 20-year-old.

```jsx
var parent = { name: "Kim", age: 50 };
var child = Object.create(parent);
child.age = 20;

console.log(child.age); //20
```

I just gave the value of `age: 20` to `object`, which is a child.

So now it prints '20' whenever I do it.

**Q. Why isn't the `age` of `50` inherited from the parent printed out?**

<br/>

- **How would you respond if the interviewer asked you this**
  Because I learned that there is an order in which to ask when getting certain data out of the JavaScript object data type.
  If you say, take out `child.age`

  1.  If an `object` called a child directly has an `age`, that is displayed.

  2.  If not, check the child's parent `prototype` and print the `age` if it is there.

  3.  If it is not there, search the parent's parent `prototype`.
      Print `age` in this order.

  So now the child comes out with `20`.

<br/>

### **Easy to make even for grandkids.**

<br/>

So it is said that children's children can easily make it.

Let's create a **grandson** that inherits all the attributes of the **parent** and all the properties of the **child**.

```jsx
var parent = { name: "Kim", age: 50 };
var child = Object.create(parent);
child.age = 20;

var grandson = Object.create(child);

console.log(grandson.age);
```

made grandchildren.

This is a child who inherits all the attributes of both the child and the parents.

So what do we get when we run `grandson.age`?

'20' is printed.

<br/>

- **If you still wonder why 20 is coming out**

  1.  Check if the grandchild has `age`, and

  2.  If not, check if it exists in parent `prototype`

  3.  If it's not there either, check if it's in the parent's parent `prototype` and...
      This is because it checks one by one and outputs the closest `age`.

<br/>

Anyway, this is how to inherit inheritance. Very simple, right?

Adding values is as easy as handling `object`.

Adding a function is easy because you just put it in an equal sign.

However, these days, developers apparently use `class` and `extends` syntax to create inheritance of inheritance.

People familiar with programming languages like Java will find it familiar.

There is a lot to memorize, so we may feel a bit reluctant.

<br/>

<img src="https://codingapple.com/wp-content/uploads/2020/03/5d8fac41eb3091fc2b844cba226c952b_155618.png" width="100%"  height="100%" title="react" alt="react" />

▲ In particular, you can sometimes see the `extends` syntax when looking at the code written with the old React syntax.
