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
import_from | false | Copy views & user config from an existing dataset. import_from.id would be source dataset ID from which you want to copy views or user config. import_from.data is an array with possible values views, user_config (one of them or both)