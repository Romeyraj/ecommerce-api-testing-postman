# API Test Cases

## Project

**Project:** E-Commerce REST API Testing  
**Tool:** Postman  
**API Under Test:** DummyJSON  
**Test Type:** Manual REST API Testing

---

## Test Case Summary

| Module | Test Cases |
|---|---:|
| Authentication | 4 |
| Users | 8 |
| **Total** | **12** |

---

# Authentication Test Cases

## TC-AUTH-001 — Login With Valid Credentials

| Field | Details |
|---|---|
| Test Case ID | TC-AUTH-001 |
| Module | Authentication |
| Test Scenario | Verify login with valid credentials |
| Method | POST |
| Endpoint | `/auth/login` |
| Test Data | Valid username and password |
| Expected Status | 200 OK |
| Expected Result | Authentication succeeds and access/refresh tokens are returned |
| Actual Result | Authentication succeeded and tokens were returned |
| Result | PASS |
| Additional Observation | Response-time assertion failed during execution because response time exceeded 1500 ms |

### Validations

- Status code is 200
- Response is JSON
- Access token is present
- Refresh token is present
- User ID is present
- Username is correct
- Response-time threshold is validated

---

## TC-AUTH-002 — Login With Invalid Credentials

| Field | Details |
|---|---|
| Test Case ID | TC-AUTH-002 |
| Module | Authentication |
| Test Scenario | Verify login rejection with incorrect password |
| Method | POST |
| Endpoint | `/auth/login` |
| Test Data | Valid username + invalid password |
| Expected Status | 400 Bad Request |
| Expected Result | Authentication is rejected with an appropriate error message |
| Actual Result | `Invalid credentials` returned |
| Result | PASS |

### Validations

- Status code is 400
- Response is JSON
- Correct error message returned
- Access token is not returned
- Refresh token is not returned
- Response time is within threshold

---

## TC-AUTH-003 — Login With Empty Credentials

| Field | Details |
|---|---|
| Test Case ID | TC-AUTH-003 |
| Module | Authentication |
| Test Scenario | Verify validation when username and password are empty |
| Method | POST |
| Endpoint | `/auth/login` |
| Test Data | Empty username and password |
| Expected Status | 400 Bad Request |
| Expected Result | API rejects empty credentials |
| Actual Result | `Username and password required` returned |
| Result | PASS |

### Validations

- Status code is 400
- Response is JSON
- Correct validation message returned
- Access token is not returned
- Refresh token is not returned
- Response time is validated

---

## TC-AUTH-004 — Login With Missing Credential Fields

| Field | Details |
|---|---|
| Test Case ID | TC-AUTH-004 |
| Module | Authentication |
| Test Scenario | Verify validation when username and password fields are omitted |
| Method | POST |
| Endpoint | `/auth/login` |
| Test Data | `{}` |
| Expected Status | 400 Bad Request |
| Expected Result | API rejects request and reports missing credentials |
| Actual Result | `Username and password required` returned |
| Result | PASS |
| Additional Observation | Response-time assertion failed during one execution because response exceeded 1500 ms |

### Validations

- Status code is 400
- Response is JSON
- Correct validation message returned
- Access token is not returned
- Refresh token is not returned
- Response-time threshold is validated

---

# Users Test Cases

## TC-USER-001 — Get Current Authenticated User

| Field | Details |
|---|---|
| Test Case ID | TC-USER-001 |
| Module | Users |
| Test Scenario | Retrieve profile of currently authenticated user |
| Method | GET |
| Endpoint | `/auth/me` |
| Authentication | Bearer Token |
| Expected Status | 200 OK |
| Expected Result | Authenticated user's profile is returned |
| Actual Result | User ID `1` and username `emilys` returned |
| Result | PARTIAL PASS |
| Security Observation | Password field was present in response |
| Performance Observation | Response exceeded 1500 ms threshold |

### Validations

- Status code is 200
- Response is JSON
- Authenticated user ID is correct
- Username is correct
- First name is present
- Last name is present
- Email is present
- Password must not be exposed
- Response time must be below 1500 ms

---

## TC-USER-002 — Get User By ID

| Field | Details |
|---|---|
| Test Case ID | TC-USER-002 |
| Module | Users |
| Test Scenario | Retrieve user using a valid user ID |
| Method | GET |
| Endpoint | `/users/{{userId}}` |
| Authentication | Bearer Token |
| Expected Status | 200 OK |
| Expected Result | Requested user's profile is returned |
| Actual Result | User ID `1` / username `emilys` returned |
| Result | PARTIAL PASS |
| Security Observation | Password field was present in response |
| Performance Observation | Response-time threshold exceeded during execution |

### Validations

- Status code is 200
- Response is JSON
- Returned user ID matches requested ID
- Username is correct
- First name is present
- Last name is present
- Email is present
- Password must not be exposed
- Response time must be below 1500 ms

---

## TC-USER-003 — Get All Users

| Field | Details |
|---|---|
| Test Case ID | TC-USER-003 |
| Module | Users |
| Test Scenario | Retrieve collection of users |
| Method | GET |
| Endpoint | `/users` |
| Authentication | Bearer Token |
| Expected Status | 200 OK |
| Expected Result | Users collection and pagination metadata are returned |
| Actual Result | Users array and metadata returned successfully |
| Result | PARTIAL PASS |
| Security Observation | Password, SSN and crypto fields were present |
| Performance Result | Passed during execution |

### Validations

- Status code is 200
- Response is JSON
- Users array exists
- At least one user exists
- Total count exists
- Skip exists
- Limit exists
- Every user has an ID
- Every user has a username
- Every user has first name
- Every user has last name
- Every user has email
- Password must not be exposed
- SSN must not be exposed
- Crypto wallet data must not be exposed
- Response time must be below 1500 ms

---

## TC-USER-004 — Search Users

| Field | Details |
|---|---|
| Test Case ID | TC-USER-004 |
| Module | Users |
| Test Scenario | Search users using a query parameter |
| Method | GET |
| Endpoint | `/users/search?q=Emily` |
| Authentication | Bearer Token |
| Expected Status | 200 OK |
| Expected Result | Relevant matching users are returned |
| Actual Result | Emily / `emilys` returned |
| Result | PARTIAL PASS |
| Security Observation | Password, SSN and crypto fields were present |
| Performance Result | Passed during execution |

### Validations

- Status code is 200
- Response is JSON
- Users array exists
- At least one result exists
- Expected user is returned
- Returned users match the search term
- Every returned user has an ID
- Password must not be exposed
- SSN must not be exposed
- Crypto wallet data must not be exposed
- Response time must be below 1500 ms

---

## TC-USER-005 — Users Pagination With Limit 5

| Field | Details |
|---|---|
| Test Case ID | TC-USER-005 |
| Module | Users |
| Test Scenario | Verify pagination using limit and skip parameters |
| Method | GET |
| Endpoint | `/users?limit=5&skip=0` |
| Authentication | Bearer Token |
| Expected Status | 200 OK |
| Expected Result | Maximum 5 users returned with correct pagination metadata |
| Actual Result | Pagination parameters were handled correctly |
| Result | PARTIAL PASS |
| Security Observation | Password, SSN and crypto fields were present |

### Validations

- Status code is 200
- Response is JSON
- Users array exists
- Returned users do not exceed requested limit
- Returned limit matches requested limit
- Returned skip matches requested skip
- Total count exists
- Every user has an ID
- Password must not be exposed
- SSN must not be exposed
- Crypto wallet data must not be exposed
- Response time must be below 1500 ms

---

## TC-USER-006 — Users Pagination Boundary With Limit 1

| Field | Details |
|---|---|
| Test Case ID | TC-USER-006 |
| Module | Users |
| Test Scenario | Verify minimum pagination limit |
| Method | GET |
| Endpoint | `/users?limit=1&skip=0` |
| Authentication | Bearer Token |
| Expected Status | 200 OK |
| Expected Result | Maximum 1 user returned and metadata reflects request |
| Actual Result | Pagination metadata and result size behaved correctly |
| Result | PARTIAL PASS |
| Security Observation | Password, SSN and crypto fields were present |
| Performance Observation | Response exceeded 1500 ms during execution |

### Validations

- Status code is 200
- Response is JSON
- Returned users do not exceed requested limit
- Returned limit matches requested limit
- Returned skip matches requested skip
- Total count exists
- Every returned user has an ID
- Password must not be exposed
- SSN must not be exposed
- Crypto wallet data must not be exposed
- Response time must be below 1500 ms

---

## TC-USER-007 — Get User Not Found

| Field | Details |
|---|---|
| Test Case ID | TC-USER-007 |
| Module | Users |
| Test Scenario | Verify behavior when requested user does not exist |
| Method | GET |
| Endpoint | `/users/999999` |
| Authentication | Bearer Token |
| Expected Status | 404 Not Found |
| Expected Result | Appropriate not-found error returned |
| Actual Result | `User with id '999999' not found` |
| Result | PASS |

### Validations

- Status code is 404
- Response is JSON
- Error message is present
- Correct error message is returned
- User data is not returned
- Sensitive data is not returned
- Response time is below threshold

---

## TC-USER-008 — Get User With Invalid ID Type

| Field | Details |
|---|---|
| Test Case ID | TC-USER-008 |
| Module | Users |
| Test Scenario | Verify API behavior when user ID has an invalid data type |
| Method | GET |
| Endpoint | `/users/abc` |
| Authentication | Bearer Token |
| Expected Status | 400 Bad Request |
| Expected Result | API rejects invalid ID format |
| Actual Result | `Invalid user id 'abc'` |
| Result | PASS |

### Validations

- Status code is 400
- Response is JSON
- Error message is present
- Correct invalid-ID message is returned
- User data is not returned
- Sensitive data is not returned
- Response time is below threshold

---

# Test Execution Notes

## Positive Coverage

- Successful authentication
- Authenticated user retrieval
- User retrieval by ID
- User collection retrieval
- User search
- Pagination

## Negative Coverage

- Invalid credentials
- Empty credentials
- Missing credentials
- Non-existent user
- Invalid user ID type

## Security/Data Exposure Coverage

The following fields were explicitly checked across user-related endpoints:

- `password`
- `ssn`
- `crypto`

These fields were observed in responses and are documented as findings for further defect analysis.

## Performance Coverage

A response-time threshold of:

**< 1500 ms**

was used during testing.

Some API requests exceeded the threshold during execution. These observations will be documented separately and should not be confused with functional API failures.

---

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

## Test Status

**Users API module:** Initial functional test coverage completed.

**Next activity:** Defect documentation and Git milestone update.