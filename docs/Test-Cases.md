# Current Users Test Inventory

| ID | Test Case | Result |
|---|---|---|
| TC-USER-001 | Current authenticated user | Partial Pass |
| TC-USER-002 | Get user by ID | Partial Pass |
| TC-USER-003 | Get all users | Partial Pass |
| TC-USER-004 | Search users | Partial Pass |
| TC-USER-005 | Pagination limit 5 | Partial Pass |
| TC-USER-006 | Pagination limit 1 | Partial Pass |
| TC-USER-007 | User not found | Pass |
| TC-USER-008 | Invalid user ID type | Pass |

---

# Products API Test Inventory

## Positive / Functional Testing

| ID | Test Case | Result |
|---|---|---|
| TC-PROD-001 | Get all products | Pass |
| TC-PROD-002 | Get product by ID | Pass |
| TC-PROD-003 | Search products | Pass |
| TC-PROD-004 | Get product categories | Pass |
| TC-PROD-005 | Get products by category | Pass |
| TC-PROD-006 | Products pagination limit 5 | Pass |
| TC-PROD-007 | Products pagination limit 1 | Pass |

## Negative Testing

| ID | Test Case | Result |
|---|---|---|
| TC-PROD-008 | Product not found | Pass |
| TC-PROD-009 | Invalid product ID type | Pass |

## CRUD Testing

| ID | Test Case | Result |
|---|---|---|
| TC-PROD-010 | Create product | Partial Pass |
| TC-PROD-011 | Update product using PUT | Pass |
| TC-PROD-012 | Update product using PATCH | Partial Pass |
| TC-PROD-013 | Delete product | Partial Pass |

---

# Products API Coverage Summary

The Products API module covers:

- Functional API testing
- Positive testing
- Negative testing
- Boundary testing
- Query parameter validation
- Category filtering
- Search validation
- Pagination validation
- CRUD testing
- Request chaining
- Environment variable usage
- Response schema validation
- Data integrity assertions
- Performance assertions

---

# Request Chaining Coverage

The Products module demonstrates dynamic request chaining.

## Product ID Chaining

```text
Get Product / Products
        ↓
Extract product ID
        ↓
productId
        ↓
Get / PUT / PATCH / DELETE Product

GET /products/categories
        ↓
Extract first category slug
        ↓
categorySlug
        ↓
GET /products/category/{{categorySlug}}

POST /products/add
        ↓
createdProductId

| Operation      | Endpoint                | Result       |
| -------------- | ----------------------- | ------------ |
| Create         | `POST /products/add`    | Partial Pass |
| Read           | `GET /products/{id}`    | Pass         |
| Update         | `PUT /products/{id}`    | Pass         |
| Partial Update | `PATCH /products/{id}`  | Partial Pass |
| Delete         | `DELETE /products/{id}` | Partial Pass |


| Request                    | Observation                                                         |
| -------------------------- | ------------------------------------------------------------------- |
| Create Product             | 1907 ms observed                                                    |
| Update Product using PUT   | 2430 ms observed on one execution; later execution passed at 568 ms |
| Update Product using PATCH | 1969 ms observed                                                    |
| Delete Product             | 1868 ms observed                                                    |


Key QA Findings
Finding 1 — Sensitive Data Exposure

The Users API responses were observed to contain sensitive fields such as:

password
ssn
crypto

These fields were validated as findings and documented separately in Defect-Report.md.

Finding 2 — Variable Response Latency

Several Products API requests exceeded the defined response-time threshold during individual executions.

These observations are recorded as performance findings and are not automatically classified as functional defects.

Finding 3 — Simulated CRUD Persistence

The API returns a generated ID for POST /products/add, but that simulated resource is not guaranteed to persist for subsequent operations.

Therefore:

POST /products/add
        ↓
createdProductId
        ↓
PUT /products/{{createdProductId}}

may return 404 Not Found.

The CRUD tests consequently distinguish between API response-contract validation and actual persistent backend behavior.
