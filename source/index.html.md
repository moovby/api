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

# Authentication

## Register via Email

```shell
curl
  -H "Content-Type: application/json"
  -X POST
  -d '{"email", "user@moovby.com", "password": "12345678"}'
  ENDPOINT
```

> The above command returns JSON structured like this:

```json
{
  "status": "true",
  "message": "You have successfully registered.",
  "data": {
    "auth_token": "c333345d4b6918c36a3df11782b7bfbf"
  }
}
```

This endpoint to sign up new user via email.

### HTTP Request

`POST /signup`

### Query Parameters

Parameter | Description
--------- | ------- | -----------
email | User email.
password | User password. Minimum length is 8 characters.

## Register via Social Media

```shell
curl
  -H "Content-Type: application/json"
  -X POST
  ENDPOINT
```

> The above command returns JSON structured like this:

```json
{
  "status": "true",
  "message": "You have successfully registered.",
  "data": {
    "auth_token": "c333345d4b6918c36a3df11782b7bfbf"
  }
}
```

This endpoint to sign up new user via social media i.e Facebook or Google.

### HTTP Request

`POST /signup/fb_login?token=764b26d5dd8772af73eef8110a33f5d9`

## Login via Email

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
  "status": "true",
  "message": "You have successfully registered.",
  "data": {
    "auth_token": "c333345d4b6918c36a3df11782b7bfbf"
  }
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

# Profile

## Create user profile

```shell
curl
  -H "Authorization: Bearer <token>"
  -H "Content-Type: application/json"
  -X POST
  -d '{"phone_number": "60136285901", "first_name": "Nik Muhammad Amin", "last_name": "Nik Muhammad Kamil", "role": 1, "avatar": "http://moovby.s3.amazonaws.com/avatar.jpg", "ic": "http://moovby.s3.amazonaws.com/ic.jpg", "licence": "http://moovby.s3.amazonaws.com/licence.jpg", "device_info": { "device_identifier": "uuid1234", "device_information": "example of user agent", "device_type": "ios|android|web"}}'
  ENDPOINT
```

> The above command returns JSON structured like this:

```json
{
  "status": "true",
  "message": "You have successfully registered.",
  "user": {}
}
```

This endpoint to sign up new user via email.

### HTTP Request

`POST /user`

### Query Parameters

Parameter | Description
--------- | ------- | -----------
phone_number | User phone number, includes country code.
first_name | User first name.
last_name | User last name.
avatar | User avatar URL.
role | Indicate user role. 1 (renter), 2 (owner). 3 (both renter and owner).
ic | User ic picture URL. This is compulsory for both.
licence | User licence picture URL. This is only for renter but not for owner.
device_identifier | UUID from the device user used to register.
device_information | Device agent info (OS info / hardware info)
device_type | Device type (Android, iOS, web)


## Update user profile

# Vehicle

## Get all vehicles

## Get a vehicle

## Filter a vehicles

## List of owner vehicles

# Booking

## Current booking

## Booking history

## Request a vehicle

## Confirm a vehicle

# Promotion

## Validate a promo code
