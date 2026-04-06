# 👽 Hardcoded Cryptographic Key in [muller](https://www.npmjs.com/package/muler?activeTab=code) 

Version: 1.1.1

## Executive Summary
The package contains a statically hardcoded encryption key (d6F3Efeq) used to protect user passwords. This key is identical for every installation of the library, making the encryption completely ineffective and rendering all stored credentials publicly readable by anyone who knows the key.

## Vulnerable Code Location
https://www.npmjs.com/package/muler?activeTab=code

<img width="262" height="70" alt="image" src="https://github.com/user-attachments/assets/69467fcb-92af-40d1-9059-abb38d572b41" />


## Why This Is Critical

- Key is public. Anyone who downloads the npm package sees the key
- Key never changes. Same key for all users, all deployments, all time
- Stored credentials exposed. Passwords saved in /tmp/.mule_settings can be decrypted by anyone with the key


