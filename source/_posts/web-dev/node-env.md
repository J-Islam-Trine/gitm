---
title: নোড এনভায়রনমেন্ট (NODE_ENV) ভ্যারিয়েবল
date: 2020-08-08 17:51:04
tags: [backend]
---
## NODE_ENV
NODE_ENV একটা দিয়ে অ্যাপ্লিকেশন কোন স্টেজে আছে, তা নির্দেশ করা যায়।

যেমন,
__NODE_ENV=developement__ মানে ডেভলপমেন্ট পর্যায়
__NODE_ENV=production__  মানে প্রোডাকশন পর্যায় (ডিপ্লয় করার পর)
__NODE_ENV=testing__ মানে টেস্টিং পর্যায়

## ব্যবহার
package.json-এর স্ক্রিপ্টের আন্ডারে আলাদা আলাদা ভাবে এনভায়রনমেন্ট এড করে দিতে হবে, যেমন - 

package.json
```json
{
    "scripts: {
        "start" : "NODE_ENV=production node index.js",
        "dev" : "NODE_ENV=developement nodemnon index.js",
        "tests" "NODE_ENV=test jest --verbose --runInBound"
    }
}
```

## উইন্ডোজে NODE_ENV
উইন্ডোজে NODE_ENV কাজ করবে না।

```
'NODE_ENV' is not recognized as an internal or external command,
operable program or batch file.
```

## সমাধান

*crossenv* নামের একটা প্যাকেজ ব্যবহার করা।

```
npm install --save crossenv
```

package.json ফাইলে প্রত্যেক এনভায়রনমেন্টের আগে cross-env যুক্ত করে দিতে হবে। যেমন - 
package.json
```json
"start" : "cross-env NODE_ENV=production node index.js"
```

## NODE_ENV-এর সুবিধা
+ আলাদা আলাদা এনভায়রনমেন্ট অনুসারে আলাদা আলাদা টেস্ট লেখা যাবে।
+ প্রোডাকশন এনভায়রনমেন্টের পারফরমেন্স অন্য দুইটার তুলনায় বেশি ভালো হয়।
+ আলাদা আলাদা এনভায়রনমেন্ট অনুসারে আলাদা আলাদা এনভায়রনমেন্ট ভ্যারিয়েবল সেট করা যাবে। যেমন, আলাদা আলাদা ডাটাবেজ কানেকশন স্ট্রিং।