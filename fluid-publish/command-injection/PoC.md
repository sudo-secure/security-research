# ☠️ Command Injection via CLI Argument Override in [fluid-publish](https://www.npmjs.com/package/fluid-publish)

Affected version: 2.4.1

## 📝 Description
The application parses user-supplied CLI arguments using publish.getCLIOpts() and merges them into runtime options:
<img width="1211" height="516" alt="image" src="https://github.com/user-attachments/assets/d0751231-d935-418c-a60b-d9a3a121f682" />

The parsed options are later deeply merged with default configuration:
<img width="1405" height="172" alt="image" src="https://github.com/user-attachments/assets/f6ae9a61-03fe-47b3-bb54-f90d043f612b" />

This allows user-controlled CLI arguments to override internal command templates such as:
- publishCmd
- publishDevCmd
- versionCmd
- vcTagCmd
- pushVCTagCmd
- changesCmd
- etc.

These values are subsequently passed into publish.execSyncFromTemplate():
<img width="1318" height="168" alt="image" src="https://github.com/user-attachments/assets/dbf1cebc-210d-41f9-b945-4289f9541026" />


Because no validation or sanitization is applied, attackers can inject arbitrary shell commands via CLI arguments.

## Impact

An attacker who can control CLI arguments can execute arbitrary commands on the host system with the privileges of the running process.

This may lead to:
- Remote Code Execution (RCE)
- CI/CD pipeline compromise
- Credential exfiltration


Example malicious CLI usage:
```js
fluid-publish --publishCmd="echo hacked && touch /tmp/pwned"
```






