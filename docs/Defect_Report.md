# Defect Report

## Project

**E-Commerce REST API Testing Project**

**API:** DummyJSON

**Testing Tool:** Postman

**Testing Type:** Manual REST API Testing

**Performance Threshold:** < 1500 ms

---

# Defect / Finding Summary

| ID | Area | Finding | Severity | Status |
|---|---|---|---|---|
| DEF-001 | Users API | Sensitive user information exposed in API responses | High | Observed |
| PERF-001 | Products API | Create Product response exceeded performance threshold | Medium | Observed |
| PERF-002 | Products API | PUT Product response exceeded performance threshold during one execution | Medium | Observed |
| PERF-003 | Products API | PATCH Product response exceeded performance threshold | Medium | Observed |
| PERF-004 | Products API | DELETE Product response exceeded performance threshold | Medium | Observed |

---

# DEF-001 — Sensitive User Information Exposed

## Title

Sensitive user information is exposed in Users API responses.

## Severity

**High**

## Priority

**High**

## Module

Users API

## Affected Endpoints

The issue was observed across multiple authenticated Users API responses, including:

```text
GET /auth/me
GET /users/{id}
GET /users
GET /users/search
GET /users?limit=5&skip=0
GET /users?limit=1&skip=0