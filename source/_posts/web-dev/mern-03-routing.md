---
title: "MERN - 03 - রাউটিং"
date: 2020-08-20 16:07:20
tags: [backend, express]
---
## রাউটিং
রাউটিং হচ্ছে এন্ডপয়েন্ট অনুসারে সার্ভারের রেসপন্স ডিফাইন করে দেয়া।

## রাউটগুলোর সাধারণ রুপ
```
app.METHOD(PATH, HANDLER)
```

## উদাহরণ
app.js
```js
app.get('/', (request, response) => {
    //....
})
```

## METHOD
সার্ভারের কাছে পাঠানো রিকুয়েস্টের মেথড যেমন, GET, PUT, POST তবে ছোট হাতের অক্ষরে।

অতি আশ্চর্যজনক ভাবে express js যে শুধু get, put post, delete মেথডই চিনে শুধু তা নয়, বরং [আরো বেশ কিছু মেথড](https://expressjs.com/en/4x/api.html#app.METHOD) সাপোর্ট করে। যেমন, subscribe, move, notify, patch ইত্যাদি।

[MDN reference](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)

## PATH
এটা একটা স্ট্রিং, যা রিসোর্স অনুসারে সার্ভারের কাছে আলাদা আলাদা রিকুয়েস্ট পাঠাতে দেয়।

**পাথ regex প্যাটার্নেরও হতে পারে।**

যেমন,
_/users_ ইউজারের জন্য
_/notes_ নোটস-এর জন্য

### এন্ডপয়েন্ট
মেথড আর পাথের কম্বিনেশনে হয় এন্ডপয়েন্ট, যেমন
```js
app.get('/users', (request, response) => {
    //....
})

app.post('/users', (request, response) => {
    //....
})
```

দুইটার পাথ একই বাট মেথড আলাদা। তাই দুইটা দুই এন্ডপয়েন্ট হিসেবে বিবেচিত হবে।

### রাউট প্যারামিটারস (route parameters)
রাউট প্যারামিটার হচ্ছে পাথের মাধ্যমে পাস করা ভ্যালু।

```js
app.get('/users/:id', (request, response) => {
    const id = request.params.id;
})
```
যা পরে request.params থেকে একসেস করা যায়।