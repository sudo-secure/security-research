# File Upload to RCE - School Management System

## 📌 Description
A file upload vulnerability exists in the School Management System that allows authenticated users (Admin or Teacher) to upload arbitrary files, leading to Remote Code Execution (RCE).

## 🏷️ Affected Product
School Management System  
https://github.com/ProjectsAndPrograms/school-management-system

## 🔐 Requirements
- Authenticated user
- Role: Admin or Teacher

## 📍 Vulnerable Endpoint
POST /school-management-system-main/school-management-system-main/assets/updateProfilePic.php

## ⚙️ Steps to Reproduce
1. Login as Admin or Teacher
2. Navigate to:
   /admin_panel/settings.php
3. Use the profile picture upload functionality
4. Intercept the request in Burp Suite
5. Modify the uploaded file to a PHP payload:
<img width="623" height="183" alt="image" src="https://github.com/user-attachments/assets/2f1a2388-98ce-4812-8279-a39aab2d9844" />

6. Upload the file. In response, you will receive the path to the uploaded file:
<img width="650" height="178" alt="image" src="https://github.com/user-attachments/assets/4a3eba59-c30c-4854-9c48-3820c9e80bb1" />

7. Access the uploaded file via browser
<img width="1220" height="184" alt="image" src="https://github.com/user-attachments/assets/1957c48b-e243-4314-9d95-c6f397f9f513" />


⚠️ Impact
An attacker can execute arbitrary code on the server, potentially leading to full system compromise.
