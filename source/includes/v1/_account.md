# Account

## Register

```http
POST /api/register HTTP/1.1
Host: vms.app
Content-Type: application/json
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09

{
    "username" : "jimlin",
    "password" : "MYPASSW0RD",
    "first_name" : "Lin",
    "last_name" : "Jim",
    "birth_year" : 2015,
    "gender" : "male",
    "city" : {
    	"id": 1,
    	"name_zh_tw": "臺北市",
    	"name_en": "Taipei City"
    },
    "address" : "128 Academia Road, Section 2, Nankang Dist.",
    "phone_number" : "0912345678",
    "email" : "jimlin@citi.sinica.edu.tw",
    "emergency_contact" : "Jeremy Lin",
    "emergency_phone" : "0919119119",
    "introduction": "I'm genius and work on Julia programming language.",
    "avatar": "data:image/jpg;base64,/9j/4AAQSkZJRgABAgAAAQABAAD/2wB...."
}
```

> Successful response:

```http
HTTP/1.1 201 Created
Content-Type: application/json;charset=UTF-8

{
    "href": "https://vms.app/api/users/me",
    "username": "jimlin",
    "auth_access_token": "56f4da226eb22caa0633023bfdd402658e5c6501c972e83bfb2866f2112b103f"
}
```

> Failure response:

> If the attribute is missing, it will return the following response:

```http
HTTP/1.1 422 Unprocessable Entity
Content-Type: application/json;charset=UTF-8

{
    "message": "422 Unprocessable Entity",
    "errors": {
        "username": ["missing_field"],
        "password": ["missing_field"]
    },
    "status_code":422
}
```

> If the password strength is not enough, it will return the following response:

```http
HTTP/1.1 422 Unprocessable Entity
Content-Type: application/json;charset=UTF-8

{
    "message": "422 Unprocessable Entity",
    "errors": {
        "username": ["missing_field"],
        "password": ["not_enough_password_strength"]
    },
    "status_code":422
}
```

> If the username or email address was used, it will return the following response:

```http
HTTP/1.1 422 Unprocessable Entity
Content-Type: application/json;charset=UTF-8

{
    "message": "422 Unprocessable Entity",
    "errors": {
        "username": ["used_field"],
        "email": ["used_field"]
    },
    "status_code":422
}
```

Volunteer registers a new account. The system will send a verification email to volunteer mailbox with an link.

### ATTRIBUTE

| Attribute | Default | Description |
|-----------|---------|-------------|
| username* |  |  |
| password* |  |  |
| first_name* | |   |
| last_name* |  |  |
| birth_year* |   |  |
| gender* |  |  |
| city* |  |  |
| address* |  |  |
| phone_number* |  |  |
| email* |  |  |
| emergency_contact* |  |  |
| emergency_phone* |  |  |
| introduction |  |  |
| avatar |  | In base64 format |

### city ATTRIBUTE

| Attribute | Default | Description |
|-----------|---------|-------------|
| id*        |  |  |
| name_zh_tw|  |  |
| name_en   |  |  |

<!-- register END -->


## Login


```http
POST /api/auth HTTP/1.1
Host: vms.app
Content-Type: application/json
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09

{
    "username": "ymhuang",
    "password": "MYPASSW0RD"
}
```

> Successful response:

```http
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOi8vdm1zLmFwcC9hcGkvYXV0aCIsImlhdCI6MTQ2NjczODYzNiwiZXhwIjoxNDY2NzQ5NDM2LCJuYmYiOjE0NjY3Mzg2MzYsImp0aSI6IjA5Zjc4YzU3ZTlhZTA3ZmIxODM5MjYyMTk1MzJmM2NhIiwic3ViIjoxfQ.g88pt_VjY5BFYSuL7Km__0B8a-Pc-XeyAl2GUbgyreU


{
  "data": {
    "username": "ymhuang",
    "first_name": "Huang",
    "last_name": "AMing",
    "birth_year": 1991,
    "gender": "male",
    "city": {
      "id": 2,
      "name_en": "New Taipei City"
    },
    "location": "Nangan",
    "phone_number": "0912345678",
    "email": "ymhuang@cc.com",
    "emergency_contact": "HuangPaPa",
    "emergency_phone": "0910234567",
    "introduction": "Wahahaaaqqqqaaabbb",
    "experiences": {
      "href": "http://vms.app/api/users/me/experiences"
    },
    "educations": {
      "href": "http://vms.app/api/users/me/educations"
    },
    "skills": [
      {
        "id": 1,
        "name": "programming"
      },
      {
        "id": 2,
        "name": "java"
      },
      {
        "id": 3,
        "name": "PHP"
      }
    ],
    "equipment": [
      {
        "id": 1,
        "name": "car"
      },
      {
        "id": 2,
        "name": "computer"
      }
    ],
    "projects": {
      "href": "http://vms.app/api/users/me/projects"
    },
    "processes": {
      "participating_number": 0,
      "participated_number": 0,
      "href": "http://vms.app/api/users/me/processes"
    },
    "avatar_url": "http://vms-openisdm.s3-website-ap-northeast-1.amazonaws.com/upload/avatars/bc26c925ee763bc0618b.png",
    "is_actived": true,
    "updated_at": {
      "date": "2016-06-24 02:09:20.000000",
      "timezone_type": 3,
      "timezone": "UTC"
    },
    "created_at": {
      "date": "2016-04-11 05:57:47.000000",
      "timezone_type": 3,
      "timezone": "UTC"
    }
  }
}
```

> Failure response:

> If the volunteer's credential is wrong, it will return the following response:

```http
HTTP/1.1 401 Unauthorized
Content-Type: application/json;charset=UTF-8

{
    "message": "Unauthorized",
    "errors": [
        "unauthorized"
    ]
}
```

> If the attribute is missing, it will return the following response:

```http
HTTP/1.1 422 Unprocessable Entity
Content-Type: application/json;charset=UTF-8

{
    "message": "422 Unprocessable Entity",
    "errors": {
        "username": ["missing_field"],
        "password": ["missing_field"]
    },
    "status_code":422
}
```

Volunteer logs into the system with credentials.

### Request attributes

| Attribute | Default | Description |
|-----------|---------|-------------|
| username* |  | volunteer's username |
| password* |  | volunteer's password |


The response will contains token in `Authorization` header.

<!-- login END -->


## Logout


```http
DELETE /api/auth HTTP/1.1
Content-Type: application/json
Host: vms.app
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
Authorization: Bearer d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
```

> Successful response:

```http
HTTP/1.1 204 No Content
```

> Failure response:

> If the volunteer's JWT is not validated, it will return the following response:

```http
HTTP/1.1 401 Not Found
Content-Type: application/json;charset=UTF-8

{
    "message": "Token Signature could not be verified.",
    "status_code": 401
}
```

Volunteer logout the system. The `Authorization` will be deleted.

<!-- logout END -->


## Authentication & retrieve volunteer's own account

```http
GET /users/me HTTP/1.1
Content-Type: application/json
Host: vms.app
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
Authorization: Bearer d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
```

> Successful response:

```http
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
    "username": "jimlin",
    "first_name": "Lin",
    "last_name": "Jim",
    "birth_year": 2015,
    "gender": "male",
    "city" : {
    	"id": 1,
    	"name_zh_tw": "臺北市",
    	"name_en": "Taipei City"
    },
    "address": "128 Academia Road, Section 2, Nankang Dist.",
    "phone_number" : "0912345678",
    "email": "jimlin@citi.sinica.edu.tw",
    "emergency_contact": "Jeremy Lin",
    "emergency_phone": "0919119119",
    "introduction": "I’m a genius. I Work on Data science/analytics and have excellent skills with Matlab and Ruby programming. My hobbies is sporting.",
    "experiences": {
        "href": "https://vms.app/api/users/me/experiences"
    },
    "educations": {
        "href": "https://vms.app/api/users/me/educations"
    },
    "skills": [
        {
            "name": "Swimming",
            "id": 82            
        },
        {
            "name": "Programming",
            "id": 73
        }
    ],
    "equipment": [
        {
            "name": "Car",
            "id": 21
        },
        {
            "name": "Scooter",
            "id": 28
        },
        {
            "name": "Camera",
            "id": 43
        }
    ],
    "projects": {
        "href": "https://vms.app/api/users/me/projects"
    },
    "processes": {
        "participating_number": 3,
        "participated_number": 8,
        "href": "https://vms.app/api/users/me/proccesses"
    },
    "avatar_url": "https://vms.app/upload/image/avatar/jimlin_366b4c757bff8643b9f97441a974d94d42f5877b.jpeg",
    "updated_at": "2015-09-22 11:38:04",
    "created_at": "2015-09-20 22:30:47"
}
```

If the `Authorization` is validated, it will return the volunteer's profile object.

<!-- authentication END -->

## Resend email address verification

```http
POST /email_verification HTTP/1.1
Content-Type: application/json
Host: vms.app
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
Authorization: Bearer d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09

{
    "email_address": "jimlin@citi.sinica.edu.tw"
}
```

> Successful response:

```http
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
    "message": "Resend verification email successfully"
}
```

Resend a verification email. A new verification email will send to volunteer's mailbox.

### ATTRIBUTE

| Attribute | Default | Description |
|-----------|---------|-------------|
| email_address* |  |  |


<!-- resend email address verification END -->


## Verify email address

```http
GET /email_verification/:email_address/:verification_token HTTP/1.1
Content-Type: application/json
Host: vms.app
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
Authorization: Bearer d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
```

> Success response:

```http
HTTP/1.1 200 Ok

{
    "message": "Successful email verification"
}
```

> If the verification token is unvalidated or expired, it will return the following response:

```http
HTTP/1.1 404 Not Found
Content-Type: application/json;charset=UTF-8

{
    "message": "Unvalidated or expired verification token",
    "errors": [
        "unvalidated_expired_verification_token"
    ]
}
```

Verify volunteer's email. The volunteer must be authenticated successfully.


| Attribute | Default | Description |
|-----------|---------|-------------|
| :email_address* |  | Volunteer's email address |
| :verification_code* |  | An unique token for identifying |


<!-- verify email address END -->


## Request for a password reset

```http
POST /users/password_reset HTTP/1.1
Content-Type: application/json
Host: vms.app
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09

{
   "email": "jimlin@citi.sinica.edu.tw"
}
```

> Successful response:

```http
HTTP/1.1 204 No Content
```


Volunteer forgot his/her password. It sends a password reset email to the volunteer.

### ATTRIBUTE

| Attribute | Default | Description |
|-----------|---------|-------------|
| email* |  | Volunteer's validated email address |

<!-- request for a password reset END -->


## Reset passowrd

```http
PUT /users/password_reset/:email_address/:reset_password_token HTTP/1.1
Content-Type: application/json
Host: vms.app
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09

{
   "password": "MY_RESET_PASSW0RD"
}
```

> Successful response:

```http
HTTP/1.1 204 No Content
```

> Failure response:

> If the field is misssing, it will return the following response:

```http
HTTP/1.1 422 Unprocessable Entity
Content-Type: application/json;charset=UTF-8

{
    "message": "Validation failed",
    "errors": [
        {
            "field": ["password"],
            "code": "missing_field"
        }
    ]
}
```

> If the volunteer's password is unsecure, it will return the following response:

```http
HTTP/1.1 422 Unprocessable Entity
Content-Type: application/json;charset=UTF-8

{
    "message": "Validation failed",
    "errors": [
        {
            "field": ["password"],
            "code": "unsecure_password"
        }
    ]
}
```

> If the volunteer's email or reset passowrd are unvalidated, it will return the following response:

```http
HTTP/1.1 403 Forbidden
Content-Type: application/json;charset=UTF-8

{
    "message": "Not validated token",
    "errors": [
        {
            "code": "cannot_access"
        }
    ]
}
```

### PARAMETER

| Parameter | Default | Description |
|-----------|---------|-------------|
| :email_address* |  | Volunteer's email address |
| :reset_password_token* |  | The unique reset password token |

### ATTRIBUTE

| Attribute | Default | Description |
|-----------|---------|-------------|
| password* |  | Volunteer's new password (8 ~ 255 characters) |

<!-- reset password reset END -->


## Changes his/her own password

```http
PUT /users/me/password HTTP/1.1
Content-Type: application/json
Host: vms.app
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
Authorization: Bearer d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09

{
   "existing_password": "MYPASSW0RD",
   "new_password": "MY_NEW_PASSWoRD"
}
```

> Successful response:

```http
HTTP/1.1 204 No Content
```

> Failure response:

> If the volunteer doesn't have right to access (ex. `existing_password` is not correct), it will return the following response:

```http
HTTP/1.1 403 Forbidden
Content-Type: application/json;charset=UTF-8

{
    "message": "Forbidden to access",
    "errors": [
        {
            "code": "cannot_access"
        }
    ]
}
```

Volunteer changes his/her own password.

| Attribute | Default | Description |
|-----------|---------|-------------|
| existing_passowrd* |  | Volunteer's existing password (8 ~ 255 characters) |
| new_password* |  | Volunteer's new password (8 ~ 255 characters) |


<!-- Change his/her own password END -->
