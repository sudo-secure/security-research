# Universal Exposure of Hardcoded Supabase Credentials in Next.js Builds

## 🐣 Product - https://github.com/zacktam12/HavenHub

## The Vulnerability: Client-Side Exposure of Hardcoded Credentials
When a Supabase client is initialized with hardcoded credentials directly in source files (e.g., /lib/supabase.ts), these strings survive the compilation process and become embedded in the final build artifacts.

Any developer who:

Hardcodes supabaseKey or supabaseUrl in their codebase

Builds the application with next build

Deploys the .next/ folder or makes it accessible

...will have their credentials exposed in plaintext within the compiled JavaScript bundles.


## 🐤 PoC 

Universal Exploitation Path: Finding ANY Supabase Key in Compiled Builds

An attacker does not need to know the specific project ID or key value in advance. They can locate the credentials by searching for patterns unique to Supabase initialization.

supabase.co - Every Supabase URL contains this domain

<img width="1531" height="491" alt="image" src="https://github.com/user-attachments/assets/32e591c7-80f7-437e-913b-47a076b764db" />
