# Payment Module API Collection

This collection contains comprehensive API endpoints for the EducateU Payment Management System.

## 📋 Module Overview

The Payment Module handles all payment-related operations including:
- **Promotional Codes**: Discount code management and application
- **Applicant Payments**: Student payment tracking and installments
- **Course Fees**: Course pricing with tiered structures
- **Agent Commissions**: Agent referral commission management
- **Commission Payments**: Agent payment processing

## 🗂 Collection Structure

### 1. Promotional Codes
- `GET` Promotional Codes - List with filtering
- `POST` Create Promotional Code - New discount codes
- `PUT` Update Promotional Code - Modify existing codes
- `GET` Get by ID - Retrieve specific code
- `DELETE` Delete Promotional Code - Soft delete (set inactive)

### 2. Applicant Payments
- `GET` Applicant Payments - Payment records with filtering
- `POST` Create Payment Record - New payment setup
- `PUT` Update Payment Status - Status and amount updates
- `POST` Add Payment History - Record payment transactions
- `GET` Payment Overview - Dashboard statistics

### 3. Course Fees
- `GET` Course Fees - List all course fees
- `POST` Create Course Fee - Basic fee structure
- `POST` Create Degree Structure - Semester/module breakdown
- `GET` By Course & Session - Load existing structure
- `GET` Advance Degree Fees - Degree-specific fees
- `GET` Advance Diploma Fees - Diploma-specific fees

### 4. Agent Overview
- `GET` Agent Overview - Statistics dashboard
- `GET` Agent Overview Data - Detailed commission data

### 5. Agent Commissions
- `GET` Agent Commissions - Commission records
- `POST` Create Commission - New commission setup
- `PUT` Update Commission - Status and clawback management

### 6. Commission Payments
- `GET` Commission Payments - Payment transaction history
- `POST` Create Payment - Record commission payments

### 7. Overview Endpoints
- `GET` Advance Degree Overview - Degree payment statistics
- `GET` Advance Diploma Overview - Diploma payment statistics

## 🔧 Environment Variables

The collection uses these environment variables (defined in LOCAL.bru):

```
baseUrl: http://localhost:3333
userId: 39ac3e0e-07bb-42f4-ab61-e53c6c27e1d7
portalCategoryId: 8afa700e-216b-454f-a88d-6f3e44b06a9c
roleId: 11111111-1111-1111-1111-111111111111
applicationId: 22222222-2222-2222-2222-222222222222
courseId: 33333333-3333-3333-3333-333333333333
sessionId: 44444444-4444-4444-4444-444444444444
agentId: 55555555-5555-5555-5555-555555555555
promoCodeId: 66666666-6666-6666-6666-666666666666
paymentRecordId: 77777777-7777-7777-7777-777777777777
commissionId: 88888888-8888-8888-8888-888888888888
```

## 🔐 Authentication

All endpoints require these headers:
```
user-id: {{userId}}
portal-category-id: {{portalCategoryId}}
role-id: {{roleId}}
```

## 📊 Response Format

All endpoints return standardized responses:
```json
{
  "status": "success",
  "statusCode": 200,
  "message": "Request was successful",
  "data": { /* response data */ },
  "pagination": { /* pagination info when applicable */ }
}
```

## 🧪 Testing Guide

### 1. Setup Environment
1. Ensure local server is running on port 3333
2. Update environment variables with actual UUIDs from your database
3. Verify authentication headers are properly set

### 2. Test Sequence
1. **Promotional Codes**: Create → List → Update → Get by ID
2. **Course Fees**: Create course fee → Create degree structure
3. **Payment Records**: Create → Add payment history → Update status
4. **Agent Commissions**: Create → Update status → Create payment

### 3. Common Test Scenarios

#### Promotional Code Workflow
```
1. POST /promotional-codes (Create "SUMMER25" with 25% discount)
2. GET /promotional-codes (Verify it appears in list)
3. PUT /promotional-codes/{id} (Update discount to 30%)
4. DELETE /promotional-codes/{id} (Soft delete)
```

#### Payment Processing Workflow
```
1. POST /applicant-payments (Create payment record for application)
2. POST /payment-history (Add first payment transaction)
3. PUT /applicant-payments/{id} (Update status after payment)
4. GET /applicant-payments (Verify updated amounts)
```

#### Course Fee Management
```
1. POST /course-fees (Create basic fee structure)
2. POST /course-fees/degree-structure (Add semester breakdown)
3. GET /course-fees/by-course-session (Load for editing)
4. GET /course-fees/advance-degree (View in degree dashboard)
```

## 🚨 Error Handling

Common error responses:
- `400` - Validation errors (invalid data format)
- `401` - Authentication errors (missing/invalid headers)
- `404` - Resource not found
- `409` - Duplicate data (e.g., promotional code name exists)

## 📈 Performance Notes

- Use pagination for large datasets (`page` and `limit` parameters)
- Filter results using query parameters to reduce response size
- Overview endpoints are optimized for dashboard loading
- Payment history endpoints support date range filtering

## 🔄 Workflow Integration

The Payment Module integrates with:
- **Application Module**: Links payments to applications
- **Course Module**: Associates fees with courses and sessions
- **User Module**: Manages agent and student relationships
- **Session Module**: Handles academic session-based pricing

## 💡 Tips for Frontend Integration

1. **Reuse Components**: Agent commission and applicant payment endpoints return the same data format for UI consistency
2. **Real-time Updates**: Use the update endpoints to refresh payment statuses
3. **Batch Operations**: Consider implementing bulk payment processing for efficiency
4. **Error Handling**: Implement proper error handling for payment failures
5. **Validation**: Use the same validation rules as the backend (defined in validation.ts)