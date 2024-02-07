# Task

## Fetch Status

```shell
curl --location --request GET 'https://v3-api.polymersearch.com/v1/task/65c324f463a20b6727a1116b' \
--header 'accept: application/json, text/plain, */*' \
--header 'x-api-key: {{apikey}}'
```

> The above command returns JSON structured like this:

```json
{
    "file_id": "65c32d8334632067c1d32d18",
    "status": "inprogress"
}
```

```json
{
    "file_id": "65bc94d3cdb8f39435d3e21a",
    "status": "done"
}
```

```json
{
    "status": "done",
    "error": "An error has occurred (processing timeout). Our team is looking into it."
}
```


### HTTP Request

`GET https://v3-api.polymersearch.com/v1/task/:id`

### Body content

Field | Datatype | Description
--------- | ------- | -----------
status | String | If set to 'done' then task is executed and you can find file_id. If set to 'inprogress' please poll again in 5 seconds
error | String | if we encounter any processing error