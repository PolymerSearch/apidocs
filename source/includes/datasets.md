# Dataset

The Dataset API allows the creation of new Polymer sites from your CSV files.


## Upload a Dataset

This endpoint starts processing provided CSV.

```shell
curl --location --request POST 'https://v3.polymersearch.com/api/v1/dataset' \
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
curl --location --request POST 'https://v3.polymersearch.com/api/v1/dataset' \
--header 'x-api-key: XXd5c7f6-feXX-43XX-XX4d-5673d8f0d5XX' \
--header 'Content-Type: application/json' \
--data-raw '{
    "url": "https://abcc.s3.amazonaws.com/myfile.csv",
    "name": "Payment yearly2.csv"
}'
```

```shell
curl --location --request POST 'https://v3.polymersearch.com/api/v1/dataset' \
--header 'x-api-key: XXd5c7f6-feXX-43XX-XX4d-5673d8f0d5XX' \
--header 'Content-Type: application/json' \
--data-raw '{
    "ingestion_type": "json",
    "name": "Payment yearly3.csv",
    "records": [
        {
            "ticket_id": "ID2",
            "created_at": "2022-10-21",
            "language": "Spanish",
            "number1": 14
        },{
            "ticket_id": "ID2",
            "created_at": "2022-10-21",
            "language": "Spanish",
            "number1": 14
        }
    ]
}'
```

```shell
curl --location --request POST 'https://v3.polymersearch.com/api/v1/dataset' \
--header 'x-api-key: XXd5c7f6-feXX-43XX-XX4d-5673d8f0d5XX' \
--form 'name="Payment yearly 2022 920.csv"' \
--form 'file=@"/local_file_path/file_name.csv"'
```

> The above command returns JSON structured like this:

```json
{
    "task_id": "65c3249d63a20b6727a11127"
}
```

### HTTP Request

`POST https://v3.polymersearch.com/api/v1/dataset`

### Body content

Field | Mandatory | Description
--------- | ------- | -----------
url | false | URL to a valid public downloadable CSV.
file | false | Type: file. The file to upload.
name | true | Name of the dataset/file.
starting_row | false | Desired row number where Polymer should start processing your file.
update | false | Boolean. Force update dataset in case a dataset already exists with the given name.
auto_generated_board | false | Boolean. Generate auto board

Note: Either 'url' or 'file' parameter is required.

## Update a Dataset

This endpoint updates the content and metadata of an existing dataset.

```shell
curl --location --request PUT 'https://v3.polymersearch.com/api/v1/dataset/6151754dfad3627deeb8f84b' \
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
    "task_id": "65c324f463a20b6727a1116b"
}
```

> The above command returns JSON structured like this:

```json
{
    "success": false,
    "errors": [
        {
            "message": "duplicate file name"
        }
    ]
}
```

### HTTP Request

`PUT https://v3.polymersearch.com/api/v1/dataset/:id`


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



## Fetch Datasets

This endpoint returns list of datasets

```shell
curl --location --request PUT 'https://v3.polymersearch.com/api/v1/dataset' \
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
    "data": [
    {
        "_id": "65d775c6428356ae03b21b1f",
        "user": "65d775a24283563f98b21a75",
        "user_email": "v3-api-demo@polymersearch.com",
        "name": "11_payment 624 CSV copy 1114.csv",
        "source_type": "upload",
        "workspace_id": "65d775a24283564ab4b21a81",
        "created_at": "2024-02-22T16:26:46.352Z",
        "extension": "csv",
        "num_rows": 59626,
        "status": "success",
        "id": "65d775c6428356ae03b21b1f"
    },
    {
        "_id": "65d778bc4283568b69b221ef",
        "user": "65d775a24283563f98b21a75",
        "user_email": "v3-api-demo@polymersearch.com",
        "name": "DS1",
        "source_type": "api",
        "workspace_id": "65d775a24283564ab4b21a81",
        "extension": "csv",
        "created_at": "2024-02-22T16:39:24.358Z",
        "num_rows": 5,
        "status": "success",
        "id": "65d778bc4283568b69b221ef"
    },
    {
        "_id": "65ddabc9428356050bb89426",
        "user": "65d775a24283563f98b21a75",
        "user_email": "v3-api-demo@polymersearch.com",
        "name": "File upload demo dataset",
        "source_type": "api",
        "workspace_id": "65d775a24283564ab4b21a81",
        "extension": "csv",
        "created_at": "2024-02-27T09:30:49.830Z",
        "num_rows": 5,
        "status": "success",
        "id": "65ddabc9428356050bb89426"
    }],
    "limit": 100,
    "page": 1,
    "sort_key": "name",
    "sort_order": "asc"
}
```


### HTTP Request

`GET https://v3.polymersearch.com/api/v1/dataset`


### Query string

Field | Mandatory | Description
--------- | ------- | -----------
limit | false | Page limit.
page | false | Page number.
sort_key | false | name, created_at, num_rows
sort_order | false | desc,asc
