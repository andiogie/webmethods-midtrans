# 💳 webMethods × Midtrans Integration

This project showcases how to integrate **Midtrans**, an Indonesian payment gateway, with **Software AG webMethods Integration Server**. It focuses on checking transaction status via Midtrans Core API using **REST** and **Base64-based Authorization**.

---

## ✨ Key Features

- ✅ Integration with **Midtrans Sandbox** environment  
- ✅ Call Midtrans `GET /v2/{order_id}/status` from webMethods  
- ✅ Create Basic Auth header (**Base64 of Server Key**)  
- ✅ Use `pub.client:http` to call external APIs  
- ✅ Parse JSON response into Document format  
- ✅ Test via **Postman** or **webMethods REST endpoint**

---

## 📦 Requirements

- Software AG **webMethods Integration Server (IS) 10.x or above**  
- **Midtrans Sandbox Account** ([Register here](https://dashboard.midtrans.com/register))  
- **Server Key** from your Midtrans account (Sandbox only)  
- Access to **webMethods Designer** / Developer to create Flow Services  

---

## 🛠️ Setup Guide

1. **Register a Midtrans account** and set environment to **Sandbox**
2. **Copy your Server Key** from Midtrans Dashboard → Sandbox tab
3. **Create a Flow Service** in webMethods with the following:
   - One input field: `order_id`
   - Use `pub.client:http` to call:  
     `https://api.sandbox.midtrans.com/v2/{order_id}/status`
   - Build Authorization header using:  
     `Basic Base64(ServerKey + ":")`
   - Parse JSON response using:  
     `pub.json:jsonStringToDocument`
4. **Test via Postman** or from your REST-enabled Flow Service

🧪 **Example REST endpoint (RESTv2)**:  
localhost:5555/restv2/integration.thirdparty.midtrans.ws:midtransws/midtransws/{order-id}

## 📬 Testing via Postman

- **Method:** `GET`  
- **URL:** `https://api.sandbox.midtrans.com/v2/{order_id}/status`  
- **Headers:**
  - `Authorization`: `Basic {base64-encoded-server-key}`
  - `Accept`: `application/json`
