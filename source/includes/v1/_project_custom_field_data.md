# Project Custom Field Data

*This endpoints are unstable.*

## Fill bulk of custom field data

```http
POST /projects/:project_id/members/bulk_custom_field_data HTTP/1.1
Host: vms.app
Content-Type: application/json
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
Authorization: Bearer d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09

[
    {
        "payload": {
            "value": "Academia Sinica"
        },
        "custom_field": {
            "id": 1
        }
    },
    {
        "payload": {
            "value": "Teacher"
        },
        "custom_field": {
            "id": 2
        }
    }
]
```

> Successful response:

```http
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
    "message": "Update custom field data successfully",
    "data": [
        {
            "payload": {
                "value": "Academia Sinica"
            },
            "custom_field": {
                "id": 1,
                "name": "Which school?",
                "type": "text",
                "description": "Enter your school name",
                "required": true,
                "order": 1
            }
        },
        {
            "payload": {
                "value": "Teacher"
            },
            "custom_field": {
                "id": 2,
                "name": "Teacher or student?",
                "type": "radio_button",
                "description": "Please select your position",
                "required": true,
                "order": 2,
                "metadata": {
                    "options": [
                        {
                            "display_name": "Teacher"
                        },
                        {
                            "display_name": "Student"
                        }
                    ]
                }
            }
        }
    ]
}
```

> Failure response:

> If ...

```http
```

## Get member's own custom field data

```http
GET /projects/:project_id/members/custom_field_data HTTP/1.1
Host: vms.app
Content-Type: application/json
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
Authorization: Bearer d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
```

> Successful response:

```http
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
    "data": [
        {
            "payload": {
                "value": "Academia Sinica"
            },
            "custom_field": {
                "id": 1,
                "name": "Which school?",
                "type": "text",
                "description": "Enter your school name",
                "required": true,
                "order": 1
            }
        },
        {
            "payload": {
                "value": "Teacher"
            },
            "custom_field": {
                "id": 2,
                "name": "Teacher or student?",
                "type": "radio_button",
                "description": "Please select your position",
                "required": true,
                "order": 2,
                "metadata": {
                    "options": [
                        {
                            "display_name": "Teacher"
                        },
                        {
                            "display_name": "Student"
                        }
                    ]
                }
            }
        }
    ]
}
```

> Failure response:

> If ...

```http
```

## Get all members' custom field data

```http
GET /projects/:project_id/members/all_custom_field_data HTTP/1.1
Host: vms.app
Content-Type: application/json
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
Authorization: Bearer d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
```

> Successful response:

```http
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
    "data": [
        {
            "custom_field_data": [
                {
                    "payload": {
                        "value": "Academia Sinica"
                    },
                    "custom_field": {
                        "id": 1
                    }
                },
                {
                    "payload": {
                        "value": "Teacher"
                    },
                    "custom_field": {
                        "id": 2
                    }
                },
            ],
            "user": {
                "id": 1,
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
                "avatar_url": "https://vms.app/upload/image/avatar/jimlin_366b4c757bff8643b9f97441a974d94d42f5877b.jpeg",
                "is_actived": true
            }
        }
    ],
    "included": {
        "custom_field": [
            {
                "id": 1,
                "name": "Which school?",
                "type": "text",
                "description": "Enter your school name",
                "required": true,
                "order": 1
            },
            {
                "id": 2,
                "name": "Teacher or student?",
                "type": "radio_button",
                "description": "Please select your position",
                "required": true,
                "order": 2,
                "metadata": {
                    "options": [
                        {
                            "display_name": "Teacher"
                        },
                        {
                            "display_name": "Student"
                        }
                    ]
                }
            }
        ]
    }
}
```

> Failure response:

> If ...

```http
```
