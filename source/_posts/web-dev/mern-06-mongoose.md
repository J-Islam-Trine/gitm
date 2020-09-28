---
title: MERN - 06 - মঙ্গোজ (Mongoose ODM)
date: 2020-08-21 14:28:07
tags: [backend, mongoose, express, mern]
---
## মঙ্গোজ 
Mongoose হচ্ছে মঙ্গো ডিবি (Mongo DB)-এর জন্যে একটা অবজেক্ট ডকুমেন্ট মডেলার।

## কেন মঙ্গোজ? 
+ ডকুমেন্ট ডাটাবেজের সাথে স্কিমা ইউজ করতে দেয়। 
+ ভ্যালিডেশন করা যায় সহজে। 

## ইনস্টলেশন
```
npm install --save mongoose
```

## অ্যাপে মঙ্গোজ যোগ করা
app.js
```js
const mongoose = require('mongoose');
```

## স্কিমা
কোন কালেকশনে কী ধরণে ডেটা থাকবে সেটা স্কিমার মধ্য দিয়ে নির্দিষ্ট করে দেয়া যায়।

model/order.js
```js
const orderSchema = new mongoose.Schema({
    orderNo: Number,
    client: String,
    details: Array,
})

```

## মডেল
মডেল স্কিমার ডেটা সহ নমুনা।

```js
const order = mongoose.model('User', orderSchema);
```

ডাটাবেজে এইটার কালেকশনের নাম হবে Users আর পরেরটা বলছে যে কোন স্কিমা থেকে তা বানানো।

## ভ্যালিডেশন
মঙ্গোজ দিয়ে সহজেই ডেটা ভ্যালিডেট করা যায়।

model/order.js
```js
const userSchema = new mongoose.Schema({
     username: 
    {
        type: String,
        required: [true, 'user name needed']
    },
    name: 
    {
        type: String
    },
    password: 
    {
        type: String,
        required: true
    }
})

```


