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
  -d '{"email", "nik@moovby.com", "password": "12345678"}'
  ENDPOINT
```

> The above command returns JSON structured like this:

```json
{
    "status": "true",
    "message": "You have successfully registered.",
    "token": "c333345d4b6918c36a3df11782b7bfbf",
    "user": {
        "id": 1,
        "email": "nik@moovby.com",
        "created_at": "2016-12-17 09:54:21",
        "updated_at": "2016-12-17 09:54:22",
        "is_admin": false,
        "is_super_admin": false,
        "provider": null,
        "uid": null
    }
}
```

This endpoint to sign up new user via email.

### HTTP Request

`POST /signup`

### Data Parameters

Parameter | Description
--------- | ------- | -----------
email | User email.
password | User password. Minimum length is 8 characters.

## Register via Social Media

```shell
curl
  -H "Content-Type: application/json"
  -X POST
  -d '{"device_info": { "device_identifier": "uuid1234", "device_information": "example of user agent", "device_type": "ios|android|web"}}'
  ENDPOINT
```

> The above command returns JSON structured like this:

```json
{
    "status": "true",
    "message": "You have successfully registered.",
    "token": "c333345d4b6918c36a3df11782b7bfbf",
    "user": {
        "id": 1,
        "email": "nik@moovby.com",
        "created_at": "2016-12-17 09:54:21",
        "updated_at": "2016-12-17 09:54:22",
        "is_admin": false,
        "is_super_admin": false,
        "provider": "facebook",
        "uid": "764b26d5dd8772af73eef8110a33f5d9"
    }
}
```

This endpoint to sign up new user via social media i.e Facebook or Google.

### HTTP Request

`POST /signup/fb_login?token=764b26d5dd8772af73eef8110a33f5d9`

### Query Parameters

Parameter | Description
--------- | ------- | -----------
token | Token returned from fb / google.
device_identifier | UUID from the device user used to register.
device_information | Device agent info (OS info / hardware info)
device_type | Device type (Android, iOS, web)

## Login via Email

```shell
curl
  -H "Content-Type: application/json"
  -X POST
  -d '{"email": "nik@moovby.com", "password": "12345678", "device_info": { "device_identifier": "uuid1234", "device_information": "example of user agent", "device_type": "ios|android|web"}}'
  ENDPOINT
```

> The above command returns JSON structured like this:

```json
{
    "status": "true",
    "message": "You have successfully registered.",
    "token": "c333345d4b6918c36a3df11782b7bfbf",
    "user": {
        "id": 1,
        "email": "nik@moovby.com",
        "created_at": "2016-12-17 09:54:21",
        "updated_at": "2016-12-17 09:54:22",
        "is_admin": false,
        "is_super_admin": false,
        "provider": "",
        "uid": ""
    }
}
```

This endpoint to sign in existing user.

### HTTP Request

`POST /signin`

### Data Parameters

Parameter | Description
--------- | ------- | -----------
email | User email.
password | User password. Minimum length is 8 characters.
device_identifier | UUID from the device user used to register.
device_information | Device agent info (OS info / hardware info)
device_type | Device type (Android, iOS, web)

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
  -d '{"phone_number": "60136285901", "first_name": "Nik Muhammad Amin", "last_name": "Nik Muhammad Kamil", "role": 1, "avatar": "http://.../file.jpg", "ic": "http://.../file.jpg", "licence": "http://.../file.jpg", "latitude": 3.0748967, "longitude": 101.6438697}'
  ENDPOINT
```

> The above command returns JSON structured like this:

```json
{
    "status": "true",
    "message": "You have successfully registered.",
    "user": {
        "id": 1,
        "email": "nik@moovby.com",
        "created_at": "2016-12-21T22:06:22.899+08:00",
        "updated_at": "2016-12-23T10:45:47.953+08:00",
        "is_admin": false,
        "is_super_admin": false,
        "provider": null,
        "uid": null,
        "profile": {
            "id": 1,
            "first_name": "Nik Muhammad Amin",
            "last_name": "Nik Muhammad Kamil",
            "role": 1,
            "avatar": {
                "url": "http://.../file.jpg",
                "square": {
                    "url": "http://.../file.jpg"
                }
            },
            "latitude": 3.0748967,
            "longitude": 101.6438697,
            "created_at": "2016-12-21T22:06:22.964+08:00",
            "updated_at": "2016-12-23T10:57:59.810+08:00",
            "phone_number": "60136285901",
            "renter_verified": false,
            "ic": {
                "url": "http://.../file.jpg",
                "thumb": {
                    "url": "http://.../file.jpg"
                }
            },
            "driving_license": {
                "url": "http://.../file.jpghttp://.../file.jpg",
                "thumb": {
                    "url": "http://.../file.jpg"
                }
            }
        }
    }
}
```

This endpoint to create a new user info.

### HTTP Request

`POST /user`

### Data Parameters

Parameter | Description
--------- | ------- | -----------
phone_number | User phone number, includes country code.
first_name | User first name.
last_name | User last name.
avatar | User avatar URL.
role | Indicate user role. 1 (renter), 2 (owner). 3 (both renter and owner).
ic | User ic picture URL. This is compulsory for both.
licence | User licence picture URL. This is only for renter but not for owner.
location_latitude | User last location latitude.
location_longitude | User last location longitude.


## Update user profile

```shell
curl
  -H "Authorization: Bearer <token>"
  -H "Content-Type: application/json"
  -X POST
  -d '{"email":"nik@moovby.com","profile":{"id":1,"first_name":"Nik Muhammad Amin","last_name":"Nik Muhammad Kamil","avatar":"http://.../file.jpg","dob":"1991-02-27","gender":"Male","age":25,"occupation":"Engineer","address":"Jalan Klang Lama Taman Desa Kuala Lumpur Federal Territory of Kuala Lumpur Malaysia","latitude":3.0748967,"longitude":101.6438697,"race":"Malay","religion":"Muslim","is_married":true,"education":"Degree","phone_number":"60136285901","ic_num":"890820035573"}}'
  ENDPOINT
```

> The above command returns JSON structured like this:

```json
{
    "status": "true",
    "message": "You have successfully updated your profile.",
    "user": {
        "id": 1,
        "email": "nik@moovby.com",
        "created_at": "2016-12-21T22:06:22.899+08:00",
        "updated_at": "2016-12-23T10:45:47.953+08:00",
        "is_admin": true,
        "is_super_admin": false,
        "provider": null,
        "uid": null,
        "profile": {
            "id": 1,
            "first_name": "Nik Muhammad Amin",
            "last_name": "Nik Muhammad Kamil",
            "role": 1,
            "avatar": {
                "url": "http://.../file.jpg",
                "square": {
                    "url": "http://.../file.jpg"
                }
            },
            "dob": "1991-02-27",
            "gender": "Male",
            "age": 25,
            "occupation": "Engineer",
            "address": "Jalan Klang Lama Taman Desa Kuala Lumpur Federal Territory of Kuala Lumpur Malaysia",
            "latitude": 3.0748967,
            "longitude": 101.6438697,
            "income": null,
            "race": "Malay",
            "religion": "Muslim",
            "is_banned": null,
            "is_married": true,
            "education": "Degree",
            "rating": null,
            "rating_count": null,
            "created_at": "2016-12-21T22:06:22.964+08:00",
            "updated_at": "2016-12-23T10:57:59.810+08:00",
            "phone_number": "60136285901",
            "renter_verified": false,
            "ic": {
                "url": "http://.../file.jpg",
                "thumb": {
                    "url": "http://.../file.jpg"
                }
            },
            "driving_license": {
                "url": "http://.../file.jpghttp://.../file.jpg",
                "thumb": {
                    "url": "http://.../file.jpg"
                }
            },
            "verification_comments": null,
            "ic_num": "890820035573"
        }
    }
}
```

This endpoint to update existing user info.

### HTTP Request

`PUT /user/<id>/update`

"profile": {
        "id": 1,
        "first_name": "Nik Muhammad Amin",
        "last_name": "Nik Muhammad Kamil",
        "avatar": "http://.../file.jpg",
        "dob": "1991-02-27",
        "gender": "Male",
        "age": 25,
        "occupation": "Engineer",
        "address": "Jalan Klang Lama Taman Desa Kuala Lumpur Federal Territory of Kuala Lumpur Malaysia",
        "latitude": 3.0748967,
        "longitude": 101.6438697,
        "race": "Malay",
        "religion": "Muslim",
        "is_married": true,
        "education": "Degree",
        "phone_number": "60136285901",
        "ic_num": "890820035573"

### Data Parameters

Parameter | Description
--------- | ------- | -----------
email | User's email.
first_name | User's first name.
last_name | User's last name.
avatar | User's avatar URL.
dob | Date of Birth. i.e 1992-01-29
gender | User's gender. i.e Male / Female.
age | User's age. Should pass integer.
occupation | User's current occupation.
address | Home address of user.
location_latitude | Latitude that belong to user home address.
location_longitude | Longitude that belong to user home address.
race | User's race. i.e Malay
religion | User's religion. i.e Islam
is_married | Indicate user's marriage status. Should pass boolean (true/false).
education | Indicate user's education level.
phone_number | User phone number, includes country code.
ic_num | User's ic number.

# Vehicle

## Get all vehicles

```shell
curl
  -H "Authorization: Bearer <token>"
  -H "Content-Type: application/json"
  -X GET
  ENDPOINT
```

> The above command returns JSON structured like this:

```json
{
    "vehicle": [
        {
            "id": 509,
            "vehicle_detail_id": 10,
            "user_id": 145,
            "is_insurance_valid": null,
            "year": 2014,
            "transmission": "Auto",
            "color": "White",
            "plate_num": "WA 9415 U",
            "is_verified": true,
            "is_available": true,
            "created_at": "2016-12-13T14:07:56.757+08:00",
            "updated_at": "2016-12-13T14:07:56.757+08:00",
            "description": "This is car description.",
            "roadtax": {
                "url": "http://.../file.jpg",
                "thumb": {
                    "url": "http://.../file.jpg"
                }
            },
            "insurance_covernote": {
                "url": "http://.../file.jpg",
                "thumb": {
                    "url": "http://.../file.jpg"
                }
            },
            "address": "NO. 26/2, JALAN PJS 3/34, TAMAN SRI MANJA 46000, PETALING JAYA",
            "latitude": 3.0748967,
            "longitude": 101.6438697,
            "view_count": 0,
            "distance": 2.91736860283402,
            "bearing": "251.871341032653",
            "reviews": [
                {
                    "id": 1,
                    "review_for": "",
                    "comment": "This car is awesome",
                    "created_at": "2016-12-13T14:07:56.757+08:00",
                    "updated_at": "2016-12-13T14:07:56.757+08:00",
                    "rating": 3,
                    "booking_id": 11
                },
                {
                    "id": 2,
                    "review_for": "",
                    "comment": "Joe is a friendly owner. His car is a badass supercar. Will repeat my booking for sure!",
                    "created_at": "2016-12-13T14:07:56.757+08:00",
                    "updated_at": "2016-12-13T14:07:56.757+08:00",
                    "rating": 4.5,
                    "booking_id": 13
                }
            ]
        },
        {
            "id": 110,
            "vehicle_detail_id": 28,
            "user_id": 145,
            "is_insurance_valid": null,
            "year": 2014,
            "transmission": "Auto",
            "color": "White",
            "plate_num": "G1M5306",
            "is_verified": true,
            "is_available": true,
            "created_at": "2016-12-13T14:07:24.780+08:00",
            "updated_at": "2016-12-14T12:32:53.535+08:00",
            "description": "This is car description.",
            "roadtax": {
                "url": "http://.../file.jpg",
                "thumb": {
                    "url": "http://.../file.jpg"
                }
            },
            "insurance_covernote": {
                "url": "http://.../file.jpg",
                "thumb": {
                    "url": "http://.../file.jpg"
                }
            },
            "address": "NO. 26/2, JALAN PJS 3/34, TAMAN SRI MANJA 46000, PETALING JAYA",
            "latitude": 3.0748967,
            "longitude": 101.6438697,
            "view_count": 6,
            "distance": 2.91736860283402,
            "bearing": "251.871341032653",
            "reviews": []
        }
    ]
}
```

This endpoint to show all available vehicles nearby.

### HTTP Request

`GET /vehicles?location_latitude=3.0748967&location_longitude=101.6438697&location_address=KLCC&begin_at=2016-12-13T14:07:24.780+08:00&end_at=2016-12-13T14:07:24.780+08:00&duration=32&type_id=1&model_id=33`

`Note: For default request, all params should be null. So it will get all vehicles within 15km radius.`

### Query Parameters

Parameter | Description
--------- | ------- | -----------
location_latitude | Searching location latitude.
location_longitude | Searching location longitude.
location_address | Searching location address.
begin_at | Vehicle booking begin time.
end_at | Vehicle booking end time.
duration | Renting duration in hour(s).
type_id | Type of vehicle id.
model_id | Model of vehicle id.

## Get a vehicle

```shell
curl
  -H "Authorization: Bearer <token>"
  -H "Content-Type: application/json"
  -X GET
  ENDPOINT
```

> The above command returns JSON structured like this:

```json
{
    "id": 509,
    "vehicle_detail_id": 10,
    "user_id": 145,
    "is_insurance_valid": null,
    "year": 2014,
    "transmission": "Auto",
    "color": "White",
    "plate_num": "WA 9415 U",
    "is_verified": true,
    "is_available": true,
    "created_at": "2016-12-13T14:07:56.757+08:00",
    "updated_at": "2016-12-13T14:07:56.757+08:00",
    "description": "This is car description.",
    "roadtax": {
        "url": "http://.../file.jpg",
        "thumb": {
            "url": "http://.../file.jpg"
        }
    },
    "insurance_covernote": {
        "url": "http://.../file.jpg",
        "thumb": {
            "url": "http://.../file.jpg"
        }
    },
    "address": "NO. 26/2, JALAN PJS 3/34, TAMAN SRI MANJA 46000, PETALING JAYA",
    "latitude": 3.0748967,
    "longitude": 101.6438697,
    "view_count": 0,
    "distance": 2.91736860283402,
    "bearing": "251.871341032653",
    "reviews": [
        {
            "id": 1,
            "review_for": "",
            "comment": "This car is awesome",
            "created_at": "2016-12-13T14:07:56.757+08:00",
            "updated_at": "2016-12-13T14:07:56.757+08:00",
            "rating": 3,
            "booking_id": 11
        },
        {
            "id": 2,
            "review_for": "",
            "comment": "Joe is a friendly owner. His car is a badass supercar. Will repeat my booking for sure!",
            "created_at": "2016-12-13T14:07:56.757+08:00",
            "updated_at": "2016-12-13T14:07:56.757+08:00",
            "rating": 4.5,
            "booking_id": 13
        }
    ]
}
```

This endpoint to show a vehicle.

### HTTP Request

`GET /vehicle/<id>`

## Review a vehicle

```shell
curl
  -H "Authorization: Bearer <token>"
  -H "Content-Type: application/json"
  -X POST
  -d '{"review_for": "", "comment": "This car is awesome", "rating": 3, "booking_id": 11}'
  ENDPOINT
```

> The above command returns JSON structured like this:

```json
{
  "status": "true",
  "message": "Your review has been successfully created."
}
```

This endpoint to create a review for a vehicle.

### HTTP Request

`POST /vehicle/<id>/review`

### Data Parameters

Parameter | Description
--------- | ------- | -----------
review_for | Review for...
comment | Comment that belong to a vehicle.
rating | Rating value for a vehicle.
booking_id | Booking id.

## List of owner vehicles

```shell
curl
  -H "Authorization: Bearer <token>"
  -H "Content-Type: application/json"
  -X GET
  ENDPOINT
```

> The above command returns JSON structured like this:

```json
{
    "id": 509,
    "vehicle_detail_id": 10,
    "user_id": 145,
    "is_insurance_valid": null,
    "year": 2014,
    "transmission": "Auto",
    "color": "White",
    "plate_num": "WA 9415 U",
    "is_verified": true,
    "is_available": true,
    "created_at": "2016-12-13T14:07:56.757+08:00",
    "updated_at": "2016-12-13T14:07:56.757+08:00",
    "description": "This is car description.",
    "roadtax": {
        "url": "http://.../file.jpg",
        "thumb": {
            "url": "http://.../file.jpg"
        }
    },
    "insurance_covernote": {
        "url": "http://.../file.jpg",
        "thumb": {
            "url": "http://.../file.jpg"
        }
    },
    "address": "NO. 26/2, JALAN PJS 3/34, TAMAN SRI MANJA 46000, PETALING JAYA",
    "latitude": 3.0748967,
    "longitude": 101.6438697,
    "view_count": 0,
    "distance": 2.91736860283402,
    "bearing": "251.871341032653",
    "reviews": [
        {
            "id": 1,
            "review_for": "",
            "comment": "This car is awesome",
            "created_at": "2016-12-13T14:07:56.757+08:00",
            "updated_at": "2016-12-13T14:07:56.757+08:00",
            "rating": 3,
            "booking_id": 11
        },
        {
            "id": 2,
            "review_for": "",
            "comment": "Joe is a friendly owner. His car is a badass supercar. Will repeat my booking for sure!",
            "created_at": "2016-12-13T14:07:56.757+08:00",
            "updated_at": "2016-12-13T14:07:56.757+08:00",
            "rating": 4.5,
            "booking_id": 13
        }
    ]
}
```

This endpoint to show a vehicle that belong to user.

### HTTP Request

`GET /user/<id>/vehicles`

## Create new vehicle

```shell
curl
  -H "Authorization: Bearer <token>"
  -H "Content-Type: application/json"
  -X POST
  -d '{"vehicle_detail_id":10,"year":2014,"transmission":"Auto","color":"Green","plate_num":"WUV 3271","is_available":true,"description":"It is very comfortable to ride in it. I think people will love the ride experience in a this car. Great gas saver especially when you have to do a lot of driving. Wish you enjoy the trip. No smoking or pets please! Safe drive.","roadtax":"base64String","insurance_covernote":"base64String","address":"Taman Sri Manja Petaling Jaya Selangor Malaysia","latitude":3.075213,"longitude":101.6469241}'
  ENDPOINT
```

> The above command returns JSON structured like this:

```json
{
    "id": 509,
    "vehicle_detail_id": 10,
    "user_id": 145,
    "is_insurance_valid": null,
    "year": 2014,
    "transmission": "Auto",
    "color": "White",
    "plate_num": "WA 9415 U",
    "is_verified": true,
    "is_available": true,
    "created_at": "2016-12-13T14:07:56.757+08:00",
    "updated_at": "2016-12-13T14:07:56.757+08:00",
    "description": "This is car description.",
    "roadtax": {
        "url": "http://.../file.jpg",
        "thumb": {
            "url": "http://.../file.jpg"
        }
    },
    "insurance_covernote": {
        "url": "http://.../file.jpg",
        "thumb": {
            "url": "http://.../file.jpg"
        }
    },
    "address": "NO. 26/2, JALAN PJS 3/34, TAMAN SRI MANJA 46000, PETALING JAYA",
    "latitude": 3.0748967,
    "longitude": 101.6438697,
    "view_count": 0,
    "distance": 2.91736860283402,
    "bearing": "251.871341032653",
    "reviews": [
        {
            "id": 1,
            "review_for": "",
            "comment": "This car is awesome",
            "created_at": "2016-12-13T14:07:56.757+08:00",
            "updated_at": "2016-12-13T14:07:56.757+08:00",
            "rating": 3,
            "booking_id": 11
        },
        {
            "id": 2,
            "review_for": "",
            "comment": "Joe is a friendly owner. His car is a badass supercar. Will repeat my booking for sure!",
            "created_at": "2016-12-13T14:07:56.757+08:00",
            "updated_at": "2016-12-13T14:07:56.757+08:00",
            "rating": 4.5,
            "booking_id": 13
        }
    ]
}
```

This endpoint to create new vehicle

### HTTP Request

`POST /user/<id>/vehicle/new`

## Update vehicle details

```shell
curl
  -H "Authorization: Bearer <token>"
  -H "Content-Type: application/json"
  -X POST
  -d '{"vehicle_detail_id":10, "is_insurance_valid":null, "year":2014, "transmission":"Auto", "color":"Green", "plate_num":"WUV 3271", "is_verified":true, "is_available":true, "description":"It is very comfortable to ride in it. I think people will love the ride experience in a this car. Great gas saver especially when you have to do a lot of driving. Wish you enjoy the trip. No smoking or pets please! Safe drive.", "roadtax": {"url":"http://.../file.jpg", "thumb":{"url":"http://.../file.jpg"}}, "insurance_covernote": {"url":"http://.../file.jpg", "thumb":{"url":"http://.../file.jpg"}}, "address":"Taman Sri Manja Petaling Jaya Selangor Malaysia", "latitude":3.075213, "longitude":101.6469241, "view_count":3}'
  ENDPOINT
```

> The above command returns JSON structured like this:

```json
{
    "id": 509,
    "vehicle_detail_id": 10,
    "user_id": 145,
    "is_insurance_valid": null,
    "year": 2014,
    "transmission": "Auto",
    "color": "White",
    "plate_num": "WA 9415 U",
    "is_verified": true,
    "is_available": true,
    "created_at": "2016-12-13T14:07:56.757+08:00",
    "updated_at": "2016-12-13T14:07:56.757+08:00",
    "description": "This is car description.",
    "roadtax": {
        "url": "http://.../file.jpg",
        "thumb": {
            "url": "http://.../file.jpg"
        }
    },
    "insurance_covernote": {
        "url": "http://.../file.jpg",
        "thumb": {
            "url": "http://.../file.jpg"
        }
    },
    "address": "NO. 26/2, JALAN PJS 3/34, TAMAN SRI MANJA 46000, PETALING JAYA",
    "latitude": 3.0748967,
    "longitude": 101.6438697,
    "view_count": 0,
    "distance": 2.91736860283402,
    "bearing": "251.871341032653",
    "reviews": [
        {
            "id": 1,
            "review_for": "",
            "comment": "This car is awesome",
            "created_at": "2016-12-13T14:07:56.757+08:00",
            "updated_at": "2016-12-13T14:07:56.757+08:00",
            "rating": 3,
            "booking_id": 11
        },
        {
            "id": 2,
            "review_for": "",
            "comment": "Joe is a friendly owner. His car is a badass supercar. Will repeat my booking for sure!",
            "created_at": "2016-12-13T14:07:56.757+08:00",
            "updated_at": "2016-12-13T14:07:56.757+08:00",
            "rating": 4.5,
            "booking_id": 13
        }
    ]
}
```

This endpoint to update vehicle detail

### HTTP Request

`POST /user/<id>/vehicle/<id>`

# Booking

## Current booking

```shell
curl
  -H "Authorization: Bearer <token>"
  -H "Content-Type: application/json"
  -X GET
  ENDPOINT
```

> The above command returns JSON structured like this:

```json
[
  {
      "id": 3,
      "user_id": 9,
      "vehicle_id": 15,
      "status": "requested",
      "starts": "2017-01-03T10:30:00.000+08:00",
      "ends": "2017-01-06T14:00:00.000+08:00",
      "process_type": "one_to_one",
      "paid": false,
      "total": "1120.0",
      "created_at": "2016-12-31T10:18:16.278+08:00",
      "updated_at": "2016-12-31T10:22:31.555+08:00",
      "comments": null,
      "token": "c6f2b93c49b15b65",
      "address": "Kuala Lumpur International Airport",
      "latitude": 3.146642,
      "longitude": 101.6958449,
      "wk": 0,
      "dy": 3,
      "hr": 3,
      "mn": "0.5"
  },
  {
      "id": 3,
      "user_id": 9,
      "vehicle_id": 15,
      "status": "requested",
      "starts": "2017-01-03T10:30:00.000+08:00",
      "ends": "2017-01-06T14:00:00.000+08:00",
      "process_type": "one_to_one",
      "paid": false,
      "total": "1120.0",
      "created_at": "2016-12-31T10:18:16.278+08:00",
      "updated_at": "2016-12-31T10:22:31.555+08:00",
      "comments": null,
      "token": "c6f2b93c49b15b65",
      "address": "Kuala Lumpur International Airport",
      "latitude": 3.146642,
      "longitude": 101.6958449,
      "wk": 0,
      "dy": 3,
      "hr": 3,
      "mn": "0.5"
  }
]
```
This endpoint to create a new vehicle booking

### HTTP Request

`GET /booking?status=current`

### Query Parameters

Parameter | Description
--------- | ------- | -----------
status | Booking status

## Booking history

```shell
curl
  -H "Authorization: Bearer <token>"
  -H "Content-Type: application/json"
  -X GET
  ENDPOINT
```

> The above command returns JSON structured like this:

```json
[
  {
      "id": 3,
      "user_id": 9,
      "vehicle_id": 15,
      "status": "rejected",
      "starts": "2017-01-03T10:30:00.000+08:00",
      "ends": "2017-01-06T14:00:00.000+08:00",
      "process_type": "one_to_one",
      "paid": false,
      "total": "1120.0",
      "created_at": "2016-12-31T10:18:16.278+08:00",
      "updated_at": "2016-12-31T10:22:31.555+08:00",
      "comments": null,
      "token": "c6f2b93c49b15b65",
      "address": "Kuala Lumpur International Airport",
      "latitude": 3.146642,
      "longitude": 101.6958449,
      "wk": 0,
      "dy": 3,
      "hr": 3,
      "mn": "0.5"
  },
  {
      "id": 3,
      "user_id": 9,
      "vehicle_id": 15,
      "status": "cancelled",
      "starts": "2017-01-03T10:30:00.000+08:00",
      "ends": "2017-01-06T14:00:00.000+08:00",
      "process_type": "one_to_one",
      "paid": false,
      "total": "1120.0",
      "created_at": "2016-12-31T10:18:16.278+08:00",
      "updated_at": "2016-12-31T10:22:31.555+08:00",
      "comments": null,
      "token": "c6f2b93c49b15b65",
      "address": "Kuala Lumpur International Airport",
      "latitude": 3.146642,
      "longitude": 101.6958449,
      "wk": 0,
      "dy": 3,
      "hr": 3,
      "mn": "0.5"
  },
  {
      "id": 3,
      "user_id": 9,
      "vehicle_id": 15,
      "status": "closed",
      "starts": "2017-01-03T10:30:00.000+08:00",
      "ends": "2017-01-06T14:00:00.000+08:00",
      "process_type": "one_to_one",
      "paid": false,
      "total": "1120.0",
      "created_at": "2016-12-31T10:18:16.278+08:00",
      "updated_at": "2016-12-31T10:22:31.555+08:00",
      "comments": null,
      "token": "c6f2b93c49b15b65",
      "address": "Kuala Lumpur International Airport",
      "latitude": 3.146642,
      "longitude": 101.6958449,
      "wk": 0,
      "dy": 3,
      "hr": 3,
      "mn": "0.5"
  }
]
```
This endpoint to show booking history

### HTTP Request

`GET /booking?status=history`

### Query Parameters

Parameter | Description
--------- | ------- | -----------
status | Booking status

## Create new vehicle booking (renter)

```shell
curl
  -H "Authorization: Bearer <token>"
  -H "Content-Type: application/json"
  -X POST
  -d '{"starts":"2017-01-03T10:30:00.000+08:00","ends":"2017-01-06T14:00:00.000+08:00","address":"Kuala Lumpur International Airport","latitude":3.146642,"longitude":101.6958449}'
  ENDPOINT
```

> The above command returns JSON structured like this:

```json
{
    "id": 3,
    "user_id": 9,
    "vehicle_id": 15,
    "status": "requested",
    "starts": "2017-01-03T10:30:00.000+08:00",
    "ends": "2017-01-06T14:00:00.000+08:00",
    "process_type": "one_to_one",
    "paid": false,
    "total": "1120.0",
    "created_at": "2016-12-31T10:18:16.278+08:00",
    "updated_at": "2016-12-31T10:22:31.555+08:00",
    "comments": null,
    "token": "c6f2b93c49b15b65",
    "address": "Kuala Lumpur International Airport",
    "latitude": 3.146642,
    "longitude": 101.6958449,
    "wk": 0,
    "dy": 3,
    "hr": 3,
    "mn": "0.5"
}
```
This endpoint to create a new vehicle booking

### HTTP Request

`POST /booking/new`

### Data Parameters

Parameter | Description
--------- | ------- | -----------
starts | Start booking date and time.
ends | End booking date and time.
address | Pickup address for the vehicle.
latitude | Pickup coordinate - latitude.
longitude | Pickup coordinate - longitude.

## Cancel a vehicle booking (renter)

```shell
curl
  -H "Authorization: Bearer <token>"
  -H "Content-Type: application/json"
  -X PUT
  ENDPOINT
```

> The above command returns JSON structured like this:

```json
{
    "id": 3,
    "user_id": 9,
    "vehicle_id": 15,
    "status": "cancelled",
    "starts": "2017-01-03T10:30:00.000+08:00",
    "ends": "2017-01-06T14:00:00.000+08:00",
    "process_type": "one_to_one",
    "paid": false,
    "total": "1120.0",
    "created_at": "2016-12-31T10:18:16.278+08:00",
    "updated_at": "2016-12-31T10:22:31.555+08:00",
    "comments": null,
    "token": "c6f2b93c49b15b65",
    "address": "Kuala Lumpur International Airport",
    "latitude": 3.146642,
    "longitude": 101.6958449,
    "wk": 0,
    "dy": 3,
    "hr": 3,
    "mn": "0.5"
}
```
This endpoint to cancel vehicle booking

### HTTP Request

`PUT /booking/<id>/cancel`

## Confirm a vehicle booking (owner)

```shell
curl
  -H "Authorization: Bearer <token>"
  -H "Content-Type: application/json"
  -X PUT
  ENDPOINT
```

> The above command returns JSON structured like this:

```json
{
    "id": 3,
    "user_id": 9,
    "vehicle_id": 15,
    "status": "confirmed",
    "starts": "2017-01-03T10:30:00.000+08:00",
    "ends": "2017-01-06T14:00:00.000+08:00",
    "process_type": "one_to_one",
    "paid": false,
    "total": "1120.0",
    "created_at": "2016-12-31T10:18:16.278+08:00",
    "updated_at": "2016-12-31T10:22:31.555+08:00",
    "comments": null,
    "token": "c6f2b93c49b15b65",
    "address": "Kuala Lumpur International Airport",
    "latitude": 3.146642,
    "longitude": 101.6958449,
    "wk": 0,
    "dy": 3,
    "hr": 3,
    "mn": "0.5"
}
```
This endpoint to confirmed vehicle booking

### HTTP Request

`PUT /booking/<id>/confirm`

## Reject a vehicle booking (owner)

# Promotion

## Validate a promo code
