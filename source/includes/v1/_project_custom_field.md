# Project Custom Field

*This endpoints are unstable.*

## Custom field type format

### Text

> Text type

```json
{
    "name": "Which school?",
    "type": "text",
    "description": "Enter your school name",
    "required": true,
    "order": 1
}
```

### Radio button (Single choice)

> Radio button type

```json
{
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
```

## Create/update a custom field in a project

```http
POST /projects/:project_id/custom_fields HTTP/1.1
Host: vms.app
Content-Type: application/json
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
Authorization: Bearer d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09

{
    "name": "Which school?",
    "type": "text",
    "description": "Enter your school name",
    "required": true,
    "order": 1
}
```

> Successful response:

```http
HTTP/1.1 201 Created
Content-Type: application/json;charset=UTF-8

{
    "message": "The custom field was created successfully.",
    "data": {
        "id": 1,
        "name": "Which school?",
        "type": "text",
        "description": "Enter your school name",
        "required": true,
        "order": 1
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
            "field": ["type"],
            "code": "not_in_acceptable_list"
        }
    ]
}
```

ATTRIBUTE

| Attribute | Type | Description |
|-----------|---------|-------------|
| name | String | Custom field name |
| type | String  | Custom field type |
| description | String | Custom field description |
| required | boolean | Indicate the custom field is mandatory or optional |
| order | integer | The order of the custom field |
| metadata |  |  |

## Get all custom fields in a project

```http
GET /projects/:project_id/custom_fields HTTP/1.1
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
```

> Failure response:

> If the project id doesn't exist, it will return the following response:

```http
HTTP/1.1 404 Not Found
Content-Type: application/json;charset=UTF-8

{
    "status_code": 404,
    "message": "The project id doesn't exist",
    "errors": [
        {
            "code": "not_exist_project_id"
        }
    ]
}
```

List all custom field in a project

## Delete a custom field in a project

```http
DELETE /projects/:project_id/custom_fields/:custom_field_id HTTP/1.1
Host: vms.app
Content-Type: application/json
X-VMS-API-Key: d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09
Authorization: Bearer d6527aa8bcf55187490154283e4d2a1a268a94ead2322f883276a7c3cb52cd09

```

> Successful response:

```http
HTTP/1.1 204 No Content
Content-Type: application/json;charset=UTF-8
```

> Failure response:

> If the custom_field_id doesn't exist, it will return the following response:

```http
HTTP/1.1 404 Not Found
Content-Type: application/json;charset=UTF-8

{
    "status_code": 404,
    "message": "The custom_field_id id doesn't exist",
    "errors": [
        {
            "code": "not_exist_custom_field_id"
        }
    ]
}
```
