**Title:** SQL Injection Vulnerability in get_town.php (Online Appointment Booking System) https://github.com/girishsaraf/Online-Appointment-Booking-System

**Summary:**
A SQL Injection vulnerability was identified in the `get_town.php` file of the *Online Appointment Booking System*. The application constructs SQL queries using unsanitized user input from POST parameters, which may allow attackers to manipulate database queries.

---

**Affected File:**
`get_town.php`

---

**Vulnerable Code:**

```php
$query ="SELECT * FROM clinic WHERE City = '" . $_POST["countryid"] . "'";
```

---

**Description:**
The application directly embeds user-controlled input (`countryid`) into an SQL query without sanitization or the use of parameterized queries. This allows an attacker to modify the structure of the SQL query.

---

**Impact:**
An attacker may be able to:

* Retrieve unintended data from the database
* Bypass intended filtering logic
* Enumerate available towns or related database records

---

**Proof of Concept (Conceptual):**
By providing specially crafted input in the `countryid` POST parameter, it is possible to alter the SQL query logic and influence the data returned by the application.

---

**Root Cause:**

* Direct concatenation of user input into SQL queries
* Lack of input validation
* Absence of prepared statements

---

**Recommended Fix:**
Use prepared statements with parameter binding:

```php
$stmt = $conn->prepare("SELECT * FROM clinic WHERE City = ?");
$stmt->bind_param("s", $_POST["countryid"]);
$stmt->execute();
$results = $stmt->get_result();
```

---

**Severity:**
High (depending on database permissions and exposure)

---

**Conclusion:**
The vulnerability is caused by insecure handling of user input. Using parameterized queries and proper validation will mitigate this issue.
