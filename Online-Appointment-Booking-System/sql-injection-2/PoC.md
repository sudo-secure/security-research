**Title:** SQL Injection Vulnerability in getclinic.php (Online Appointment Booking System) https://github.com/girishsaraf/Online-Appointment-Booking-System

**Summary:**
A SQL Injection vulnerability was identified in the `getclinic.php` file of the *Online Appointment Booking System*. The application constructs SQL queries using unsanitized user input from POST parameters, allowing potential manipulation of database queries.

---

**Affected File:**
`getclinic.php`

---

**Vulnerable Code:**

```php
$query ="SELECT * FROM clinic WHERE Town = '" . $_POST["townid"] . "'";
```

---

**Description:**
The application directly incorporates user-controlled input (`townid`) into an SQL query without any sanitization or parameterization. This behavior allows an attacker to alter the structure of the SQL query.

---

**Impact:**
An attacker may be able to:

* Retrieve unintended records from the database
* Bypass filtering conditions
* Enumerate database contents depending on application behavior

---

**Proof of Concept (Conceptual):**
By supplying crafted input in the `townid` POST parameter, it is possible to manipulate the SQL query logic and influence the results returned by the application.

---

**Root Cause:**

* Direct concatenation of user input into SQL queries
* Absence of input validation
* No use of prepared statements

---

**Recommended Fix:**
Use parameterized queries (prepared statements):

```php
$stmt = $conn->prepare("SELECT * FROM clinic WHERE Town = ?");
$stmt->bind_param("s", $_POST["townid"]);
$stmt->execute();
$results = $stmt->get_result();
```

---

**Severity:**
High (depending on database exposure and privileges)

---

**Conclusion:**
The vulnerability is caused by improper handling of user input. Implementing prepared statements and proper validation will effectively mitigate the issue.
