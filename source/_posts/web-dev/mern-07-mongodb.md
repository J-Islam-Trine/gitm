---
title: MERN - 07 - মঙ্গোডিবিতে ডাটা রাখা, মুছা, আপডেট ও দেখা
date: 2020-08-21 14:51:59
tags: [express, mern, mongodb, mongoose, backend]
---

### MongoDB Atlas-এ যুক্ত হওয়ার জন্য কানেকশন স্ট্রিং
[এখান](https://docs.atlas.mongodb.com/getting-started/) থেকে ছবি সহ বিস্তারিত নির্দেশনা পাওয়া যাবে।

## Dotenv 
dotenv-এর মাধ্যমে কানেকশন স্ট্রিং নোডের এনভায়রনমেন্ট ভ্যারিয়েবল হিসেবে .env নামের একটা ফাইলে স্টোর করে রাখা যায়।

### ইনস্টলেশন 
```
npm install --save dotenv
```

### .env ফাইল
মূল ফোল্ডারে .env নামের একটা ফাইল তৈরি করা যাক।

### কানেকশন স্ট্রিং রাখা।
.env ফাইলের মধ্যে - 
DB_URL=mongodb+srv://<username>:<password>@cluster0.gpsrn.mongodb.net/<database>?retryWrites=true

এবারে আমাদের অ্যাপে process.env.DB_URL থেকে ভ্যালুটা নেয়া যাবে।

## ডাটাবেজের সাথে কানেক্ট করা
```js
mongoose.connect(config.DB_URL, {useNewUrlParser: true, useUnifiedTopology: true})
```

## ডিসকানেক্ট করা
```
mongoose.connection.close();
```

**অনেক ক্ষেত্রে কোন একটা এন্ডপয়েন্টের জন্য রিকুয়েস্ট-রেসপনস শেষ করার পর কানেকশন ক্লোজ করে দিলে এরপরে অন্য কোন এন্ডপয়েন্টে পাঠানো রিকুয়েস্টের সময় ডাটাবেজের সাথে কানেক্ট নাও হতে পারে।**

**এখানে Person মডেলের কথা মাথায় রেখে উদাহরণ দেয়া হয়েছে।**

## সব আইটেম আনা
```js
const allPersons = await Person.find({})
res.json(allPersons)
```

## একটা আইটেম আনা
এটা কাজ করবে আইডির উপর ভিত্তি করে। 
```js
const id = req.params.id;
const singlePerson = await Person.findById(id);
res.json(singlePerson);
```

## ডাটা পোস্ট করা
```js
const newData = new Person({
    name: 'some name',
    age: 41
})

const response = await newData.save();
res.json(response);
```

## ডাটা আপডেট করা
```js
const id = req.params.id;
const newData = {
    name: 'some name',
    age: 42
}

const response = await Person.findByIdAndUpdate(id, newData, {new: true});
res.json(response);
```
+ newData কিন্তু model-এর অবজেক্ট নয় বরং প্লেইন অবজেক্ট।
+ new: true মানে আপডেট করার পর নতুন ভ্যালু পাঠাবে। false দেয়া থাকলে পুরনোটা পাঠাতো।

## ডেটা ডিলিট করা
```js
    await Order.findByIdAndRemove(req.params.id);
    res.status(204).end();
```

+ এই ক্ষেত্রে রেসপন্সে কোন ডেটা আসবে না।
+ ডিলিট হোক আর না হোক, এভাবে স্ট্যাটাস কোড 204-ই যাবে।






