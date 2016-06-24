# Project Member

*This endpoints are unstable.*

## Attach a volunteer into a project

```http
PUT /projects/:id/members/:user_id HTTP/1.1
Host: vms.app
Content-Type: application/json
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
```

> Successful response:

```http
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
    "message": "Successfully attached a volunteer into a project",
    "data": {
        "state": "pending",
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
}
```

> Failure response:

> If the user already exist in the project, it will return the following response:

```http
HTTP/1.1 409 Conflict
Content-Type: application/json;charset=UTF-8

{
    "message": "Already exist in the project",
    "errors": [
        {
            "code": "already_exist_in_project"
        }
    ]
}
```

A project manager attaches a user into a project.

## Attend a project

```http
PUT /projects/:id/members HTTP/1.1
Host: vms.app
Content-Type: application/json
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
```

> Successful response:

```http
HTTP/1.1 204 No Content
Content-Type: application/json;charset=UTF-8
```

> Failure response:

> If the user already attended the project, it returns the following response:

```http
HTTP/1.1 409 Conflict
Content-Type: application/json;charset=UTF-8

{
    "message": "Already exist in the project",
    "errors": [
        {
            "code": "already_exist_in_project"
        }
    ]
}
```

A volunteer attends a project.

## Show members in a project
/**
 * @TODO
 */

## Dettach a project from a project

```http
DELETE /projects/:id/members/:userId HTTP/1.1
Host: vms.app
Content-Type: application/json
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
```

> Successful response:

```http
HTTP/1.1 204 No Content
Content-Type: application/json;charset=UTF-8
```

> Failure response:

> If the user doesn't exist in the project, it will return the following response:

```http
HTTP/1.1 404 Not Found
Content-Type: application/json;charset=UTF-8

{
    "message": "The user doesn't exist in the project",
    "errors": [
        {
            "code": "not_exist_in_project"
        }
    ]
}
```

A project manager dettach a volunteer from a project.

## Quit a project from a project

```http
DELETE /projects/:id/members HTTP/1.1
Host: vms.app
Content-Type: application/json
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
```

> Successful response:

```http
HTTP/1.1 204 No Content
Content-Type: application/json;charset=UTF-8
```

> Failure response:

> If the user doesn't exist in the project, it will return the following response:

```http
HTTP/1.1 404 Not Found
Content-Type: application/json;charset=UTF-8

{
    "message": "The user doesn't exist in the project",
    "errors": [
        {
            "code": "not_exist_in_project"
        }
    ]
}
```

A volunteer quits a project.
