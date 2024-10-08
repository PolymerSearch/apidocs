# Embed

A Polymer-generated app can be embedded to create new boards and to browse or edit existing ones.



## Generate an auth token

This endpoint generates a token to provide authenticated access to embedded apps:

### HTTP Request

`GET https://v3.polymersearch.com/api/v1/auth/token?access_level=${permission_level}`

### Query string

Field | Mandatory | Description
--------- | ------- | -----------
permission_level | true | board_read_only: Grants permission to read data from the specified board ID.<br /><br /> board_edit: Grants permission to read and edit data from the specified board ID.<br /><br /> workspace_read_only: Authorizes read-only access to all board data within the workspace.<br /><br /> workspace_edit: Grant permission for reading, adding, and editing all board data within the workspace.<br /><br />block_level_read_only: Grants permission to read, add, and edit all board data within the workspace.
board_id | false | Grants permission to read data from the specified block on the board.


> Request

```shell
curl --location 'https://v3.polymersearch.com/api/v1/auth/token?access_level=workspace_edit' \
--header 'x-api-key: XXd5c7f6-XXf9-4320-XX4d-5673d8XXd5bb' \
--header 'workspace-id: 64XX73dd2221f86XXbc934XX'
```

### Note: workspace-id header is optional and only needed when you want to generate auth-token for a specific workspace which is different than default workspace defined with APIKEY

> The above command returns JSON structured like this:

```json
{
    "token": "XXXX72f4-df9c-XX6e-92XX-XXX09f41XX",
    "expires_at": "2023-07-20T12:15:40.741Z"
}
```

## Generating an embed URL using an authentication token

`https://v3.polymersearch.com/b/${board_id}?ptoken={token}`