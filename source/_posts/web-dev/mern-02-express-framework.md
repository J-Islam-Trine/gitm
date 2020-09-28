---
title: MERN - 02 - এক্সপ্রেস ফ্রেমওয়ার্ক যুক্ত করা
date: 2020-08-18 14:53:20
tags: [node, express, backend, MERN]
---
## এক্সপ্রেস ফ্রেমওয়ার্ক
রাউট ম্যানেজ করা থেকে হেডার পাঠানো - সবই এক্সপ্রেস সহজ করে দেয়।

### ইনস্টল করা
```
npm install --save express
```

### এক্সপ্রেস যুক্ত করার পর 
index.js
```js
const express = require('express');
const app = express();

const server = http.createServer(app)

server.listen(3001, () => {
    console.log(`listening for connections at port 3001`);
})
```

## সার্ভার আর এক্সপ্রেস অ্যাপ আলাদা করা
## কেন? 
+ টেস্টিং-এর সময় সমস্যা হবে না হলে।
+ গুছানো প্রজেক্ট।

### আলাদা ফাইলে এক্সপ্রেস অ্যাপ
মূল ফোল্ডারে app.js নামে একটা ফাইল তৈরি করি।
app.js 
```
const express = require('express');
const app = express();

module.exports = app;
```

### এক্সপ্রেস অ্যাপ সার্ভার ফাইলে নিয়ে আসা
index.js
```
const app = require('./app')
```

