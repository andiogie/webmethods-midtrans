# 💳 webMethods × Midtrans Integration

description: >
  This project showcases how to integrate Midtrans, an Indonesian payment gateway,
  with Software AG webMethods Integration Server. It includes sending payment
  transactions via /charge and checking their status via /status using REST and
  Base64-based authorization.

---

## ✨ Key Features

- Integration with Midtrans **Sandbox** environment
- Send payments using `POST /v2/charge`
- Check status using `GET /v2/{order_id}/status`
- Basic Auth header using Base64(Server Key + ":")
- Use `pub.client:http` to interact with external APIs
- Parse JSON response to webMethods Document
- Testable via Postman or REST endpoint

---

## 📦 Requirements

- Software AG **webMethods Integration Server** (10.x+)
- Midtrans **Sandbox Account** (register: https://dashboard.midtrans.com/register)
- **Server Key** from Midtrans Dashboard (Sandbox tab)
- Access to webMethods Designer / Developer

---

## 🛠️ Setup Guide

### 🔐 Authentication
- Authentication: Type: Basic Auth
- format: Base64(ServerKey + ":")
- charge-flow:
  - endpoint: POST /v2/charge
  - url: https://api.sandbox.midtrans.com/v2/charge
- headers:
  - Content-Type: application/json
  - Authorization: Basic {base64-encoded-server-key}
- Sample Payload (webMethods Version)
```yaml  
{
    "paymentType": "qris",
    "grossAmount": 300000,
    "firstName": "Andi",
    "lastName": "Ogie",
    "email": "test123@gmail.com",
    "phone": "081122334455",
    "item_details": [
        {
            "id": "ID-A01",
            "price": 100000,
            "quantity": 1,
            "name": "Boneka Stich"
        },
        {
            "id": "ID-A02",
            "price": 100000,
            "quantity": 1,
            "name": "Boneka Labubu"
        },
        {
            "id": "ID-A03",
            "price": 100000,
            "quantity": 1,
            "name": "Boneka Spongebob"
        }
    ],
    "serverKey":"Mid-server-T2-H9VUgOL2gp2x_NMc-U5qS"
}
```

- status-flow:
  - endpoint: GET /v2/{order_id}/status
  - url: https://api.sandbox.midtrans.com/v2/{order_id}/status
- Headers:
  - Authorization: Basic {base64-encoded-server-key}
  - Accept: application/json
  

## 🗂 Folder Structure

package: integration.thirdparty.midtrans

services:
  - chargePayment: Call Midtrans /charge endpoint
  - checkStatus: Call Midtrans /status endpoint
  - buildAuthHeader: Build Base64 Authorization
  - generateOrderId: Custom order_id formatter
  - parsePayloadAmounts: Convert strings to integers

---

## 🧪 Postman Testing

```yaml
test_charge:
  method: POST
  url: https://api.sandbox.midtrans.com/v2/charge
  headers:
    - Authorization: Basic {base64-encoded-server-key}
    - Content-Type: application/json

test_status:
  method: GET
  url: https://api.sandbox.midtrans.com/v2/{order_id}/status
  headers:
    - Authorization: Basic {base64-encoded-server-key}
    - Accept: application/json
```

## 🙋‍♂️ Author

name: Andi Ogie  
role: Integration Engineer  
linkedin: https://linkedin.com/in/andiogie  
notes: >
  Focused on simplifying enterprise integration, API orchestration, and 
  real-time data workflows using webMethods, REST, and modern Java services.

