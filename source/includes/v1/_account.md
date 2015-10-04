# Account

## Register

```http
POST /api/v1.0/register HTTP/1.1
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
    "emergency_phone" : "0919119119"
}
```

> Successful response:

```http
HTTP/1.1 201 Created
Content-Type: application/json;charset=UTF-8

{
    "href": "https://vms.app/api/v1.0/users/me",
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
    "message": "Validation failed",
    "errors": [
        {
            "field": ["username", "password"],
            "code": "missing_field"
        }
    ]
}
```

> If the password strength is not enough, it will return the following response:

```http
HTTP/1.1 422 Unprocessable Entity
Content-Type: application/json;charset=UTF-8

{
    "message": "Validation failed",
    "errors": [
        {
            "field": ["passsword"],
            "code": "not_enough_password_strength"
        }
    ]
}
```

> If the username or email address was used, it will return the following response:

```http
HTTP/1.1 422 Unprocessable Entity
Content-Type: application/json;charset=UTF-8

{
    "message": "Validation failed",
    "errors": [
        {
            "field": ["username", "password"],
            "code": "used_field"
        }
    ]
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

### city ATTRIBUTE

| Attribute | Default | Description |
|-----------|---------|-------------|
| id*        |  |  |
| name_zh_tw|  |  |
| name_en   |  |  |

<!-- register END -->


## Login


```http
POST /api/v1.0/auth HTTP/1.1
Host: vms.app
Content-Type: application/json
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09

{
    "username": "jimlin",
    "password": "MYPASSW0RD"
}
```

> Successful response:

```http
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
    "href": "https://vms.app/api/v1.0/users/me",
    "auth_access_token": "56f4da226eb22caa0633023bfdd402658e5c6501c972e83bfb2866f2112b103f"
}
```

> Failure response:

> If the volunteer's credential is wrong, it will return the following response:

```http
HTTP/1.1 401 Unauthorized
Content-Type: application/json;charset=UTF-8

{
    "message": "Authentication failed",
    "errors": [
        {
            "code": "incorrect_login_credentials"
        }
    ]
}
```

> If the attribute is missing, it will return the following response:

```http
HTTP/1.1 422 Unprocessable Entity
Content-Type: application/json;charset=UTF-8

{
    "message": "Validation failed",
    "errors": [
        {
            "field": ["username", "password"],
            "code": "missing_field"
        }
    ]
}
```

Volunteer logs into the system with credentials.

### ATTRIBUTE

| Attribute | Default | Description |
|-----------|---------|-------------|
| username* |  | volunteer's username |
| password* |  | volunteer's password |

<!-- login END -->


## Logout


```http
DELETE /api/v1.0/auth HTTP/1.1
Content-Type: application/json
Host: vms.app
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
X-VMS-Auth-Token: jimlin:d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
```

> Successful response:

```http
HTTP/1.1 204 No Content
```

> Failure response:

> If the volunteer's `auth_access_token` doesn't exist, it will return the following response:

```http
HTTP/1.1 404 Not Found
Content-Type: application/json;charset=UTF-8

{
    "message": "Failed to logout",
    "errors": [
        {
            "code": "no_existing_auth_access_token"
        }
    ]
}
```

Volunteer logout the system. The `X-VMS-Auth-Token` will be deleted.

<!-- logout END -->


## Authentication & retrieve volunteer's own account

```http
GET /api/v1.0/users/me HTTP/1.1
Content-Type: application/json
Host: vms.app
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
X-VMS-Auth-Token: jimlin:d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
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
    "experience": {
        "href": "https://vms.app/api/v1.0/users/me/exeperience" 
    },
    "education": {
        "href": "https://vms.app/api/v1.0/users/me/education"
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
        "href": "https://vms.app/api/v1.0/users/me/projects"
    },
    "processes": {
        "participating_number": 3,
        "participated_number": 8,
        "href": "https://vms.app/api/v1.0/users/me/proccesses"
    },
    "avatar_url": "https://vms.app/upload/image/avatar/jimlin_366b4c757bff8643b9f97441a974d94d42f5877b.jpeg",
    "updated_at": "2015-09-22 11:38:04",
    "created_at": "2015-09-20 22:30:47"
}
```

> Failure response:

> If the volunteer doesn't have right to access, it will return the following response:

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

If the `X-VMS-Auth-Token` is validated, it will return the volunteer's profile object.

<!-- authentication END -->

## Resend email address verification

```http
POST /email_verification HTTP/1.1
Content-Type: application/json
Host: vms.app
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
X-VMS-Auth-Token: jimlin:d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09

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

> Failure response:

> If the volunteer doesn't have right to access, it will return the following response:

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
X-VMS-Auth-Token: jimlin:d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
```

> Success response:

```http
HTTP/1.1 200 Ok

{
    "message": "Successful email verification"
}
```

> Failure response:

> If the volunteer doesn't have right to access, it will return the following response:

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

> If the verification token is unvalidated or expired, it will return the following response:

```http
HTTP/1.1 404 Not Found
Content-Type: application/json;charset=UTF-8

{
    "message": "Unvalidated or expired verification token",
    "errors": [
        {
           "code": "unvalidated_expired_verification_token"
        }
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
POST /api/v1.0/request_password_reset HTTP/1.1
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

> Failure response:

> If the field is misssing, it will return the following response: 

```http
HTTP/1.1 422 Unprocessable Entity
Content-Type: application/json;charset=UTF-8

{
    "message": "Validation failed",
    "errors": [
        {
            "field": ["username"],
            "code": "missing_field"
        }
    ]
}
```

> If the email is unvalidated, it will return the following response: 

```http
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
    "message": "Validation failed",
    "errors": [
        {
            "field": ["username"],
            "code": "unvalidated_username"
        }
    ]
}
```

Volunteer forgot his/her password. It sends a password reset email to the volunteer.

### ATTRIBUTE

| Attribute | Default | Description |
|-----------|---------|-------------|
| email* |  | Volunteer's validated email address |

<!-- request for a password reset END -->


## Reset passowrd

```http
POST /api/v1.0/reset_password/:email_address/:reset_password_token HTTP/1.1
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
HTTP/1.1 400 Bad Request
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
X-VMS-Auth-Token: jimlin:d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09

{
   "existing_passowrd": "MYPASSW0RD",
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
