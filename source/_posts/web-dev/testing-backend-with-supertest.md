---
title: Supertest দিয়ে ব্যাকএন্ড টেস্টিং
date: 2020-08-09 07:38:30
tags: [backend, testing]
---

## ইনস্টলেশন 

Supertest
```
npm install --save-dev supertest
```

Jest(না ইনস্টল করা থাকলে)
```
npm install --save-dev jest
```

## testEnvironment ডিফাইন করা
jest.config.js নামে একটা ফাইল তৈরি করি প্রজেক্টের মূল ফোল্ডারে

jest.config.js
```js
module.exports = {
    testEnvironment: 'node'
}
```

## টেস্ট ফাইল ক্রিয়েট করা

.test.js এক্সটেনশনের একটা ফাইল বানাই, যেমন: tests_for_api.test.js

## Supertest যুক্ত করা 
tests_for_api.test.js
```js
const supertest = require('supertest')
```

## Supertest-কে app পাস করা 
tests_for_api.test.js
```js
const app = require('../app)
const api = supertest(app)
```
**এখানে app হচ্ছে express app ফাইলটা, যেটাতে রাউটগুলো আর মিডলওয়্যার দেয়া রয়েছে। এটা করার উপায় হচ্ছে, সার্ভার আর অ্যাপ আলাদা আলাদা ফাইলে ডিক্লেয়ার করা।**

## টেস্ট
```js
test('notes are returned as json', async () => {
        await api
        .get('/orders')
        .expect(200)
        .expect('Content-Type', /application\/json/)
})
```

## টেস্টের পর

```js
afterAll(() => {
    mongoose.connection.close();
})
```
কানেকশন না ক্লোজ করলে অপারেশন রান করতে থাকবে টেস্ট রান হয়ে যাওয়ার পরেও।

আমি এখানে mongoose ODM ইউজ করেছি। যদি অন্য কিছু ইউজ করা হয়, তাহলেও সেটাকে ইমপোর্ট করে নিয়ে আসতে হবে। আমি শুরুতেই mongoose ইমপোর্ট করে নিয়েছি।

```js
const mongoose = require('mongoose')
```

## টেস্ট রান করা
যখন Jest দিয়ে সবগুলো টেস্ট রান করবো, তখন এটাও রান হয়ে যাবে। 

অথবা 

```
npm test -- tests/tests_for_api.test.js
```

## টেস্টের জন্যে ডাটাবেজ
টেস্ট মূল ডাটাবেজের উপর রান না করে আলাদা একটা ডাটাবেজের উপর রান করানোই ভালো। 

ধরি, ভ্যালু আপডেট হচ্ছে কি না টেস্ট করা হবে, যদি কারেন্ট ডাটাবেজের উপর টেস্ট রান করা হয় তাহলে ইউজার যদি ডাটাবেজে থাকা সেই ভ্যালু ডিলিট করে দেন, তাহলে টেস্টের সময় তা ফেইল করে যাবে। ফলে ইনকনসিস্টেন্সি তৈরি হবে।

## টেস্ট রান করানোর আগে
এমন ভাবে টেস্ট সেট করা যাক যেন ডাটাবেজে থাকা আগের ডাটা মুছে দিয়ে একটা নির্দিষ্ট সেট প্রতি বারই নতুন করে ডাটাবেজে ইনসার্ট হয়। 

আগে মঙ্গোজের মডেলটা ইমপোর্ট করি - 

```js
const Order = require('../models/order')
```

```js
beforeEach(async () => {
    await Order.deleteMany({})
    let i =0;
    while (i < dummyOrders.length)
    {
        let newOrder = new Order(dummyOrders[i]);
        await newOrder.save();
        i++;
    }
})
```

beforeEach() প্রতিটা আলাদা আলাদা টেস্ট রান করার আগে ডাটাবেজের ডাটা ডিলিট করবে আর আগে থেকে স্থির করে রাখা dummyOrders নামের ভ্যারিয়েবলে থাকা ডাটা একটা লুপের মধ্যে দিয়ে ডাটাবেজে সেভ করবে।

**এখানে forEach() কাজ করবে না, কলব্যাক নেয় এমন কোন লুপ দিয়ে এটা করা যাবে না কারণ তখন await অংশটুকু async ফাংশন থেকে আলাদা হয়ে যাবে। তাই অতি পরিচিত while লুপই ভরসা।**

## হেল্পার ফাংশন 
API-এর কোন একটা এন্ডপয়েন্ট কাজ করছে কি না, তা নিশ্চিত হয়ে দেখার জন্যে যদি ডাটাবেজ থেকে ডাটা আবার রিট্রিভ করতে হয়, তখন তার জন্য GET এন্ডপয়েন্ট ব্যবহার না করে, আলাদা ভাবে অন্য কোন ফাংশনের মধ্যে দিয়ে করাই ভালো। 

