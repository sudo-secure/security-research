**Title:** SQL Injection Vulnerability in modifierProduit.php (Stock Management System) https://github.com/BouglaceMarouane/Stock-Management

**Summary:**
A critical SQL Injection vulnerability was identified in the modifierProduit.php file of the Stock Management System. The application constructs an SQL query by directly embedding unsanitized user input from the GET parameter ref without any validation, parameterized queries, or prepared statements. This flaw allows attackers to manipulate the structure of SQL queries executed against the database, potentially leading to data exfiltration, unauthorized data modification, or complete database compromise.


---

**Affected File:**
`modifierProduit.php`

---

**Vulnerable Code:**

```php
<?php
  $conn = new PDO("mysql:host=localhost;dbname=gestionstock", "root", "");
  $ref = $_GET['ref'];
  $errorMsg = "";

  // ... POST handling code ...

  $prd = $conn->query("SELECT * FROM Produit WHERE Ref=$ref")->fetch(PDO::FETCH_OBJ);
?>
 "'";
```

---

**Description:**
The application takes user-controlled input from the GET parameter ref and concatenates it directly into the SQL query string. No input sanitization, type casting, or parameterized queries are used. This enables an attacker to inject arbitrary SQL code that will be executed by the database.


---

**Recommended Fix:**
Replace the vulnerable code with prepared statements using parameter binding. This ensures user input is treated as data, not executable code.

---

**Severity:**
High (depending on database permissions and exposure)

---

**Conclusion:**
The insecure handling of user input in modifierProduit.php exposes the Stock Management System to SQL Injection attacks. The vulnerability exists because the ref GET parameter is directly concatenated into an SQL query without any sanitization or parameterization. Implementing prepared statements and input validation will effectively remediate this issue and protect the integrity and confidentiality of the system's data.

