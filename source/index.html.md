---
title: Moovby API

language_tabs:
  - cURL

includes:
  - errors

search: true
---

# Introduction

Welcome to the Moovby API. This API documentation is created to ease and breeze the communication and process of development team.

This API documentation should be used internally within Moovby development team only. So it is restricted to expose this API documentation to public.

The API can be access via:

`https://api.moovby.com/v1`

`Authorization: Bearer YOUR_API_TOKEN`

# Users

## Register

```shell
curl
  -H "Content-Type: application/json"
  -X POST
  -d '{"email", "user@moovby.com", "password": "12345678", "device_identifier": "uuid1234", "device_information": "example of user agent", "device_type", "ios|android|web"}'
  ENDPOINT
```

> The above command returns JSON structured like this:

```json
{
  "status": "verified",
  "message": "You have successfully registered.",
  "user": {
    "id": 1,
    "name": "John Doe",
    "email": "user@moovby.com",
    "state": "active"
  }
}
```

This endpoint to sign up new user.

### HTTP Request

`POST /signup`

### Query Parameters

Parameter | Description
--------- | ------- | -----------
email | User email.
password | User password. Minimum length is 8 characters.
device_identifier | UUID from the device user used to register.
device_information | Device agent info (OS info / hardware info)
device_type | Device type (Android, iOS, web)

## Login

```shell
curl
  -H "Content-Type: application/json"
  -X POST
  -d '{"email", "user@moovby.com", "password": "12345678"'
  ENDPOINT
```

> The above command returns JSON structured like this:

```json
{
  "id": 1,
  "name": "John Doe",
  "email": "user@moovby.com",
  "token": "c333345d4b6918c36a3df11782b7bfbf",
  "state": "active"
}
```

This endpoint to sign in existing user.

### HTTP Request

`POST /signin`

### Query Parameters

Parameter | Description
--------- | ------- | -----------
email | User email.
password | User password. Minimum length is 8 characters.

## Logout

```shell
curl
  -H "Authorization: Bearer <token>"
  -H "Content-Type: application/json"
  ENDPOINT
```

> The above command returns JSON structured like this:

```json
{
  "status": "200|401",
  "message": "You have been signed out"
}
```

This endpoint to sign out user.

### HTTP Request

`DELETE /account`
