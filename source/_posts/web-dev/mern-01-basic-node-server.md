---
title: "MERN - 01 - বেসিক সার্ভার"
date: 2020-08-17 16:52:49
tags: [backend, express, node]
---

## npm প্যাকেজ তৈরি করা
```
npm init
```
চাইলে এন্টার চেপে সবগুলো অপশান স্কিপ করে ডিফল্ট সেটিং ইউজ করা যায়।

## বেসিক ওয়েবসার্ভার 
### http মডিউল যুক্ত করা
index.js
```js
const http = require('http');
```

### সার্ভার অ্যাপ
index.js
```js
const app = (request, response) => 
{
    response.writeHead(200, { 'Content-Type' : 'text/plain' });
    response.send('hello world');
}

const server = http.createServer(app)
```
writeHead() ফাংশনটি 200 OK স্ট্যাটাস কোড দিবে আর পাঠানো কন্টেন্টের টাইপ বলে দিবে।


index.js
```js
server.listen(3001, () => {
    console.log(`listening for connections at port 3001`);
})
```

এবারে অ্যাপটি 3001 পোর্টে চালু হয়ে যাবে।

### সার্ভার রান করা
প্রজেক্ট ফোল্ডারে টার্মিনাল থেকে রান করতে হবে - 
```
node index.js
```

থামানোর জন্য ctrl+c চাপতে হবে।

### package.json-এ কমান্ড এড করা
package.json ওপেন করে তার মধ্যে script-এ যুক্ত করতে হবে - 
package.json
```js
//.....
  "scripts": {
    "start": "node index.js"
  },
//....
```

### scripts-এ ভ্যালু এড করার পর সার্ভার রান করা
প্রজেক্ট ফোল্ডারে টার্মিনাল থেকে রান করতে হবে - 
```
npm start
```
থামানোর জন্য ctrl+c চাপতে হবে।




