# Dataset

The Dataset API allows the creation of new Polymer sites from your CSV files.


## Upload a Dataset

This endpoint starts processing provided CSV.

```shell
curl --location --request POST 'https://api.polymersearch.com/v1/dataset' \
--header 'x-api-key: XXd5c7f6-XXf9-4320-XX4d-5673d8XXd5bb' \
--header 'Content-Type: application/json' \
--data-raw '{
    "url": "https://abcc.s3.amazonaws.com/myfile.csv",
    "name": "Payment yearly.csv",
    "starting_row": 10,
    "update": true
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

```shell
curl --location --request POST 'https://api.polymersearch.com/v1/dataset' \
--header 'x-api-key: XXd5c7f6-feXX-43XX-XX4d-5673d8f0d5XX' \
--form 'name="Payment yearly 2022 920.csv"' \
--form 'file=@"/local_file_path/file_name.csv"'
```

> The above command returns JSON structured like this:

```json
{
    "message": "file processing done",
    "success": true,
    "file_id": "6409b295e0eb635a29d8c8f7"
}
```

### HTTP Request

`POST https://api.polymersearch.com/v1/dataset`

### Body content

Field | Mandatory | Description
--------- | ------- | -----------
url | false | URL to a valid public downloadable CSV.
file | false | Type: file. The file to upload.
name | true | Name of the dataset/file.
starting_row | false | Desired row number where Polymer should start processing your file.
update | false | Boolean. Force update dataset in case a dataset already exists with the given name.

Note: Either 'url' or 'file' parameter is required.

## Update a Dataset

This endpoint updates the content and metadata of an existing dataset.

```shell
curl --location --request PUT 'https://api.polymersearch.com/v1/dataset/6151754dfad3627deeb8f84b' \
--header 'x-api-key: XXeca66c-21f3-XX39-b407-64e00c62XXXX' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "FB Ad List Q2 C-uploaded.csv",
    "url": "https://test-csv-datasets.s3.us-east-2.amazonaws.com/Test+-+Bank+Loans.csv"
}'
```


> The above command returns JSON structured like this:

```json
{
    "message": "file processing done",
    "success": true,
    "file_id": "6409b295e0eb635a29d8c8f7"
}
```

### HTTP Request

`PUT https://api.polymersearch.com/v1/dataset/:id`


### Params content

Field | Mandatory | Description
--------- | ------- | -----------
id | true | Dataset ID.

### Body content

Field | Mandatory | Description
--------- | ------- | -----------
url | false | URL to a valid public downloadable CSV.
file | false | Type: file. The file to upload.
name | false | Name of the dataset/file.
incremental_update | In case you are passing incremental updates only
primary_key | Yes if incremental_update = true | name of the column
