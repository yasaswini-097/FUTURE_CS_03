 🔐 API Security Risk Analysis  
 JSONPlaceholder Public API Assessment  

---

 📌 Project Overview

This project presents a structured security assessment of the public demo API:

https://jsonplaceholder.typicode.com

The objective of this assessment was to analyze common API security risks aligned with the **OWASP API Security Top 10** framework.

> ⚠️ Note: JSONPlaceholder is a public demo API. This analysis is strictly for educational and learning purposes.

🎯 Scope of Testing

- Read-only API testing
- No exploitation performed
- No modification of data
- No brute force attacks
- No denial-of-service attempts

Testing focused only on publicly accessible endpoints.


 🛠 Tools Used

- Kali Linux  
- curl (Command-line HTTP client)  
- Browser DevTools  
- Git & GitHub  

---

🔍 API Endpoints Tested

| Endpoint      | Description               |
|---------------|---------------------------|
| `/users`      | Retrieves all users       |
| `/users/{id}` | Retrieves a specific user |
| `/posts`      | Retrieves posts           |
| `/comments`   | Retrieves comments        |

---

🚨 Security Findings

 1️⃣ Unauthenticated Access

Observation:
Sensitive user data is accessible without authentication.

Example:
curl https://jsonplaceholder.typicode.com/users

Risk: 
Anyone can access user information without login or API key.

Severity: Medium

2️⃣ Excessive Data Exposure
Observation: 
The `/users` endpoint exposes full user details including:
- Name  
- Email  
- Phone  
- Address  
- Geo location  
- Company details  
Risk: 
Overexposure of data may increase attack surface in real-world systems.
Severity: High
 3️⃣ Broken Object Level Authorization (IDOR)

Observation:
By modifying the user ID in the URL, data of other users can be accessed.
Example:
curl https://jsonplaceholder.typicode.com/users/1
curl https://jsonplaceholder.typicode.com/users/2
Risk:  
If implemented in real systems without proper authorization checks, this could allow unauthorized data access.
Severity:High
 4️⃣ Rate Limiting Analysis

Multiple requests were sent in a loop:

for i in {1..20}; do
  curl -s https://jsonplaceholder.typicode.com/users > /dev/null
done
Observation:  
No immediate blocking occurred.  
Headers indicate rate limiting values exist but threshold is high.
Severity: Low–Medium
5️⃣ Input Validation & Error Handling

Invalid requests tested:
curl https://jsonplaceholder.typicode.com/users/abc
curl https://jsonplaceholder.typicode.com/users/999999
Response:
```
{}
```

Observation: 
The API handles invalid input gracefully without exposing stack traces or backend errors.

Severity: Informational (Good Practice Observed)

---

# 📊 Risk Summary

| Vulnerability                     | Severity       |
|-----------------------------------|----------------|
| Unauthenticated Access            | Medium         |
| Excessive Data Exposure           | High           |
| Broken Object Level Authorization | High           |
| Rate Limiting                     | Low–Medium     |
| Input Validation                  | Informational  |

 🛡 Recommendations
- Implement authentication (JWT / API Keys)
- Apply proper object-level authorization checks
- Minimize exposed response fields
- Enforce strict rate limiting
- Implement response filtering
📚 Learning Outcomes

Through this assessment, the following concepts were practiced:

- API enumeration  
- HTTP header analysis  
- IDOR testing  
- Data exposure analysis  
- Rate limit observation  
- Secure error handling evaluation  

---

# 🧑‍💻 Author

**Yasaswini Vanukuri**  
Cybersecurity Enthusiast | API Security Learner  
