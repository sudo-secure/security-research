# 👀 RCE via LFI in [json-tool](https://www.npmjs.com/package/json-tool)

Affected version: 1.1.2


## 📝 Description
 The json-tool utility uses require() to load JSON files:  

<img width="1538" height="380" alt="image" src="https://github.com/user-attachments/assets/83fb9fae-2712-4665-b273-1e2aaa323fdb" />


 In Node.js, require() doesn't limit to .json files. It executes:  
- .js files as JavaScript modules
- .node files as native addons
-  Any file with valid JS syntax

 Since the 'file' parameter comes from user input with NO validation an attacker can supply a path to a malicious .js file and achieve RCE
