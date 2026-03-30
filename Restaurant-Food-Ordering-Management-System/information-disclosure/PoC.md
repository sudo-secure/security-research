## Sensitive Information Disclosure in Restaurant Food Ordering Management System
https://github.com/arnobt78/Restaurant-Food-Ordering-Management-System--React-MERN-FullStack

## 📌 Vulnerability Summary

**Affected Software:** Restaurant Food Ordering Management System (React MERN FullStack)

**Vulnerable Component:** Backend API endpoint `/api/business-insights/test`

**Vulnerability Type:** Information Disclosure / Broken Access Control (CWE-200 / CWE-284)

**Impact:** Unauthenticated attackers can access critical business intelligence, financial records, customer order history, and performance metrics intended only for restaurant owners/admins.

## 🏷️ Description
The Restaurant Food Ordering Management System exposes a debug/test endpoint (`/api/business-insights/test`) that returns complete business analytics without requiring authentication or authorization. 

By manipulating the `timeRange` parameter (e.g., `?timeRange=*`), an unauthenticated attacker can retrieve:

- **Financial Summaries:** Total revenue ($13k+), average order value, and growth percentages.
- **Customer Data:** Names (e.g., "Test User", "Anshul Garg", "Atif Afridi"), order IDs, and specific order amounts.
- **Geographic Intelligence:** Top cities where customers are ordering from (including "new york" and "peshawar").
- **Operational Metrics:** Exact cuisine popularity (revealing that BBQ, Breakfast, and Burgers have 100% order frequency).
- **Temporal Data:** Monthly breakdown showing zero activity for 8 months followed by a spike in March, revealing business seasonality.

This data is typically found only in a password-protected Admin Dashboard. Exposing it allows competitors to reverse-engineer sales strategies, pricing, and customer distribution.

## Affected Versions
All versions up to and including the latest commit (as of March 2026) are affected. The vulnerability exists because the `/api/business-insights` routes lack authentication middleware, and the `/test` endpoint is left exposed in production.

## ⚙️ Proof of Concept (PoC)

The following unauthenticated request successfully retrieves the full business insight report.

**Request:**
```http
GET /api/business-insights/test?timeRange=* HTTP/1.1
Host: food-ordering-backend.arnobmahmud.com
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36
Accept: application/json

<img width="1523" height="200" alt="image" src="https://github.com/user-attachments/assets/7f06fa56-5fec-4325-8898-76c528dcf785" />
