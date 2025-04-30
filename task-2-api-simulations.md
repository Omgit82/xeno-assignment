# Xeno Assignment – Task 2: API Request & Response Simulation

This document covers request and response simulations for 3 selected APIs.

## API 1: Generate Registration OTP
- Method: POST  
- Endpoint: `/api/customer/generate-otp`  
- Headers:
```plaintext

{
  "Content-Type": "application/json",
  "Authorization": "Bearer <token>"
}
 #request
{
  "mobile": "9876543210",
  "country_code": "+91"
}
#success response
{
  "status": "success",
  "message": "OTP sent successfully",
  "otp_id": "otp_67891234"
}
#error response
{
  "status": "error",
  "errorCode": "MOBILE_INVALID",
  "message": "Invalid mobile number format"
}
json

##  API 2: Add/Update Customer
Method: POST
Endpoint: /api/customer/add-update
Headers:

{
  "Content-Type": "application/json",
  "Authorization": "Bearer <token>"
}
#request
{
  "mobile": "9876543210",
  "email": "goel@example.com",
  "name": "Goel Kumar",
  "city": "Delhi",
  "dob": "2000-01-15"
}
#success response
{
  "status": "success",
  "message": "Customer added/updated successfully",
  "customer_id": "cust_123456"
}
#error resonse
{
  "status": "error",
  "errorCode": "DUPLICATE_EMAIL",
  "message": "This email is already associated with another customer"
}


## API 3: Add Orders (V2)
Method: POST
Endpoint: /api/orders/add
Headers:
Content-Type: application/json  
Authorization: Bearer <token>

#request
{
  "order_id": "ORD123456",
  "customer_id": "cust_123456",
  "amount": 2199,
  "items": [
    { "sku": "TSHIRT001", "quantity": 2, "price": 1099 }
  ],
  "order_date": "2025-04-30T10:30:00Z"
}

#success response
{
  "status": "success",
  "message": "Order created successfully",
  "order_id": "ORD123456"
}
 #error response
{
  "status": "error",
  "errorCode": "INVALID_CUSTOMER",
  "message": "Customer ID not found"
}


### Error Schema Design (for Add Orders API)
{
  "status": "error",
  "errorCode": "INVALID_CUSTOMER",
  "message": "Customer ID not found",
  "path": "/api/orders/add",
  "timestamp": "2025-04-30T13:20:00Z",
  "request_id": "req_abcd1234"
}


status: Always "error" for failed responses

errorCode: Developer-readable code

message: End-user friendly error message

path: API endpoint that caused the error

timestamp: Time of the error in ISO format

request_id: Unique ID to trace the request in logs
