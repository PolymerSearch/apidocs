# Workspace

## Create a new workspace

```shell
curl --location --request POST 'https://v3.polymersearch.com/api/v1/workspace' \
--header 'accept: application/json, text/plain, */*' \
--header 'x-api-key: {{apikey}}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "My Workspace Name",
    "slug": "workspace-slug",
    "settings": {
        "disable_share_button": true
    }
}'
```

### HTTP Request

`POST https://v3.polymersearch.com/api/v1/workspace`


### Body content

| Field                                              | Mandatory | Data Type | Description                                                                                          |
|----------------------------------------------------|-----------|-----------|------------------------------------------------------------------------------------------------------|
| name                                               | true      | String    | Name of the workspace.                                                                               |
| slug                                               | true      | String    | Slug to be used in custom URLs. Alphanumeric characters, underscores, and dashes are allowed. It cannot end with an underscore or a dash. |
| settings.disable_share_button                      | false     | Boolean   | Set this flag to disable the share button on the board.    
| settings.disable_email_report                      | false     | Boolean   | Set this flag to disable the `Email Report` section in share section.                                               |
| settings.enable_polyai_in_read_only_permission     | false     | Boolean   | Set this flag to enable PolyAI on read-only permissions.                                              |
| notifications.board_digest_emails.disabled         | false     | Boolean   | Set this flag to disable all board digest emails.                                                     |
| notifications.board_digest_emails.enabled_by_default | false   | Boolean   | Set this flag to enable weekly digest emails on boards created.                                       |
| notifications.board_digest_emails.exclude_workspace_members | false | Boolean | Set this flag to send board digest emails only to the board owner.                                 |



## Get workspaces

```shell
curl --location --request GET 'https://v3.polymersearch.com/api/v1/workspaces' \
--header 'accept: application/json, text/plain, */*' \
--header 'x-api-key: {{apikey}}'
```

### HTTP Request

`GET https://v3.polymersearch.com/api/v1/workspaces`

> The above command returns JSON structured like this:

```json
{
    "data": [
        {
            "_id": "636e0856759be73b280cfa11",
            "slug": "api-demo",
            "name": "Polymer's Workspace",
            "default_name_unedited": true,
            "user_role": "Creator",
            "default": true,
            "members": [
                {
                    "_id": "636e0856759be7e1f00cfa0f",
                    "name": "Polymer Search",
                    "email": "member1@polymersearch.com"
                }
            ]
        },
        {
            "_id": "638850663e5ca0629efc34ed",
            "name": "Marketing",
            "slug": "polymer-marketing",
            "user_role": "Creator",
            "default": false,
            "settings": {
                "disable_share_button": false,
                "disable_email_report": true
            },
            "members": [
                {
                    "_id": "636e0856759be7e1f00cfa0f",
                    "name": "Polymer Search",
                    "email": "member1@polymersearch.com"
                },
                {
                    "_id": "638b60eb3dc9fa2645946403",
                    "name": "Remo",
                    "email": "member2@polymersearch.com"
                },
                {
                    "_id": "6390cdea9a51cd0743387a6e",
                    "name": "Ras",
                    "email": "member2@polymersearch.com"
                }
            ]
        }
    ]
}
```



## Edit workspace

```shell
curl --location --request PATCH 'https://v3.polymersearch.com/api/v1/workspace/64c25eae9797258e69dff54d' \
--header 'x-api-key: {{apikey}}' \
--header 'Content-Type: application/json' \
--data '{
    "name": "My Workspace Edited name",
    "settings": {
        "disable_share_button": true,
        "enable_polyai_in_read_only_permission": true
    }
}'
```

### HTTP Request

`PATCH https://v3.polymersearch.com/api/v1/workspace/:id`


### Body content

| Field                                              | Mandatory | Data Type | Description                                                                                          |
|----------------------------------------------------|-----------|-----------|------------------------------------------------------------------------------------------------------|
| name                                               | false     | String    | Name of the workspace.                                                                               |
| slug                                               | false     | String    | Slug to be used in custom URLs. Alphanumeric characters, underscores, and dashes are allowed. It cannot end with an underscore or a dash. |
| settings.disable_share_button                      | false     | Boolean   | Set this flag to disable the share button on the board.    
| settings.disable_email_report                      | false     | Boolean   | Set this flag to disable the `Email Report` section in share section.                                             |
| settings.enable_polyai_in_read_only_permission     | false     | Boolean   | Set this flag to enable PolyAI on read-only permissions.                                              |
| notifications.board_digest_emails.disabled         | false     | Boolean   | Set this flag to disable all board digest emails.                                                     |
| notifications.board_digest_emails.enabled_by_default | false   | Boolean   | Set this flag to enable weekly digest emails on boards created.                                       |
| notifications.board_digest_emails.exclude_workspace_members | false | Boolean | Set this flag to send board digest emails only to the board owner.                                    |



## Delete workspace

```shell
curl --location --request DELETE 'https://v3.polymersearch.com/api/v1/workspace/638da37174ea61d5d9b9a6c7' \
--header 'accept: application/json, text/plain, */*' \
--header 'x-api-key: {{apikey}}'
```

### HTTP Request

`DELETE https://v3.polymersearch.com/api/v1/workspace/:id`


> The above command returns JSON structured like this:

```json
{
    "success": true
}
```

### URL Params

Field | Mandatory | Description
--------- | ------- | -----------
id | true | Type: String<br /> _id field from '/v1/workspaces' response