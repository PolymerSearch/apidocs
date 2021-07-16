# Dataset API

The Dataset API allows creating new PolymerSearch sites from your CSV.


## Upload a Dataset

This endpoint starts processing of provided CSV.

```shell
curl --location --request POST 'http://api.polymersearch.com/dataset' \
--header 'x-api-key: c5c498f8-1005-4274-acfb-0ab04a0e10fe' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'url=https://abcc.s3.amazonaws.com/myfile.csv' \
--data-urlencode 'name=Payments.csv'
```

> The above command returns JSON structured like this:

```json
{
    "message": "file processing done",
    "launch_url": "https://app.polymersearch.com/polymer/data/60f1334a7a6fa55bf5cdd268",
    "embed_code": "<iframe height=\"1200\" scrolling=\"no\" src=\"https://app.polymersearch.com/polymer/data/60f1334a7a6fa55bf5cdd268\" style=\"overflow:hidden;height:100%;width:100%;position:absolute;top:0;left:0;right:0;bottom:0\" width=\"100%\"></iframe>",
    "task_id": "60f133497a6fa5b4c6cdd265"
}
```

### HTTP Request

`POST http://api.polymersearch.com/dataset`

### Body content

Field | Mandatory | Description
--------- | ------- | -----------
url | true | URL to a valid public downloadable CSV.
name | true | Name of the dataset/file.
sharing | false | Desired sharing status for the dataset (public | password-protected | private). Defaults to private.
password | false | Required only in case of sharing: password-protected, Validation: min 6 characters.


