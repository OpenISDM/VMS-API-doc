# Project

*This endpoints are unstable.*

## Create a project

```http
POST /api/project HTTP/1.1
Host: vms.app
Content-Type: application/json
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
Authorization: Bearer d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09

{
    "name": "Inspect earthquake hazard",
    "is_published": true,
    "permission": "public",
    "organization": "IES, Academia Sinica",
    "description": "The purpose of the project is for training volunteers.",
    "hyperlinks": [
        {
            id: 1
        },
        {
            id: 2
        }
    ]
}
```

> Successful response:

```http
HTTP/1.1 201 Created
Content-Type: application/json;charset=UTF-8

{
  "message": "The project was created.",
  "data": {
    "id": 1,
    "name": "Inspect earthquake hazard",
    "is_published": true,
    "permission": "public",
    "organization": "IES, Academia Sinica",
    "creator": {
      "id": 1,
      "username": "liang",
      "name": "Liang Wen Chung",
      "avatar": "http://avatar.vms.app/01a34d.jpg",
      "url": "http://vms.app/api/v1/users/1"
    },
    "description": "The purpose of the project is for training volunteers.",
    "hyperlinks": [
      {
        "id": 1,
        "name": "About us",
        "url": "http://ies.siinca.edu.tw/about-us"
      },
      {
        "id": 2,
        "name": "Training material",
        "url": "http://ies.siinca.edu.tw/slides/"
      }
    ]
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
            "field": ["is_published"],
            "code": "missing_field"
        }
    ]
}
```

> Failure response:

> If one of the hyperlinks don't exist, it will return the following response:

```http
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
    "message": "Link ids don't exist",
    "errors": [
        {
          "id": [1]
        }
    ]
}
```

### ATTRIBUTE

| Attribute | Type | Description |
|-----------|---------|-------------|
| name | String |   |
| is_published | boolean | Indicate the visibility of the project. The default value is `true`. |
| permission | String | The project's permission includes `public`, `private_for_user` and `private_for_member`. The default value is `public` |
| organization | String |  |
| description | String |  |
| hyperlinks | Array | The hyperlink ids. It is also a `array` type. |

## Get a specific project

```http
GET /projects/:id HTTP/1.1
Content-Type: application/json
Host: vms.app
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
Authorization: Bearer d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
````

> Successful response:

```http
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
    "data": {
      "id": 1,
      "name": "Inspect earthquake hazard",
      "is_published": true,
      "permission": "public",
      "organization": "IES, Academia Sinica",
      "creator": {
        "id": 1,
        "username": "liang",
        "name": "Liang Wen Chung",
        "avatar": "http://avatar.vms.app/01a34d.jpg",
        "url": "http://vms.app/api/v1/users/1"
      },
      "description": "The purpose of the project is for training volunteers.",
      "hyperlinks": [
        {
          "id": 1,
          "name": "About us",
          "url": "http://ies.siinca.edu.tw/about-us"
        },
        {
          "id": 2,
          "name": "Training material",
          "url": "http://ies.siinca.edu.tw/slides/"
        }
      ]
    }
}
```

> Failure response:

> If the id doesn't exist, it will return the following response:

```http
HTTP/1.1 404 Not Found
Content-Type: application/json;charset=UTF-8

{
    "message": "The project id doesn't exist",
    "errors": [
        {
            "code": "not_exist_project_id"
        }
    ]
}
```

### Response

| Attribute | type | Description |
|-----------|---------|-------------|
| id | integer |   |
| name | string |   |
| is_published | boolean | Indicate the visibility of the project  |
| permission | string | The project's permission includes `public`, `private_for_user` and `private_for_member` |
| organization | string |  |
| description | string |  |
| hyperlinks | array | The hyperlink data in array type includes `id`, `name` and `url` |


## Get all projects

```http
GET /projects HTTP/1.1
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
    "data": [
        {
            "id": 1,
            "name": "Inspect earthquake hazard",
            "is_published": true,
            "permission": "public",
            "organization": "IES, Academia Sinica",
            "creator": {
              "id": 1,
              "username": "liang",
              "name": "Liang Wen Chung",
              "avatar": "http://avatar.vms.app/01a34d.jpg",
              "url": "http://vms.app/api/v1/users/1"
            },
            "description": "The purpose of the project is for training volunteers.",
            "hyperlinks": [
              {
                "id": 1,
                "name": "About us",
                "url": "http://ies.siinca.edu.tw/about-us"
              },
              {
                "id": 2,
                "name": "Training material",
                "url": "http://ies.siinca.edu.tw/slides/"
              }
            ]
        },
        {
            "id": 2,
            "name": "Flood Survellience",
            "is_published": true,
            "permission": "public",
            "organization": "Water Resource Agency",
            "creator": {
              "id": 2,
              "username": "joehuang",
              "name": "Huang Joe",
              "avatar": "http://avatar.vms.app/0x123f.jpg",
              "url": "http://vms.app/api/v1/users/2"
            },
            "description": "Crowdsourcing for survellience surrounding flood issue.",
            "hyperlinks": [
              {
                "id": 4,
                "name": "Affected area map",
                "url": "http://water.tw/maps"
              },
              {
                "id": 6,
                "name": "Reporting platform",
                "url": "http://water.tw/platform"
              }
            ]
        }
    ]
}
```

## Get managed projects

```http
GET /manage-projects HTTP/1.1
Content-Type: application/json
Host: vms.app
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
Authorization: Bearer d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
````

> Successful response:

```http
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

[
    {
        "id": 1,
        "name": "Inspect earthquake hazard",
        "is_published": true,
        "permission": "public",
        "organization": "IES, Academia Sinica",
        "creator": {
          "id": 1,
          "username": "liang",
          "name": "Liang Wen Chung",
          "avatar": "http://avatar.vms.app/01a34d.jpg",
          "url": "http://vms.app/api/v1/users/1"
        },
        "description": "The purpose of the project is for training volunteers.",
        "hyperlinks": [
          {
            "id": 1,
            "name": "About us",
            "url": "http://ies.siinca.edu.tw/about-us"
          },
          {
            "id": 2,
            "name": "Training material",
            "url": "http://ies.siinca.edu.tw/slides/"
          }
        ]
    }
]
```

List all project managed by the authenticated user.

## Get attending projects

```http
GET /attending-projects HTTP/1.1
Content-Type: application/json
Host: vms.app
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
Authorization: Bearer d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
````

> Successful response:

```http
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

[
    {
        "id": 2,
        "name": "Flood Survellience",
        "is_published": true,
        "permission": "public",
        "organization": "Water Resource Agency",
        "creator": {
          "id": 2,
          "username": "joehuang",
          "name": "Huang Joe",
          "avatar": "http://avatar.vms.app/0x123f.jpg",
          "url": "http://vms.app/api/v1/users/2"
        },
        "description": "Crowdsourcing for survellience surrounding flood issue.",
        "links": [
          {
            "id": 4,
            "name": "Affected area map",
            "url": "http://water.tw/maps"
          },
          {
            "id": 6,
            "name": "Reporting platform",
            "url": "http://water.tw/platform"
          }
        ]
    }
]
```

List all project attending by the authenticated user.

## Update a project

```http
PUT /projects/:project_id HTTP/1.1
Content-Type: application/json
Host: vms.app
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
Authorization: Bearer d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09

{
    "name": "Inspect earthquake hazard",
    "is_published": true,
    "permission": "public",
    "organization": "IES, Academia Sinica",
    "description": "The purpose of the project is for training volunteers.",
    "links": [
      1,
      3
    ]
}
```

> Successful response:

```http
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
    "message": "The project was updated.",
    "data": {
      "id": 1,
      "name": "Inspect earthquake hazard",
      "is_published": true,
      "permission": "public",
      "organization": "IES, Academia Sinica",
      "creator": {
        "id": 1,
        "username": "liang",
        "name": "Liang Wen Chung",
        "avatar": "http://avatar.vms.app/01a34d.jpg",
        "url": "http://vms.app/api/v1/users/1"
      },
      "description": "The purpose of the project is for training volunteers.",
      "links": [
        {
          "id": 1,
          "name": "About us",
          "url": "http://ies.siinca.edu.tw/about-us"
        },
        {
          "id": 3,
          "name": "Instruction manual",
          "url": "http://ies.siinca.edu.tw/instruction/"
        }
      ]
    }
}
```

> Failure response:

> If the project id doesn't exist, it will return the following response:

```http
HTTP/1.1 404 Not Found
Content-Type: application/json;charset=UTF-8

{
    "message": "The project id doesn't exist",
    "errors": [
        {
            "code": "not_exist_project_id"
        }
    ]
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
            "field": ["is_published"],
            "code": "missing_field"
        }
    ]
}
```

Update the project managed by authenticated user.

### ATTRIBUTE

| Attribute | Type | Description |
|-----------|---------|-------------|
| name | String |   |
| is_published | boolean | Indicate the visibility of the project. The default value is `true`. |
| permission | String | The project's permission includes `public`, `private_for_user` and `private_for_member`. The default value is `public` |
| organization | String |  |
| description | String |  |
| hyperlinks | Array | The hyperlink ids. It is also a `array` type. |

## Delete a project

```http
DELETE /projects/:project_id HTTP/1.1
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
    "message": "Delete the project successfully"
}
```

> Failure response:

> If the project id doesn't exist, it will return the following response:

```http
HTTP/1.1 404 Not Found
Content-Type: application/json;charset=UTF-8

{
    "message": "The project id doesn't exist",
    "errors": [
        {
            "code": "not_exist_project_id"
        }
    ]
}
```
