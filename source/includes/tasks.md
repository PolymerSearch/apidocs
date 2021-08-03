# Task API

## Fetch Status

```shell
curl --location --request GET 'https://api.polymersearch.com/v1/tasks/610805441afac351d4f2f2ad' \
--header 'accept: application/json, text/plain, */*' \
--header 'x-api-key: {{apikey}}'
```

> The above command returns JSON structured like this:

```json
{
    "data":
    {
        "id": "60f139c67168e50baf7c0d00",
        "user_id": "60990e185b2895737aa8841c",
        "status": "Done",
        "type": "dataset_upload",
        "created_at": "2021-07-16T07:48:22.435Z",
        "updated_at": "2021-07-16T07:51:32.692Z",
        "data":
        {
            "message": "file processing done",
            "launch_url": "https://app.polymersearch.com/polymer/data/60f7bdd7c07d8900b5ac60f8",
            "embed_code": "<iframe height=\"1200\" scrolling=\"no\" src=\"https://app.polymersearch.com/polymer/data/60f7bdd7c07d8900b5ac60f8\" style=\"overflow:hidden;height:100%;width:100%;position:absolute;top:0;left:0;right:0;bottom:0\" width=\"100%\"></iframe>",
            "success": true
        }
    }
}
```

### HTTP Request

`GET https://api.polymersearch.com/v1/tasks/:id`

### Body content

Field | Datatype | Description
--------- | ------- | -----------
data.status | String | If set to 'Done' then task is executed and you can find response in data.data key
data.data.success | Boolean | If true then dataset was processed successfully and launch URL (data.data.launch_url) is ready
data.data.launch_url | String | launch URL (data.data.launch_url), only if data.data.success is true
data.data.embed_code | String | Embed Code (data.data.embed_code), only if data.data.success is true
data.errors | List | List of errors, only if data.data.success is false