# 📘 API Interview Cheat Sheet

## 🔹 1. What is an API?
**Definition:**  
API (Application Programming Interface) is a set of rules that allows different software systems to communicate.

**Example:**  
Weather app → calls API → gets live weather data

---

## 🔹 2. What is REST API?
**Definition:**  
REST (Representational State Transfer) is an architectural style that uses HTTP methods to perform operations on resources.

**Example:**
GET    /restaurants      → Fetch list  
POST   /orders           → Create order  
GET    /orders/{id}      → Get order  
DELETE /orders/{id}      → Cancel order

---

## 🔹 3. HTTP Methods

| Method | Use |
|--------|-----|
| GET    | Fetch data |
| POST   | Create data |
| PUT    | Update entire resource |
| PATCH  | Partial update |
| DELETE | Remove data |

**Example:**
GET    /api/products  
POST   /api/cart  
PUT    /api/users/123  
PATCH  /api/orders/10  
DELETE /api/comments/5

---

## 🔹 4. GET vs POST

### GET
- Retrieve data
- Parameters in URL
- Cacheable
- Bookmarkable

### POST
- Send data
- Data in request body
- Not cacheable
- More secure than GET

---

## 🔹 5. What is an Endpoint?
**Definition:**  
A specific URL where an API can be accessed.

**Example:**
GET  /api/accounts  
GET  /api/accounts/{id}  
POST /api/transfers

---

## 🔹 6. Request vs Response

### Request (Client → Server)
POST /api/login  
Content-Type: application/json

{
"username": "john",
"password": "pass123"
}

### Response (Server → Client)
200 OK  
Content-Type: application/json

{
"token": "abc123",
"user": { "id": 1, "name": "John" }
}

---

## 🔹 7. What is JSON?
**Definition:**  
JSON (JavaScript Object Notation) is a lightweight data format for data exchange.

**Example:**
{
"name": "Sarah",
"email": "sarah@email.com",
"address": {
"city": "San Francisco"
}
}

---

## 🔹 8. HTTP Status Codes

### Success
- 200 → OK
- 201 → Created
- 204 → No Content

### Client Errors
- 400 → Bad Request
- 401 → Unauthorized
- 403 → Forbidden
- 404 → Not Found
- 429 → Too Many Requests

### Server Errors
- 500 → Internal Server Error
- 502 → Bad Gateway
- 503 → Service Unavailable

---

## 🔹 9. What is RESTful API?
API that follows REST principles:
- Stateless
- Uses HTTP methods properly
- Structured endpoints

**Example:**
GET    /products  
POST   /products  
GET    /products/{id}  
PUT    /products/{id}  
PATCH  /products/{id}  
DELETE /products/{id}

---

## 🔹 10. What is Statelessness?
Server does not store client state.  
Each request must contain all required information.

---

## 🔹 11. What is CRUD?

| Operation | Method |
|-----------|--------|
| Create    | POST   |
| Read      | GET    |
| Update    | PUT/PATCH |
| Delete    | DELETE |

---

## 🔹 12. API Testing
**Definition:**  
Testing APIs for functionality, performance, security, and reliability.

**Tools:**
- Postman
- Swagger/OpenAPI
- SoapUI

---

## 🔹 13. What is Payload?
Data sent in request or response body.

**Example:**
{
"content": "Hello world",
"privacy": "public"
}

---

## 🔹 14. Headers

**Definition:**  
Key-value pairs providing metadata about request/response.

**Common Headers:**
Authorization: Bearer token  
Content-Type: application/json  
Accept: application/json

---

## 🔹 15. Content-Type
Specifies format of request/response body.

**Examples:**
application/json  
multipart/form-data

👉 Important for POST, PUT, PATCH

---

## 🔹 16. Accept Header
Tells server which response format client expects.

**Example:**
Accept: application/json  
Accept: text/html

---

# 🚀 Interview Tips

✔️ Always answer in 3 steps:
1. Definition
2. Example
3. Use-case

✔️ Important lines to remember:
- REST APIs are stateless
- GET is idempotent, POST is not
- Headers contain metadata
- Status codes define response result

---

# 🎯 Quick Revision

- API = communication bridge
- REST = rules using HTTP
- CRUD = Create Read Update Delete
- JSON = data format
- Status codes = result of request
- Headers = metadata
- Stateless = no server memory  