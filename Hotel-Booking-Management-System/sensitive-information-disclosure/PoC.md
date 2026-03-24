## Sensitive Information Disclosure in Hotel Booking Management System 
https://github.com/arnobt78/Hotel-Booking-Management-System--React-MERN-FullStack


## 📌  Vulnerability Summary


Affected Software: Hotel Booking Management System (React MERN FullStack)

Vulnerable Component: Backend API endpoint /api/health/detailed

Vulnerability Type: Information Disclosure / Security Misconfiguration (CWE-200)

Impact: Exposure of sensitive system and infrastructure information to unauthenticated attackers



##🏷️ Description
The Hotel Booking Management System exposes a detailed health check endpoint /api/health/detailed that returns extensive system information without requiring authentication. This endpoint discloses:

System information: Platform (Linux), architecture (x64), Node.js version (v20.20.0), process ID (PID)

Performance metrics: Memory usage (heap, RSS), CPU usage, application uptime

Database credentials: MongoDB hostname, port, database name, connection status

This information can be leveraged by attackers for reconnaissance, targeted exploitation, and infrastructure mapping.


## Affected Versions

All versions up to and including the latest commit (as of February 2026) are affected. The vulnerability exists in the backend codebase where the health check routes are implemented without authentication middleware.


##⚙️ PoC 
GET /api/health/detailed

<img width="343" height="459" alt="image" src="https://github.com/user-attachments/assets/87409c90-55f4-4f4c-b994-fe748c4b819c" />
