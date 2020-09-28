---
title: MERN - 04- রাউটিং হ্যান্ডলার
date: 2020-08-20 16:21:44
tags: [node, mern, express]
---
### রাউটিং হ্যান্ডলার
রাউটিং হ্যান্ডলার হচ্ছে একটা কলব্যাক ফাংশন যার মাধ্যমে রিকুয়েস্ট রিসিভ আর রেসপন্স সেন্ড করা যায়(সাথে ডেটা, যদি থাকে)।

app.get('/', **(request, response) => {**
    **//....**
**}**)

**নোট: রাউটিং হ্যান্ডলার হতে পারে-**
+ **একটা মাত্র ফাংশন**(উপরের উদাহরণের মত)
+ **ফাংশনের অ্যারে**
+ **একটা ফাংশন আর অ্যারের কম্বিনেশন**

## রেসপন্স হ্যান্ডল করা
### text বা html রেসপন্স
```js
app.get('/', (request, response) => {
    //...
    response.send('some text!')
})
```

### খালি রেসপন্স
```js
app.get('/', (request, response) => {
    //...
    response.end();
})
```

### শুধু স্ট্যাটাস কোড
```js
app.get('/', (request, response) => {
    //...
    response.status(404).end();
})
```

### json রেসপন্স
```js
//...
app.use(express.json())
//...
app.get('/', (request, response) => {
    //...
    response.status(404).json({error: 'object not found.'});
})

```

**নোটঃ রাউটিং হ্যান্ডলার next() নামে আরেকটা এক্সট্রা প্যারামিটার নিতে পারে।**