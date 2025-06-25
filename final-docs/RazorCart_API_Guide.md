# RazorCart - API Guide

# RazorCart API Documentation

## Overview

RazorCart is a lightweight payment API that allows developers to integrate seamless checkout, order creation, and payment processing into their applications.

This guide walks you through:

- How to get started with RazorCart
- Authentication setup (using JWT tokens)
- Creating orders
- Capturing payments
- Handling errors

## API Endpoints

### Create Order

**Endpoint:**

`POST /api/v1/orders`

**Request Headers:**
Authorization: Bearer <your_jwt_token>
Content-Type: application/json

**Request Body:**

```json
{
  "amount": 5000,
  "currency": "INR",
  "receipt": "rcptid_11"
}
Response:
{
  "id": "order_ABC123",
  "status": "created",
  "amount": 5000,
  "currency": "INR"
}
```

## Authentication

To get started:

1. Register your developer account.
2. Get your API key and secret.
3. Generate a JWT token using your credentials.

Sample JWT payload:

```json
{
  "user_id": "dev_123",
  "exp": 1719216000
}
Use this token in the Authorization header:
Authorization: Bearer <your_jwt_token>

---

## ❌ STEP 5: Common Error Codes

```markdown
## ❌ Error Codes

| Code | Message | Description |
|------|---------|-------------|
| 400  | Bad Request | Missing or invalid data |
| 401  | Unauthorized | JWT token missing or invalid |
| 404  | Not Found | The requested endpoint doesn't exist |
| 500  | Server Error | Something went wrong on our end |
```

## Sample Use Case

### Scenario: A user clicks "Pay Now" on your app.

Your frontend will:

- Call `POST /api/v1/orders` to create an order
- Receive the order ID
- Use RazorCart's frontend SDK to collect payment
- Once payment is done, call `/api/v1/capture-payment` to finalize it