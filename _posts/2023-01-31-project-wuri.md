---
layout: post
title: "Project Wuri."
summary: "About the project"
author: ge5rg2
date: "2023-01-31 14:37:05 +0900"
category: project
thumbnail: /assets/img/project/wuri.png
keywords: project
permalink: /blog/wuri/about
usemathjax: true
---

<br/>

# Side project “Wuri”

Name called by “우리들의 다이어리, Wuri”

> **Wuri** is a side project app that allows users to keep a diary of their day, date with their lover, and parenting activities. It will feature OAuth login with Firebase, diary sharing with a lover, and diary creation and commenting. The technology stack includes React, Styled-Components, Firebase, and NotionDB. The project includes a welcome page, main page, diary page, new post page, sign out page, account page, and couple diary page. An ERD diagram is also available.

<br/>

## Background 🌐

---

Action point

1. An app that keeps a diary of the day.
2. Keep a diary of your date with your lover.
3. Parenting, keeping a diary of animals.

<br/>

## Project goal 💡

---

1. Implementation of oauth function and login using firebase
2. When setting up a lover, you can share your diary if the lover information you entered matches each other.
3. Create or comments (including modification)

<br/>

## Technology stack 👨‍🔧

---

Client - React, styled-component

Server - firebase

DB - firebase

Deploy - firebase, gh-pages

<br/>

## Schedule 📆

---

[Project Wuri](https://www.notion.so/c00f659653444fa38152b99ee6deaeb7)

<br/>

## Page component 📃

---

Welcome page → show auth method / Sign in, Sign up

Main page → Show up diary(preview) / New post / Nav var

1. Show up diary(preview): when user click each preview diary, then move to that diary page that can edit, comment(only couple diary)
2. New post: when user click this new post button, move to new-post page that can write new diary.
3. Nav var → Sign out, Account, Couple diary
   1. Sign out: sign out and move to Welcome page
   2. Account: move to account page that show user Info, delete account
   3. Couple diary: ….

Couple diary: If the user who doesn’t registered couple diary, show pop up dialog that register couple info. else move to couple diary page

<br/>

## ERD diagram

---

[A Free Database Designer for Developers and Analysts](https://dbdiagram.io/d/63f3006c296d97641d822e33)

![ERD](/assets/img/project/ERD.png)
