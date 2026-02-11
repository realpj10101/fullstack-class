
# 🔐 Token & JWT

---

# 🪪 What is a Token?

A **token** is a digital key that proves a user has been authenticated.

### Analogy

Imagine a security guard at a building entrance:

1. You show your ID.
    
2. The guard verifies it.
    
3. He gives you a paper (token).
    
4. As long as you hold that paper, you can move freely inside.

> The token replaces repeated identity checks.

---

# 📦 What is JWT?

**JWT (JSON Web Token)** is an industry standard for tokens — **RFC 7519**.

It is **self-contained**, meaning:

> The server does NOT need to query the database to understand who the user is.

---

## Example JWT Payload

```json
{
  "userId": "123",
  "role": "admin",
  "exp": 1719830400
}
```

From this token, the server knows:

- 👤 Who is the user? → `userId: 123`
    
- 🛡 What is the role? → `admin`
    
- ⏳ Until when is it valid? → `exp`

---

# 🧠 JWT is Self-Contained

A JWT may include:

---

## 1️⃣ Credentials

Used to identify the user without DB lookup

- `userId`
    
- `username`

---

## 2️⃣ Claims

Statements about the user

- `"role": "admin"`
    
- `"exp": 1719830400`

---

## 3️⃣ Custom Data

Optional application-specific data

```json
{
  "lang": "fa",
  "theme": "dark",
  "teamId": 5
}
```

---

# 🧩 JWT Structure

A JWT consists of **three parts**:

```
HEADER.PAYLOAD.SIGNATURE
```

![[jwt-structure.png]]

---

## 1️⃣ Header

Contains:

- Token type
    
- Signing algorithm

Example:

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

---

## 2️⃣ Payload

Contains:

- User information
    
- Claims
    
- Custom data    

---

## 3️⃣ Signature

Prevents tampering.

```
Signature = hash( header + payload + secretKey )
```

If someone modifies the payload, the signature becomes invalid.

---

# 🔄 Token Authentication Flow

![[token-auth.png]]
---

# 🚀 Benefits of JWT

---

## ✅ No Session Management

- No server-side session storage
    
- Stateless architecture
    
- Scales easily


---

## 🌍 Portable

- Works across multiple services
    
- Ideal for microservices


---

## 📱 Mobile-Friendly

- No cookies required
    
- Can be stored in:
    
    - `localStorage`
        
    - `sessionStorage`


---

## ⚡ High Performance

- Only signature verification required
    
- No database call per request
    
- Lightweight and fast