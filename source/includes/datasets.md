# Dataset API

The Dataset API allows creating new PolymerSearch sites from your CSV.


## Upload a Dataset

This endpoint starts processing of provided CSV.

```shell
curl --location --request POST 'https://api.polymersearch.com/v1/dataset' \
--header 'x-api-key: XXd5c7f6-XXf9-4320-XX4d-5673d8XXd5bb' \
--header 'Content-Type: application/json' \
--data-raw '{
"url": "https://abcc.s3.amazonaws.com/myfile.csv",
"name": "Payment yearly.csv"
}'
```

```shell
curl --location --request POST 'https://api.polymersearch.com/v1/dataset' \
--header 'x-api-key: XXd5c7f6-feXX-43XX-XX4d-5673d8f0d5XX' \
--header 'Content-Type: application/json' \
--data-raw '{
    "url": "https://abcc.s3.amazonaws.com/myfile.csv",
    "name": "Payment yearly2.csv",
    "import_from": {
        "id": "6107ab93fa0ec85cb863f0e1",
        "data": [
            "views"
        ]
    }
}'
```

```shell
curl --location --request POST 'https://api.polymersearch.com/v1/dataset' \
--header 'x-api-key: XXd5c7f6-feXX-43XX-XX4d-5673d8f0d5XX' \
--header 'Content-Type: application/json' \
--data-raw '{
    "url": "https://abcc.s3.amazonaws.com/myfile.csv",
    "name": "Payment yearly3.csv",
    "import_from": {
        "id": "6107ab93fa0ec85cb863f0e1",
        "data": [
            "views","user_config"
        ]
    }
}'
```

> The above command returns JSON structured like this:

```json
{
    "task_id": "60f7bdd7c07d897637ac60f5"
}
```

### HTTP Request

`POST https://api.polymersearch.com/v1/dataset`

### Body content

Field | Mandatory | Description
--------- | ------- | -----------
url | true | URL to a valid public downloadable CSV.
name | true | Name of the dataset/file.
sharing | false | Desired sharing status for the dataset (public | password-protected | private). Defaults to private.
password | false | Required only in case of sharing: password-protected, Validation: min 6 characters.
import_from | false | Object for copy views & user config from an existing dataset (see below).
import_from.id | true | source dataset ID from which you want to copy views or user config.
import_from.data | true | Array containing views, user_config (one of them or both).