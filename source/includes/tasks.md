# Task

## Fetch Status

```shell
curl --location --request GET 'https://api.polymersearch.com/v1/tasks/610805441afac351d4f2f2ad' \
--header 'accept: application/json, text/plain, */*' \
--header 'x-api-key: {{apikey}}'
```

> The above command returns JSON structured like this:

```json
{
    "user_id": "644b656f5279d0d125043fdf",
    "status": "Done",
    "type": "dataset_upload",
    "created_at": "2023-07-20T06:42:16.893Z",
    "updated_at": "2023-07-20T06:42:17.482Z",
    "data": {
        "message": "file processing done",
        "launch_url": "https://app.polymersearch.com/polymer/data/64b8d748c9afb894d91cfe83",
        "embed_code": "<iframe height=\"1200\" scrolling=\"no\" src=\"https://app.polymersearch.com/polymer/data/64b8d748c9afb894d91cfe83\" style=\"overflow:hidden;height:100%;width:100%;position:absolute;top:0;left:0;right:0;bottom:0\" width=\"100%\"></iframe>",
        "success": true,
        "file_id": "64b8d748c9afb894d91cfe83"
    },
    "id": "64b8d748c9afb849f81cfe80"
}
```

### HTTP Request

`GET https://api.polymersearch.com/v1/tasks/:id`

### Body content

Field | Datatype | Description
--------- | ------- | -----------
status | String | If set to 'Done' then task is executed and you can find response in data key
data.success | Boolean | If true then dataset was processed successfully and launch URL (data.launch_url) is ready
data.launch_url | String | launch URL (data.launch_url), only if data.success is true
data.embed_code | String | Embed Code (data.embed_code), only if data.success is true
data.errors | List | List of errors, only if data.success is false