---
layout: post
title: "ES2017(ES8) Async/await"
summary: "If you feel Promises are difficult, so if you don't like to use them, use async/await."
author: ge5rg2
date: "2023-02-24 11:10:15 +0900"
category: javascript
thumbnail: /assets/img/posts/async.png
keywords: javascript
permalink: /blog/async-await/
usemathjax: true
---

[Reference](https://codingapple.com/)

<br/>

If `promises` are difficult, there is an ES8 syntax that makes it much easier to use.

The keywords `async` and `await` are syntax that make Promise and then very easy, respectively.

Let's find out together.

<br/>

### **If you use the `async` keyword, a Promise object is created as a clause.**

It's literally like that. You don't need to do `new Promise()` something.

However, this keyword can only be placed before function declarations.

```jsx
async function Arithmetic() {
  1 + 1;
}
```

<br/>

Then this function itself becomes a `Promise`.

So, you can append then to <span style="color: red">when executing this function. Because it's a promise.</span>

However, unlike `promises`, only success is possible.

(Executing the function leaves a `Promise` instance (the `object` created with `new Promise()`) in its place.)

<br/>

```jsx
async function plus() {
  1 + 1;
}

plus().then(function () {
  console.log("sucess plus");
});
```

So now we can add then to execute something after the `plus()` function succeeds, just like we did when we created the Promise.

<br/>

If you want to use the result of an operation in a function in `then`

```jsx
async function plus() {
  return 1 + 1;
}

plus().then(function (result) {
  console.log(result);
});
```

You can do this.

Just write the result to the right of return. Then it is passed to the then function.

<br/>

### **If you don't like the `then()` function, you can use the `await` keyword.**

<br/>

You can use `await` inside a function using the `async` keyword.

Think of `await` as just a `promise.then()` replacement.

<span stlye="color: red">However, the syntax is much simpler than then.</span>

<br/>

Let's create a new example.

I want to create a **`Promise` that determines success/failure after executing difficult operations in a function.**

```jsx
async function plus() {
  var Arithmetic = new Promise((sucess, fail) => {
    var result = 1 + 1;
    sucess();
  });
  Arithmetic.then();
}
plus();
```

You can do this as you have done many times.

(Or if you don't want to make a `Promise`, you can use async after making `Arithmetic` a function)

<br/>

Then `Arithmetic.then()` can run specific code on success like this.

But if you don't want to see `.then()` because it's too complicated

You can use the keyword `await`.

<br/>

```jsx
async function plus() {
  var Arithmetic = new Promise((sucess, fail) => {
    var result = 1 + 1;
    sucess();
  });
  var result = await Arithmetic;
}
plus();
```

Syntax very similar to `Arithmetic.then().`

The exact meaning is **Wait for `Arithmetic Promise`, then put the result in a variable when completed**

no see.

<br/>

If you want to print the result of an operation or something like that

You said you could put a parameter in the success function, right?

```jsx
async function plus() {
  var Arithmetic = new Promise((sucess, fail) => {
    var result = 1 + 1;
    sucess(result);
  });
  var result = await Arithmetic;
  console.log(result);
}
plus();
```

The `parameter 2` in the `sucess()` function is

Stored in a variable called **var result**.

Then you can print the result of the Promise's operation.

<br/>

(Caution) If you include code that is processed **asynchronously**, the browser may freeze for a moment while waiting for await.

<br/>

### **If `await` fails, an error is thrown and the code stops**

<br/>

Let's run the code below where the `Promise` fails.

```jsx
async function plus() {
  var Arithmetic = new Promise((sucess, fail) => {
    fail();
  });
  var result = await Arithmetic;
  console.log(result);
}
plus();
```

When an `Arithmetic Promise` Fails

The code called `await Arithmetic` throws an error and stops executing the code.

Then the code at the bottom of await won't be executed anymore.

<br/>

So if the promise fails

If you don't want to stop the execution of your code, you need a slightly special method.

```jsx
async function plus(){
  var Arithmetic = new Promise((sucess, fail)=>{
    fail();
  });
  try {  var result = await Arithmetic }
  catch { Code to run if an Arithmetic Promise fails }
}

```

It is a JavaScript syntax called `try catch`.

If the code inside `try {}` throws an error and stops

Instead, the code inside the `catch {}` is executed.

<br/>

### **Example: Creating a Promise that succeeds when a `<button>` is pressed**

Q. Create a button within an HTML page

I want to create a Promise that succeeds when I click on it.

If successful, it prints 'success' to the console window.

How can I code it?

(If you need async, await, let's use it)

<br/>

```html
<button id="test">button</button>

<script>
  let currentBtn = document.querySelector("#test");
  let clickEvent = new Promise((sucess, fail) => {
    currentBtn.addEventListener("click", () => {
      sucess("Sucess!!!");
    });
  });

  const onClickBtn = async () => {
    let result = await clickEvent;
    console.log(result);
  };
  onClickBtn();
</script>
```

1. Once the above button is pressed, a Promise is created that determines success.

2. But now I tried to write a code that does `console.log()` if it succeeds, but I don't want to use then

`await clickEvent;` I wrote this.

3. But if you want to use `await`, you can only use it inside an `async functinon`, right?

So `await clickEvent;` I just wrapped the code in an `async` function.

Or maybe it was structured like this.

```jsx
<button id="test">button</button>

<script>
  async function clickEvent(){
    document.getElementById('test').addEventListener('click', function(){
      return 'Sucess'
    });
  }

  async function onClickBtn(){
    var result = await clickEvent();
    console.log(result)
  }

  onClickBtn();
</script>
```

▲But the above code doesn't work well.

I wrote an async function `clickEvent()` and put the event listener inside

I expected that pressing the button would result in a success judgment by return something, but it didn't work.

In fact, `return 'Sucess'` is not a return of an `async` function, but a return statement of a function in an `event listener`, so there is a problem.

More important than that is this.

<br/>

**1. Code in event listeners is not executed immediately. Executes when button is pressed.**

**2. So when the computer reads the code all the way, the inside of the async function clickEvent() function is equivalent to blank.**

**3. JavaScript executes by automatically filling in return undefined if there is a blank inside the function.**

(Then, by number 3, `async function clickEvent()` is automatically judged as `success()` in 0 seconds)

<br/>

so at the bottom

**var result = await clickEvent();**

This code is executed with `clickEvent()` determined to be successful in 0 seconds (because return undefined is automatically filled in the function)

Same meaning as `var result = undefined` .

That's why the code got weird.

<br/>

However, if you make it a Promise and specify `success ()` and `failure ()` cases directly

await waits nicely.
