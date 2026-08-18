# Defect Report

## Project Information

| Field | Details |
|---|---|
| Project | E-Commerce REST API Testing |
| API Under Test | DummyJSON |
| Testing Tool | Postman |
| Test Type | Manual REST API Testing |
| Environment | E-Commerce Test Environment |
| Defect Type | Security / Performance |
| Status | Open / Observation |

---

# DEF-001 — Sensitive User Information Exposed in API Response

| Field | Details |
|---|---|
| Defect ID | DEF-001 |
| Title | User APIs expose sensitive information in response payload |
| Severity | High |
| Priority | High |
| Category | Security / Data Exposure |
| Affected Module | Users |
| Status | Open |
| Reporter | Romeyraj Bundela |

## Affected Endpoints

The issue was observed across multiple user-related endpoints:

- `GET /auth/me`
- `GET /users/{id}`
- `GET /users`
- `GET /users/search`
- `GET /users?limit=5&skip=0`
- `GET /users?limit=1&skip=0`

## Preconditions

1. Valid authentication credentials are available.
2. User is authenticated successfully.
3. A valid Bearer access token is available.

## Steps to Reproduce

1. Authenticate using the valid login request.
2. Store the returned access token.
3. Send an authenticated request to one of the affected user endpoints.
4. Inspect the JSON response body.
5. Review the fields returned for the user object.

## Expected Result

The API should return only the user information required by the client.

Sensitive authentication or personally sensitive information should not be unnecessarily exposed in the response payload.

Examples of fields that should not be returned include:

- `password`
- `ssn`
- sensitive financial/wallet information such as `crypto`

## Actual Result

The API response included sensitive fields such as:

```text
password
ssn
crypto