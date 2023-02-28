---
layout: post
title: "var let const and declaration, assignment, scope"
summary: "Summary of variable new syntax  pt.1"
author: ge5rg2
date: "2023-02-27 11:04:46 +0900"
category: javascript
thumbnail: /assets/img/posts/var_let_const.png
keywords: javascript
permalink: /blog/var-let-const/
usemathjax: true
---

[Reference](https://codingapple.com/)

<br/>

### **JavaScript variables are written like this.**

<br/>

```jsx
var name = "Kim";
```

A variable is a place to temporarily store data.

1. Give a name to the right of the keyword `var`, and insert the data to be stored in the variable with an equal sign.

2. It can contain all data such as `objects`, `arrays`, and `functions`.

3. And the part called **var name** is a declaration, and the part called **name = Kim** is a value assignment. Usually, when creating a variable, you use both at the same time.

4. And when creating a variable, you can use three keywords: `var`, `let`, and `const`.

Each of the three keywords has its own characteristics. There are some differences in the **declaration, assignment, and scope** of variables, so let's find out together.

<br/>

### **Declaration of variable**

<br/>

```jsx
var name;
let age;
const height;
```

In this way, you can declare that you will create a variable using the `var`, `let`, and `const` keywords. (Even if you don't use an equal sign, a variable is created)

However, the `var` keyword can be redeclared.

The `let` and `const` keywords cannot be redeclared.

<br/>

```jsx
let age;
let age; //error const height = 188;
const height = 180; //error
```

If you make it with `let` or `const`, you cannot redeclare a variable with the same name more than once. I get an error.

This is a useful function that prevents you from making a mistake by accidentally duplicating a variable name later.

<br/>

### **Assigning a value to a variable**

Assigning a value to a variable is

```jsx
var name;
name = "Kim";
```

▲ Assigning the value 'Kim' to the variable created in the second line is called assignment.

<br/>

Assignment can also be done at the same time as declaration.

```jsx
var name = "Kim";
```

▲ Code that declares and assigns at the same time

<br/>

However, if you make a variable `var` or `let`, it can be reassigned, but if you make it `const`, you cannot reassign the value.

If you create a variable with `const`, you can't use the equal sign to change the value later.

```jsx
let name = "Kim";
name = "Park"; // possible const age = 30;
age = 40; //error
```

`Const` is short for constant in the first place, meaning a constant value that does not change.

<br/>

- By putting an object in a `const` variable, the data within the object can be changed.

```jsx
const obj = { name: "Kim" };
obj.name = "Park"; //possible
```

The example above works because, strictly speaking, we are not reassigning a variable.

If you want to make a completely immutable object

There is a basic JavaScript function called `Object.freeze()`.

`Object.freeze()` If you put an object in parentheses, an immutable object is completed.

(But it does not freeze objects within objects)

<br/>

### **Range of variables**

<br/>

When you create a variable, it has a scope.

A `var` variable has a scope of `function`.

`let` and `const` variables are almost all `{braces}` in their scope. (`for`, `if`, `function`, etc.)

<br/>

```jsx
function fn() {
  var name = "Kim";
  console.log(name); //possible
}

console.log(name); //error
```

▲ As in the example above, if a `var` variable is created within a `function`, it can only be used within the `function`.

If you call it outside `function`, it says nothing.

<br/>

```jsx
if (1 == 1) {
  let name = "Kim";
  console.log(name); //possible
}

console.log(name); //error
```

▲ As in the example above, if you create a `let` variable within `{} curly braces`, you can use it only within curly braces.

If you call it outside the curly braces, it says "no".
