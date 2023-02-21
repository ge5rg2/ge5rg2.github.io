---
layout: post
title: "ES6 Promise Simple Walkthrough"
summary: "ES6 Promise Simple Walkthrough"
author: ge5rg2
date: "2023-02-20 18:30:10 +0900"
category: javascript
thumbnail: /assets/img/posts/js-promise.png
keywords: javascript
permalink: /blog/promise-walkthrough/
usemathjax: true
---

[Reference](https://codingapple.com/)

### **Q1. <img> I want to run a specific code on successful image loading.**

<br/>

I want to execute some code when the image inside the HTML finishes loading.
<br/>

```html
<img id="test" src="https://codingapple1.github.io/kona.jpg" />
```

I want to print success in the console window when this image is loaded, and failure in the console window if the load fails.

I want to make it using the then and catch functions of the `Promise` syntax. How can I code it?

<br/>

(Note) You can check that image loading is complete by attaching an event listener called load to <img>.

(Note) You can check that image loading has failed by attaching an event listener called error to <img>.

<br/>

### **Q2. I want to run some code when the `Ajax` request succeeds.**

<br/>

If you make a `GET request` to the path `https://codingapple1.github.io/hello.txt` , you will receive a greeting message.

If you make a `GET request` here and it succeeds,

I want to display the greeting received through `Ajax` to the console window using the then function of Promise.

How can I do it?

<br/>

(Since the `jQuery` done function itself has a Promise function, the code may be a bit redundant and useless, but let's try it as an exercise.)

```html
jQuery CDN
<script src="https://code.jquery.com/jquery-3.4.1.min.js"></script>
```

<br/>

### **Q3. Promise chaining**

<br/>

After making a `GET request` to the path `https://codingapple1.github.io/hello.txt` in problem 2
I used .then to print the greeting to the console window.

This time, immediately after that, make another `GET request` to the path `https://codingapple1.github.io/hello2.txt` I want to print the greeting again using .then.

<br/>

How can I update the code created in step 2?

<br/>

### **Q1 Answer**

<br/>

To determine whether `<img>` with id test has been loaded / failed to load

```jsx
var img = document.querySelector('#test');

img.addEventListener('load', function(){
    Code to be executed on successful loading
});
img.addEventListener('error', function(){
    Code to run when loading fails
});
```

Then, let's write the code to execute `.then()` when loading is successful using `Promise` and `.catch()` when loading fails.

```jsx
var imgLoading = new Promise(function (sucess, fail) {
  var img = document.querySelector("#test");
  img.addEventListener("load", function () {
    sucess();
  });
  img.addEventListener("error", function () {
    fail();
  });
});

imgLoading
  .then(function () {
    console.log("Sucess!");
  })
  .catch(function () {
    console.log("Fail :(");
  });
```

In `Promise`, you can create the number of cases where `success()` and `failure()` are executed.

That way, you can now use `.then()` `.catch()` to execute specific code on success/failure.

<br/>

### **Q2 Answer**

<br/>

```jsx
var pro = new Promise(function (sucess, fail) {
  $.get("https://codingapple1.github.io/hello.txt").done(function (result) {
    sucess(result);
  });
});

pro.then(function (result) {
  console.log(result);
});
```

<br/>

### **Q3 Answer**

<br/>

```jsx
var pro = new Promise(function (sucess, fail) {
  $.ajax({
    type: "GET",
    url: "https://codingapple1.github.io/hello.txt",
  }).done(function (result) {
    sucess(result);
  });
});

pro
  .then(function (result) {
    console.log(result);

    var pro2 = new Promise(function (sucess, fail) {
      $.get("https://codingapple1.github.io/hello2.txt").done(function (
        result
      ) {
        sucess(result);
      });
    });

    return pro2;
  })
  .then(function (result) {
    console.log(result);
  });
```

So, Promise 2 is created in the first then, and Promise 2 makes the second ajax request and determines success.

And I created a function that returns Promise 2.

Then, you can run the code consecutively by adding then to the end.
The flow is like this.

1. If the first promise succeeds, the code in `then()` is executed.
2. But there is Promise 2 inside. If Promise 2 succeeds
3. Execute the code inside `then()` at the back.
   So this way you can step through your code using promises.

<br/>
