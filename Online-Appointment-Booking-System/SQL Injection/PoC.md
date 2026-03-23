**Title:** SQL Injection Vulnerability in getDay.php (Online Appointment Booking System) https://github.com/girishsaraf/Online-Appointment-Booking-System

**Summary:**
A SQL Injection vulnerability was identified in the `getDay.php` file of the *Online Appointment Booking System*. The application constructs SQL queries using unsanitized user input from POST parameters, which may allow an attacker to manipulate database queries.

---

**Affected File:**
`getDay.php`

---

**Vulnerable Code:**

```php
$query ="SELECT * FROM doctor_availability 
WHERE DID = '" . $_POST["didval"] . "' 
AND CID='" . $_POST["cidval"]."'";
```

---

**Description:**
The application directly embeds user-supplied input (`didval` and `cidval`) into an SQL query without proper sanitization or the use of prepared statements. This creates a vulnerability where crafted input may alter the intended SQL logic.

---

**Impact:**
An attacker may be able to:

* Bypass application logic
* Access unintended data from the database
* Potentially compromise data integrity depending on database permissions

---

**Proof of Concept (Conceptual):**
By submitting specially crafted input values in the POST parameters (`didval` or `cidval`), it is possible to influence the SQL query logic. For example, injecting conditional expressions may cause the query to return unintended results.

---

**Root Cause:**

* Lack of input validation
* Direct concatenation of user input into SQL queries
* Absence of parameterized queries

---

**Recommended Fix:**
Use prepared statements with parameter binding:

```php
$stmt = $conn->prepare("SELECT * FROM doctor_availability WHERE DID = ? AND CID = ?");
$stmt->bind_param("ss", $_POST["didval"], $_POST["cidval"]);
$stmt->execute();
```

---

**Severity:**
High (depending on database privileges and exposure)

---

**Conclusion:**
The vulnerability arises due to insecure handling of user input. Implementing parameterized queries and proper validation will mitigate the issue.
