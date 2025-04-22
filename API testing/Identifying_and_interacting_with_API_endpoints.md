
# 🧪 Lab: Finding and Exploiting an Unused API Endpoint

## 📋 Lab Description

**Goal:**  
Exploit a hidden API endpoint to purchase a **Lightweight l33t Leather Jacket** using the credentials `wiener:peter`.

**Level:** Practitioner  
**Status:** ✅ *Completed*

---

## 🔍 Phase 1: Reconnaissance

- Logged in using the provided credentials: `wiener:peter`
- Explored the application to identify visible functionality
- Captured and reviewed HTTP requests using Burp Suite
- Identified existing endpoints, such as:
  - `/api/products`
  - `/api/user/cart`
- Noticed the API request for the product 
  - `/api/products/1/price`

---

## 🧪 Phase 2: Testing & Errors

- Tried changing the API request: instead using GET replaced with OPTION --> Get the response: `only GET and PATCH methods are allowed`
- Tried to use PATCH modifying the header:
 - Removed the string in Accept parameter
 - Added Content-Type: application/json
 - Added josn body : { "price" : 0} (if not included in the header I got the response `Internal Error 5000`)

---

## 🎯 Phase 3: Exploitation

- Successful payload: 

```http
PATCH /api/hidden-purchase HTTP/1.1
Host: <host>
Content-Type: application/json

{
 "price" : 0
}
