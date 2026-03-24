**Title:** SQL Injection Vulnerability in fetchOrderData.php (PHP Inventory Management System) https://github.com/stemword/php-inventory-management-system

**Summary:**
A SQL Injection vulnerability was identified in the fetchOrderData.php file of the PHP Inventory Management System. The application constructs SQL queries by directly embedding unsanitized user input from the POST parameter orderId without any validation or parameterized queries. This flaw allows attackers to manipulate the structure of SQL queries executed against the database.

---

**Affected File:**
`php_action/fetchOrderData.php`

---

**Vulnerable Code:**

```php
$orderId = $_POST['orderId'];

$sql = "SELECT orders.order_id, orders.order_date, orders.client_name, orders.client_contact, orders.sub_total, orders.vat, orders.total_amount, orders.discount, orders.grand_total, orders.paid, orders.due, orders.payment_type, orders.payment_status FROM orders 	
    WHERE orders.order_id = {$orderId}";

$result = $connect->query($sql);
 "'";
```

---

**Description:**
The application takes user-controlled input from the orderId POST parameter and concatenates it directly into the SQL query string. No input sanitization, type casting, or parameterized queries are used. This enables an attacker to inject arbitrary SQL code that will be executed by the database.

---

**Proof of Concept (Conceptual):**
By submitting a malicious value in the orderId POST parameter, an attacker could alter the query logic. For example:

Input: 1 OR 1=1 — would return all orders instead of a single one

Input: 1 UNION SELECT username, password FROM users — could extract credentials

Input: 1; DROP TABLE orders; -- — could delete the orders table


---

**Recommended Fix:**
Replace the vulnerable code with prepared statements using parameter binding. This ensures user input is treated as data, not executable code.

---

**Severity:**
High (depending on database permissions and exposure)

---

**Conclusion:**
The vulnerability is caused by insecure handling of user input. Using parameterized queries and proper validation will mitigate this issue.
