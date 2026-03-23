# Stored XSS - classroombookings

## 📌 Description
A Stored Cross-Site Scripting (XSS) vulnerability exists in the classroombookings application. An authenticated user with the role Teacher can inject malicious JavaScript into the Display Name field. The payload is stored and executed when the profile data is rendered, leading to persistent XSS.

##  🏷️ Affected Product
[classroombookings](https://github.com/classroombookings/classroombookings)
Version: 2.16.4

##  🔐 Requirements
Authenticated user
Role: Teacher

## 📍 Vulnerable Endpoint
POST /profile/save

## ⚙️ Steps to Reproduce

1. Login as a Teacher
2. Navigate to:
/profile/edit
3. In the Display Name field, insert the following payload:
' onload='alert(1)
4. Submit the form


## 📨 Request Example

POST /profile/save HTTP/2
Content-Type: application/x-www-form-urlencoded

email=&password1=&password2=&firstname=&lastname=&displayname=%27+onload%3D%27alert%281%29&ext=

<img width="891" height="532" alt="1" src="https://github.com/user-attachments/assets/f9a5d0ff-620a-422d-aee6-d6e533041115" />

## 🔁 Trigger

After saving, navigate to any page where the display name is rendered (e.g., profile page or UI elements showing username)
The JavaScript payload executes automatically

