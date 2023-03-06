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
    "id": "60f139c67168e50baf7c0d00",
    "user_id": "60990e185b2895737aa8841c",
    "status": "Done",
    "type": "dataset_upload",
    "created_at": "2021-07-16T07:48:22.435Z",
    "updated_at": "2021-07-16T07:51:32.692Z",
    "data":
    {
        "message": "file processing done",
        "success": true
    }
}
```

### HTTP Request

`GET https://api.polymersearch.com/v1/tasks/:id`

### Body content

Field | Datatype | Description
--------- | ------- | -----------
status | String | If set to 'Done' then task is executed and you can find response in data key
data.success | Boolean | If true then dataset was processed successfully
data.file_id | String | File ID
data.errors | List | List of errors, only if data.success is false