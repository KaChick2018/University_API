# University API

- [1. Overview](#1-overview)
- [2. Authentication](#2-authentication)
- [3. Endpoints](#3-endpoints)
  - [3.1. Compare Face](#31-compare-face)

## 1. Overview

KaChick's University API is a JSON based REST API. All requests are made to endpoints beginning: `https://cityu.kachick.com/api`.

Endpoint beginning might change later so its better to put it in a configuration file.

All validation error responses are in this format:
```
{
  "field_name": [
    "This field is required"
  ]
}
```

Example:
```
{
  "student_id": [
    "This field is required"
  ],
  "image": [
    "This field is required"
  ]
}
```

## 2. Authentication

You will need a token given by KaChick and include it as HTTP Authorization header.

Should be in this format:
```
Authorization: Bearer <token>
```

Example:
```
Authorization: Bearer 181d415f34379af07b2c11d144dfbe35d
```

## 3. Endpoints

### 3.1. Compare Face

Accept a file and compare it with the student's existing photo.
```
POST /students/compare-face
```

Example request:
```
POST /api/students/compare-face HTTP/1.1
Host: cityu.kachick.com
Content-Type: multipart/form-data
Accept: application/json
```

With the following fields:

| Parameter     | Type    | Required? | Description                       |
|---------------|---------|-----------|-----------------------------------|
| `student_id`  | string  | required  | Student ID                        |
| `image`       | File    | required  | Photo to compare                  |

The response is a JSON object with `success` node.

Example response:
```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

{
  "success": true
}
```

Possible errors:

| Error code                | Description       |
|---------------------------|-------------------|
| 400 Bad Request           | Validation error  |