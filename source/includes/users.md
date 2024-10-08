# Users

## Fetch existing & invited workspace users

```shell
curl --location --request GET 'https://v3.polymersearch.com/api/v1/workspace/users' \
--header 'accept: application/json, text/plain, */*' \
--header 'x-api-key: {{apikey}}'
```

### HTTP Request

`GET https://v3.polymersearch.com/api/v1/workspace/users`

> The above command returns JSON structured like this:

```json
{
    "data": [
        {
            "_id": "636e0856759be7e1f00cfa0f",
            "name": "Polymer Search",
            "email": "api-demo@polymersearch.com",
            "role": "Creator"
        },
        {
            "_id": "6389db43daeaa35b76482b14",
            "name": "Name User",
            "email": "user1@polymersearch.com",
            "role": "Editor"
        },
        {
            "_id": "638da37174ea61d5d9b9a6c7",
            "name": "Sam Title",
            "email": "user2@polymersearch.com",
            "role": "Read-only"
        },
        {
            "role": "Read-only",
            "_id": "63ec8c9a41f84c7d02ee344e",
            "email": "user3@polymersearch.com",
            "pending": true,
            "invitation_id": "63ec8c9a41f84c7d02ee344e"
        }
    ]
}
```



## Invite a new member to workspace

```shell
curl --location --request POST 'https://v3.polymersearch.com/api/v1/workspace/invite' \
--header 'accept: application/json, text/plain, */*' \
--header 'x-api-key: {{apikey}}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "members": [
        {
            "email": "user4@polymersearch.com",
            "role": "Read-only"
        }
    ]
}'
```

### HTTP Request

`POST https://v3.polymersearch.com/api/v1/workspace/invite`


> The above command returns JSON structured like this:

```json
{
    "success": true,
    "invited": true
}
```

### Body content

| Field                | Mandatory | Data Type | Description                                               |
|----------------------|-----------|-----------|-----------------------------------------------------------|
| members              | true      | List      | List of members to invite.                                 |
| members[].email      | true      | String    | A valid email ID.                                          |
| members[].role       | true      | String    | Valid values: `Editor`, `Read-only`.                       |
| skip_invite_email    | false     | Boolean   | If true, the invitation email will not be sent.            |




## Delete existing or invited workspace user

```shell
curl --location --request DELETE 'https://v3.polymersearch.com/api/v1/workspace/user/638da37174ea61d5d9b9a6c7' \
--header 'accept: application/json, text/plain, */*' \
--header 'x-api-key: {{apikey}}'
```

### HTTP Request

`DELETE https://v3.polymersearch.com/api/v1/workspace/user/:wuid`


> The above command returns JSON structured like this:

```json
{
    "message": "user deleted successfully"
}
```

### URL Params

Field | Mandatory | Description
--------- | ------- | -----------
wuid | true | Type: String<br /> _id field from '/v1/workspace/users' response