# App_Embed

Polymer generated app can be embed to create new boards (views), and browse/edit existing ones:


## Generate an auth token


This endpoint generates token to give authenticated access to embeded apps:

> Request

```shell
curl --location 'https://v3.polymersearch.com/v1/auth/token?access_level=workspace_edit' \
--header 'x-api-key: XXd5c7f6-XXf9-4320-XX4d-5673d8XXd5bb' \
--header 'workspace-id: 64XX73dd2221f86XXbc934XX'
```
> Note: workspace-id header is optional and only needed when you want to generate auth-token for a specific workspace which is different than default workspace defined with APIKEY

> The above command returns JSON structured like this:

```json
{
    "token": "XXXX72f4-df9c-XX6e-92XX-XXX09f41XX",
    "expires_at": "2023-07-20T12:15:40.741Z"
}
```





> As soon as you have the auth token, you can pass this token to embed URL/src. 

`https://app.polymersearch.com/b/${board_id}?ptoken={token}`