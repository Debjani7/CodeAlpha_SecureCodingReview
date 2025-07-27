# CodeAlpha_SecureCodingReview

# insecure_login.py

import sqlite3

def login(username, password):
    conn = sqlite3.connect('users.db')
    cursor = conn.cursor()
    # ❌ Vulnerable to SQL Injection
    query = f"SELECT * FROM users WHERE username = '{username}' AND password = '{password}'"
    cursor.execute(query)
    result = cursor.fetchone()
    if result:
        print("Login successful!")
    else:
        print("Invalid credentials.")

if __name__ == "__main__":
    username = input("Enter username: ")
    password = input("Enter password: ")
    login(username, password)


    //Markdown

    # ✅ Secure Coding Review – Python (Login System)

## 🔍 Application:
A basic login form using Python and SQLite database.

---

## ❗ Identified Vulnerabilities:

| Vulnerability            | Description |
|--------------------------|-------------|
| SQL Injection            | Uses user input directly in query |
| No Password Hashing      | Plaintext passwords |
| No Input Validation      | Accepts raw input |
| Insecure Error Messages  | May reveal too much info |

---

## 🔧 Tools Used:
- Manual inspection
- OWASP Top 10 checklist

---

## ✅ Recommendations:

- **Use parameterized queries**:
```python
cursor.execute("SELECT * FROM users WHERE username = ? AND password = ?", (username, password))
