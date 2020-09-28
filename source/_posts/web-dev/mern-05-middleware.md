---
title: MERN - 05 - মিডলওয়্যার
date: 2020-08-21 12:17:00
tags: [mern, express, backend]
---
## মিডলওয়্যার
ফাংশন, যা রিকুয়েস্ট-রেসপন্স সাইকল চলা কালে কাজ করে। একাধিক মিডলওয়্যার থাকতে পারে একটা অ্যাপে।

## উদাহরণ 
json রেসপন্স প্রদানের জন্য আমাদেরকে নিচের মত করে express-এর json মেথড এড করে নিতে হয়েছে, যা একটা মিডলওয়্যার।
app.js
```js
//...
app.use(express.json())
//...
```

## ফর্ম
app.js
```js
app.use(/*middleware*/)
```

## ইউসেজ
+ এরর হ্যান্ডল করা।
+ অথেনটিকেশন চেক করা।
+ ভুল এন্ডপয়েন্টে রিকুয়েস্ট পাঠালে তা হ্যান্ডল করা।
+ রিকুয়েস্টের সাথে আসা আর রেসপন্সের সাথে যাওয়া অবজেক্ট চেঞ্জ করা।

## মিডলওয়্যার বানানো
```js
const ack = (req, res, next) => {
    console.log('logged!');
    next()
}
```
মিডলওয়্যারটি next নামের একটা বাড়তি প্যারামিটার নিচ্ছে, যেইটা পরের মিডলওয়্যারকে কল করে।

**মিডলওয়্যার স্ট্যাকে থাকা এলিমেন্ট হিসেবে কাজ করে।**

## মিডলওয়্যারের ক্রম
**যে মিডলওয়্যার আগে লোড হয়, তা আগে এক্সিকিউট হয়।**

+ CORS/method-override'
+ static
+ json/রিকুয়েস্ট, রেসপন্স চেঞ্জ করা মিডলওয়্যার
+ লগার
+ কন্ট্রোলার
+ ভুল এন্ডপয়েন্টে করা রিকুয়েস্টের হ্যান্ডলার
+ এরর হ্যান্ডলার

এরর হ্যান্ডলার সব সময় শেষে যাবে। অন্য গুলো না থাকলে json() মিডলওয়্যার শুরুতে যাবে।

## এরর হ্যান্ডলার
```js
const errorHandler = (error, request, response, next) => {

    //...

  next(error)
}
```

## ভুল এন্ডপয়েন্টে করা রিকুয়েস্ট হ্যান্ডলার
```js
const unknownEndpoint = (request, response) => {
  response.status(404).send({ error: 'unknown endpoint' })
}
```
এই মিডলওয়্যার সব সময় এরর হ্যান্ডলারের আগে দিয়ে এড করতে হবে।

## মিডলওয়্যারগুলো আলাদা ফাইলে নেয়া
যে মিডলওয়্যারগুলো আলাদা, যেমন, express.json() সেগুলো app.js ফাইলে থেকে যাবে। আর যেগুলো কাস্টম, সেগুলো চাইলেই আলাদা ফাইলে নেয়া যাবে।

middlewares.js
```js
const unknownEndpoint = (request, response) => {
  response.status(404).send({ error: 'unknown endpoint' })
}

const errorHandler = (error, request, response, next) => {

    //...

  next(error)
}

module.exports = {
    unknownEndpoint,
    errorHandler
}
```