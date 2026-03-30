## Sensitive Information Disclosure in Restaurant Food Ordering Management System
https://github.com/arnobt78/Restaurant-Food-Ordering-Management-System--React-MERN-FullStack

## 📌 Vulnerability Summary

**Affected Software:** Restaurant Food Ordering Management System (React MERN FullStack)

**Vulnerable Component:** Backend API endpoint `/api/business-insights/debug-orders`

**Vulnerability Type:** Information Disclosure / Broken Access Control (CWE-200 / CWE-284)

**Impact:** Unauthenticated attackers can access the complete order database including customer locations, order amounts, restaurant details, and timestamps. This exposes user privacy, business intelligence, and competitive data.

## 🏷️ Description

The Restaurant Food Ordering Management System exposes a debug endpoint `/api/business-insights/debug-orders` that returns the entire order history without requiring any authentication or authorization. This endpoint is clearly intended for debugging purposes but has been left accessible in production.

An unauthenticated attacker can retrieve:

- **Complete Order Count:** Total number of orders (28 orders exposed)
- **Customer Geographic Data:** Exact city locations for each order (Kafr El-Shaikh, Ghaziabad, New Delhi, Hh, etc.)
- **Financial Transaction Data:** Exact order amounts ($699, $849, $1498, etc.)
- **Temporal Intelligence:** Precise timestamps showing when each order was placed (down to the millisecond)
- **Restaurant Intelligence:** Restaurant ID, business name ("Hotel Eat 'em All"), and complete cuisine menu (10+ cuisine types)
- **Order ID Enumeration:** Sequential/guessable order IDs that could be used for further attacks

This data is typically restricted to authenticated restaurant administrators. Exposure allows competitors to analyze order volume, pricing strategies, peak ordering times, and geographic customer distribution.

## Affected Versions

All versions up to and including the latest commit (as of March 2026) are affected. The vulnerability exists because debug endpoints are not protected by authentication middleware and are left enabled in production environments.

## ⚙️ Proof of Concept (PoC)

The following unauthenticated request successfully retrieves the complete order database.

**Request:**
```http
GET /api/business-insights/debug-orders HTTP/1.1
Host: food-ordering-backend.arnobmahmud.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36
Accept: application/json
```
<img width="1590" height="447" alt="image" src="https://github.com/user-attachments/assets/7df0a6c7-87b8-447f-ac97-2217b2765cc4" />
