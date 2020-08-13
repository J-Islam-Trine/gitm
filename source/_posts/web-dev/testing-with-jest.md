---
title: Jest দিয়ে টেস্টিং
date: 2020-08-08 02:35:58
tags: [frontend, testing]
---

## Jest ইনস্টল করা

```
npm install --save-dev jest
```

## Jest কেন ডেভলপমেন্ট ডিপেন্ডেন্সি?
যেহেতু Jest শুধু মাত্র ডেভলপমেন্টের সময় ইউজ করা হচ্ছে (টেস্টিং), সে জন্যেই এটা ডেভ ডিপেন্ডেন্সি।

## টেস্ট রান করার জন্য রান কমান্ড এড করা
package.json-এ Scripts-এ এড করতে হবে - 
```json
//

  "scripts": {
    "tests": "jest --verbose"
  }
```
এখন npm tests বা npm run tests লিখে টেস্ট রান করা যাবে।

## টেস্ট এনভায়রনমেন্ট বলে দেয়া
package.json-এর একদম নিচের লাইনে যুক্ত করি - 
```json
"jest" : {
    "testEnvironment: "Node"
}
```

## টেস্ট ফাংশন ক্রিয়েট করা
একটা ফাইলে যে ফাংশনটা টেস্ট করবো, সেটা লিখে নিই - 

multiply.js
```js
const multiply = (x,y) => {
    return x*y;
}
```

এবারে ফাইলটাতে module.exports এর মাধ্যমে ফাংশনটা এক্সপোর্ট করি।

muliply.js
```js
module.exports = {
    multiply,
}
```

এবারে এই ফাংশনের জন্যে টেস্ট লেখি। টেস্টগুলো সব সময় .test.js নামের এক্সটেনশনওয়ালা ফাইলের মধ্যে থাকবে। যেমন - tests_for_multiply.test.js

## টেস্ট ফাইলে ফাংশন ইমপোর্ট করা

```
const multiply = require('multiply.js').multiply
```

## টেস্ট গ্রুপের নাম এড করা 
describe() দিয়ে টেস্টের নাম দেয়া যায় - 

multiply.test.js
```js
describe('multiply', ()=>{

})
```

## আলাদা আলাদা টেস্টের নাম

multiply.test.js
```js
describe('multiply', ()=> {
        test('two time three is six', ()=> {

        })
})
```

## টেস্ট করা
multiply.test.js
```js
describe('multiply', ()=> {
        test('two times three is six', ()=> {
                const result = multiply(2,3);
                expect(result).toBe(6);
        })
})
```

expect() ফাংশন multiply()-কে কল করে পাওয়া ভ্যালুর মান toBe()-তে দেয়া মানের সমান হবে ধরে নিচ্ছে।

## টেস্ট রান করা (সব টেস্ট)
আগে package.json-এ এড করা কমান্ড দিয়ে
```
npm run tests
```

## আরো টেস্ট ফাংশন 
চাইলে একই ফাইলে একাধিক ফাংশন এড করা যাবে। তবে সেগুলোর জন্যে টেস্ট আলাদা আলাদা ভাবে লিখলেই ভালো।


## একটা মাত্র টেস্ট রান করা
describe() ফাংশন লেখার সময় দেয়া নাম দিয়ে একটা মাত্র টেস্ট রান করানো যায় -

```
npm run tests -- -t 'multiply'
```

আবার চাইলে একটা নির্দিষ্ট টেস্টও রান করানো যায় - 

```js
npm run tests -- -t 'two times three is six'
```

সেম কমান্ড আবার তা 'times' শব্দটা যতগুলা টেস্টের নামে আছে, সেই সবগুলা টেস্ট রান করবে

```js
npm run tests -- -t 'times'
```

## টেস্টের আউটপুট 

```
PASS tests/tests_for_multiply.test.js
  multiply
    √ two time three is six (5 ms)

Test Suites: 3 skipped, 1 passed, 1 of 4 total
Tests:       6 skipped, 1 passed, 7 total
Snapshots:   0 total
Time:        1.764 s
Ran all test suites with tests matching "multiply".
```

## toBe বনাম toEqual
টেস্ট করার ফাংশন যদি আউটপুট দেয় নাম্বার/স্ট্রিং তাহলে toBe() দিয়েই টেস্ট করা যাবে। অবজেক্ট/অ্যারে হলে toEqual() ব্যবহার করতে হবে - 

```js
describe('Favorite Blog', () => {
    const zeroBlogs = [];
    test('zero blog, no favorite', ()=> {
        expect(favoriteBlog(zeroBlogs)).toEqual({ });
    });
});
```

কারণ অবজেক্টের ক্ষেত্রে ব্যাপারটা একই বইয়ের দুইটা কপির মতন। দুইটা একই বই, কিন্তু আলাদা আলাদা বস্তু।



