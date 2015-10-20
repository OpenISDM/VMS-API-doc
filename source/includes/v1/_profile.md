# Profile

## Update profile

```http
PUT /users/me HTTP/1.1
Content-Type: application/json
Host: vms.app
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
Authorization: Bearer d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09

{
   "phone_number": "0988123456",
   "emergency_contact": "Johnson Su",
   "emergency_phone": "0978123456"
}
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
    "phone_number" : "0988123456",
    "email": "jimlin@citi.sinica.edu.tw",
    "emergency_contact": "Johnson Su",
    "emergency_phone": "0978123456",
    "introduction": "I’m a genius. I Work on Data science/analytics and have excellent skills with Matlab and Ruby programming. My hobbies is sporting.",
    "experiences": {
        "href": "https://vms.app/api/users/me/exeperiences" 
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
    "is_actived": true,
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

Update volunteer's own profile.

### ATTRIBUTE

| Attribute | Default | Description |
|-----------|---------|-------------|
| first_name | |   |
| last_name |  |  |
| birth_year |   |  |
| gender |  |  |
| city |  |  |
| address |  |  |
| introducation |  |  |
| phone_number |  |  |
| email |  |  |
| emergency_contact |  |  |
| emergency_phone |  |  |
| avatar_url |  |  |

*Note: If volunteer wants to change his/her password, please invoke /users/me/password API endpoint.*

<!-- update profile END -->


## Upload a new avatar image

```http
POST /users/me/avatar HTTP/1.1
Content-Type: multipart/form-data; boundary=Boundary_5_1873319439_1443827312034
Host: vms.app
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
Authorization: Bearer d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09

--Boundary_5_1873319439_1443827312034
Content-Type: image/jpeg
Content-Disposition: form-data; filename="jimlin_avatar.jpg"; name="avatar"

...(binary bytes of the image)...
--Boundary_5_1873319439_1443827312034--
```


> Successful response:

> The `skip_profile` value is `false`. It will return the following response:

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
    "phone_number" : "0988123456",
    "email": "jimlin@citi.sinica.edu.tw",
    "emergency_contact": "Johnson Su",
    "emergency_phone": "0978123456",
    "introduction": "I’m a genius. I Work on Data science/analytics and have excellent skills with Matlab and Ruby programming. My hobbies is sporting.",
    "experiences": {
        "href": "https://vms.app/api/users/me/exeperiences" 
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
    "is_actived": true,
    "updated_at": "2015-09-22 11:38:04",
    "created_at": "2015-09-20 22:30:47"
}
```

> The `skip_profile` value is `true` or not be set (default value is `true`). It will return the following response:

```http
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
    "avatar_url": "https://vms.app/upload/image/avatar/jimlin_366b4c757bff8643b9f97441a974d94d42f5877b.jpeg"
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

> If the image is uncorrect, it will return the following response: 

```http
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
    "message": "Something wrong",
    "errors": [
        {
            "code": "unable_to_upload_avatar"
        }
    ]
}
```

Upload volunteer's own avatar image.

The header attribute `Content-Type` value is `multipart/form-data`.

In the future, the endpoint may support base64 encoded image data.

### ATTRIBUTE

| Attribute | Default | Description |
|-----------|---------|-------------|
| avatar* |  | A binary raw data. It supports JPEG, JPG and PNG type. |
| skip_profile | false | If the value is true, it will skip to return volunteer's profile object. |

<!-- upload a new avatar image END -->



## Get experience

```http
GET /users/me/experiences HTTP/1.1
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
    "experience": [
        {
            "id": 1,
            "name": "Academia Sinica",
            "job_title": "Research Assistant",
            "start_year": 2014,
            "end_year": null
        }
    ]
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

Get volunteer's his/her own existing experience.

The response `experience` object is an array type.

<!-- get experience END -->



## Add a new experience

```http
POST /users/me/experiences HTTP/1.1
Content-Type: application/json
Host: vms.app
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
Authorization: Bearer d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09

{
    "name": "Academia Sinica",
    "job_title": "Research Assistant",
    "start_year": 2014,
    "end_year": null
}
```

> Successful response:

> It will return the following response and include the experience id:

```http
HTTP/1.1 201 Created
Content-Type: application/json;charset=UTF-8

{
    "experience" : {
        "id": 1
    }
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
            "field": ["job_title"],
            "code": "missing_field"
        }
    ]
}
```

Volunteer adds a new experience.

### ATTRIBUTE

| Attribute | Default | Description |
|-----------|---------|-------------|
| name* |  | Company name in the experience |
| job_title* | | Job title in the experience |
| start_year* | | Begin year in the exeperience |
| end_year | null | End year in the exeperience |


<!-- add a new experience END -->


## Update an experience

```http
PUT /users/me/experiences HTTP/1.1
Content-Type: application/json
Host: vms.app
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
Authorization: Bearer d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09

{
    "id": 1,
    "name": "Academia Sinica",
    "job_title": "Research Assistant",
    "start_year": 2014,
    "end_year": null
}
```

> Successful response:

```http
HTTP/1.1 204 No Content
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
            "field": ["job_title"],
            "code": "missing_field"
        }
    ]
}
```

> If the experience id doesn't exist, it will return the following response:

```http
HTTP/1.1 404 Not Found
Content-Type: application/json;charset=UTF-8

{
    "message": "Unable to find experience",
    "errors": [
        {
            "code": "unable_to_find_experience"
        }
    ]
}
```

> If the volunteer doesn't have right to access the resource, it will return the following response:

```http
HTTP/1.1 403 Forbidden
Content-Type: application/json;charset=UTF-8

{
    "message": "Not have right to access",
    "errors": [
        {
            "code": "cannot_access"
        }
    ]
}
```

Volunteer updates his/her own existing expereience.

### ATTRIBUTE

| Attribute | Default | Description |
|-----------|---------|-------------|
| experience* | | The experience id |
| name* |  | Company name in the experience |
| job_title* | | Job title in the experience |
| start_year* | | Begin year in the exeperience |
| end_year | null | End year in the exeperience |


<!-- Update an experience END -->



## Delete an experience

```http
DELETE /users/me/experiences/:id HTTP/1.1
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

> If the attribute is missing, it will return the following response:

```http
HTTP/1.1 422 Unprocessable Entity
Content-Type: application/json;charset=UTF-8

{
    "message": "Validation failed",
    "errors": [
        {
            "field": ["job_title"],
            "code": "missing_field"
        }
    ]
}
```

> If the experience id doesn't exist, it will return the following response:

```http
HTTP/1.1 404 Not Found
Content-Type: application/json;charset=UTF-8

{
    "message": "Unable to find the experience",
    "errors": [
        {
            "code": "unable_to_find_experience"
        }
    ]
}
```

> If the volunteer doesn't have right to access the resource, it will return the following response:

```http
HTTP/1.1 403 Forbidden
Content-Type: application/json;charset=UTF-8

{
    "message": "Not have right to access",
    "errors": [
        {
            "code": "cannot_access"
        }
    ]
}
```

Volunteer deletes his/her own existing expereience.

### PARAMETER

| Parameter | Default | Description |
|-----------|---------|-------------|
| :id* | | The experience id which volunteer wants to delete |

<!-- Delete an experience END -->



## Get education

```http
GET /users/me/educations HTTP/1.1
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
    "education": [
        {
            "id": 1,
            "school": "National Cheng Kung University",
            "degree": 5,
            "field_of_study": "Computer Science",
            "start_year": 2012,
            "end_year": 2014
        }
    ]
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

Get volunteer's his/her own existing education.

The response `education` object is an array type.

<!-- get experience END -->



## Add a new education


```http
POST /users/me/educations HTTP/1.1
Content-Type: application/json
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
Authorization: Bearer d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09

{
    "school": "NCKU",
    "degree": 5,
    "field_of_study": "Computer Science",
    "start_year": 2012,
    "end_year": 2014
}
```

> Successful response:

> It will return the following response, it includes the experience id:

```http
HTTP/1.1 201 Created
Content-Type: application/json;charset=UTF-8

{
    "education": {
        "id": 1
    }
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
            "field": ["degree"],
            "code": "missing_field"
        }
    ]
}
```

Volunteer adds a new education.

### ATTRIBUTE

| Attribute | Default | Description |
|-----------|---------|-------------|
| school* | | School name |
| degree* | | The education degree |
| field_of_study | null | The major field of study  |
| start_year* | | Start year in the education |
| end_year | null | End year in the education. If until now, it is optional. |

<!-- add a new education END -->


## Update an education

| Endpoint | Action | Description |
|--------|------|-----------|
| `` | PUT |  |


```http
PUT /users/me/educations HTTP/1.1
Content-Type: application/json
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
Authorization: Bearer d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09

{
    "id": "jimlin_1",
    "school": "National Cheng Kung University",
    "degree": 5,
    "field_of_study": "Computer Science",
    "start_year": 2012,
    "end_year": 2014
}
```

> Successful response:

```http
HTTP/1.1 204 No Content
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
            "field": ["degree"],
            "code": "missing_field"
        }
    ]
}
```

> If the experience id doesn't exist, it will return the following response:

```http
HTTP/1.1 404 Not Found
Content-Type: application/json;charset=UTF-8

{
    "message": "Unable to find education",
    "errors": [
        {
            "code": "unable_to_find_education"
        }
    ]
}
```

> If the volunteer doesn't have right to access the resource, it will return the following response:

```http
HTTP/1.1 403 Forbidden
Content-Type: application/json;charset=UTF-8

{
    "message": "Not have right to access",
    "errors": [
        {
            "code": "cannot_access"
        }
    ]
}
```

Volunteer updates his/her own existing education record

### ATTRIBUTE

| Attribute | Default | Description |
|-----------|---------|-------------|
| id* | | The education ID |
| school* | | School name |
| degree* | | The education degree |
| field_of_study | null | The major field of study  |
| start_year* | | Start year in the education |
| end_year | null | End year in the education. If until now, it is optional. |

<!-- add a new education END -->



## Delete an education

```http
DELETE /users/me/experiences/:id HTTP/1.1
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

> If the experience id doesn't exist, it will return the following response:

```http
HTTP/1.1 404 Not Found
Content-Type: application/json;charset=UTF-8

{
    "message": "Unable to find education",
    "errors": [
        {
            "code": "unable_to_find_education"
        }
    ]
}
```

> If the volunteer doesn't have right to access the resource, it will return the following response:

```http
HTTP/1.1 403 Forbidden
Content-Type: application/json;charset=UTF-8

{
    "message": "Not have right to access",
    "errors": [
        {
            "code": "cannot_access"
        }
    ]
}
```

Volunteer deletes his/her own existing education.

### Parameter

| Parameter | Default | Description |
|-----------|---------|-------------|
| :id* | | The education ID |

<!-- delete an education END -->



## Update skills

```http
POST /users/me/skills HTTP/1.1
Content-Type: application/json
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
Authorization: Bearer d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09

{
    "skills": [
        "Swimming",
        "Programming",
        "Rope rescue"
    ],
    "existing_skill_indexes": [
        0,
        1
    ]
}
```

> Successful response

```http
HTTP/1.1 204 No Content
```

> Failure response

> If there is a missing field, it will return the following request:

```http
HTTP/1.1 422 Unprocessable Entity
Content-Type: application/json;charset=UTF-8

{
    "message": "Validation failed",
    "errors": [
        {
            "field": ["existing_skill_index"],
            "code": "missing_field"
        }
    ]
}
```

> If something wrong happens, it will return the following request:

```http
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
    "message": "Unable to execute",
    "errors": [
        {
           "code": "exceeding_index_value"
        }
    ]
}
```

**It's NOT CONFIRMED.**

Update volunteer's skills.

### ATTRIBUTE

| Attribute | Default | Description |
|-----------|---------|-------------|
| skills*   |         | It's an array type.  |
| existing_skill_indexes* | | It means the `skills` array index of existing skills. |

### Request description

The `Swimming` and `Programming` skills exist and `Rop rescue` skill doesn't exist. The `existing_skill_indexes` means the `skills` array index of existing skills.

<!-- update skill END -->



## Update equipment

```http
POST /users/me/equipment HTTP/1.1
Content-Type: application/json
Host: vms.app
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
Authorization: Bearer d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09

{
    "equipment": [
        "Car",
        "Scooter",
        "Camera"
    ],
    "existing_equipment_indexes": [
        0,
        1,
        2
    ]
}
```

> Successful response:

```http
HTTP/1.1 204 No Content
```

> Failure response:

> If there is a missing field, it will return the following request:

```http
HTTP/1.1 422 Unprocessable Entity
Content-Type: application/json;charset=UTF-8

{
    "message": "Validation failed",
    "errors": [
        {
            "field": ["existing_equipment_indexes"],
            "code": "missing_field"
        }
    ]
}
```

> If something wrong happens, it will return the following request:

```http
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
    "message": "Unable to execute",
    "errors": [
        {
           "code": "exceeding_index_value"
        }
    ]
}
```

Delete volunteer's equipment.

### ATTRIBUTE

| Attribute | Default | Description |
|-----------|---------|-------------|
| equipment*   |         | It's an array type.  |
| existing_equipment_indexes* | | It means the `equipment` array index of existing skills. |

### Request description

The `Car`, `Scooter` and `Camera` equipment exist. The `existing_equipment_indexes` means the `equipment` array index of existing equipment.

<!-- update equipment END -->



## Get country cities

```http
POST /country/:country_name/:state_name/cities?locale=zh-TW HTTP/1.1
Content-Type: application/json
Host: vms.app
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
```

> Successful response

```http
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
    "country_zh_tw": "臺灣",
    "cities": [
        {
            "id": 1,
            "name": "臺北市"
        },
        {
            "id": 2,
            "name": "新北市"
        },
        {
            "id": 3,
            "name": "桃園市"
        },
        {
            "id": 4,
            "name": "臺中市"
        },
        {
            "id": 5,
            "name": "臺南市"
        },
        {
            "id": 6,
            "name": "新竹市"
        },
        {
            "id": 7,
            "name": "嘉義市"
        },
        {
            "id": 8,
            "name": "新竹縣"
        }, 
        {
            "id": 9,
            "name": "苗栗縣"
        },
        {
            "id": 10,
            "name": "新北市"
        },
        {
            "id": 11,
            "name": "彰化縣"
        },
        {
            "id": 12,
            "name": "南投縣"
        },
        {
            "id": 13,
            "name": "雲林縣"
        },
        {
            "id": 14,
            "name": "嘉義縣"
        },
        {
            "id": 15,
            "name": "屏東縣"
        },
        {
            "id": 16,
            "name": "花蓮縣"
        },
                {
            "id": 17,
            "name": "臺東縣"
        },
        {
            "id": 18,
            "name": "澎湖縣"
        },
        {
            "id": 19,
            "name": "金門縣"
        },
        {
            "id": 20,
            "name": "連江縣"
        }
   ]
}
```

> Failure response

> If the country or state name don't exist, it will return the following response:

```http
HTTP/1.1 404 Not Found
Content-Type: application/json;charset=UTF-8

{
    "message": "Unable to find cities",
    "errors": [
        {
            "code": "unable_to_find_cities"
        }
    ]
}
```

**NOTICE: This endpoint and result format MAY be changed!**

### PARAMETER

| Parameter | Default | Description |
|-----------|---------|-------------|
| locale    |  en-US  | The language and country codes |

The language codes are two-letter lowercase ISO language codes (such as "zh") as defined by [ISO 639-1](http://en.wikipedia.org/wiki/ISO_639-1). 
The country codes are two-letter uppercase ISO country codes (such as "TW") as defined by [ISO 3166-1](http://en.wikipedia.org/wiki/ISO_3166-1_alpha-3)

<!-- get country cities END -->



## Get skill keyword

```http
GET /skill_candidates/:keyword HTTP/1.1
Content-Type: application/json`
Host: vms.app
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09`
```

> Successful response:

```http
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
    "result": [
        {
            "name": "Disaster Survellience",
            "id": 34,
            "head_line": "<strong>Dis</strong>aster Survellience"
        },
        {
            "name": "Disaster Recovery",
            "id": 35,
            "head_line": "<strong>Dis</strong>aster Recovery"
        },
    ]
}
```

> If the keyword is not found, it will return the following response and the result array is empty:

```http
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
    "result": [
    ]
}
```

> Failure response:


The API endpoint can search the skill keyword.

| Parameter | Default | Description |
|-----------|---------|-------------|
| :keyword* |   | The searched keyword |

<!-- Get skill keyword -->



## Get equipment keyword

```http
POST /equipment_candidates/:keyword HTTP/1.1
Content-Type: application/json`
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09`
```

> Successful response:

```http
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
    "result": [
        {
            "name": "Car",
            "id": 21,
            "head_line": "<strong>Ca</strong>r"
        },
        {
            "name": "Camera",
            "id": 43,
            "head_line": "<strong>Ca</strong>mera"
        },
    ]
}
```

> If the keyword is not found, it will return the following response and the result array is empty:

```http
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
    "result": [
    ]
}
```

> Failure response:


The API endpoint can search the skill keyword.

| Parameter | Default | Description |
|-----------|---------|-------------|
| :keyword* |   | The searched keyword |

<!-- Get equipment keyword -->

