# Dataset

The Dataset API allows the creation of new Polymer sites from your CSV files.


## Upload a Dataset

This endpoint initiates the processing of the provided CSV file.

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
url | false | URL to a valid publicly downloadable CSV.
file | false | Type: file. The file to upload.
name | true | Name of the dataset/file.
description | false | Description of the dataset/file.
starting_row | false | Desired row number where Polymer should start processing your file.
update | false | Boolean. Force update dataset in case a dataset already exists with the given name.

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


```shell
curl --location --request PUT 'https://v3.polymersearch.com/api/v1/dataset/6151754dfad3627deeb8f84b' \
--header 'x-api-key: XXeca66c-21f3-XX39-b407-64e00c62XXXX' \
--header 'Content-Type: application/json' \
--data-raw '{
    "url": "https://test-csv-datasets.s3.us-east-2.amazonaws.com/Test+-+Bank+Loans.csv",
    "incremental_update": true,
    "primary_key": "column1"
}'
```


```shell
curl --location --request PUT 'https://v3.polymersearch.com/api/v1/dataset/6151754dfad3627deeb8f84b' \
--header 'x-api-key: XXeca66c-21f3-XX39-b407-64e00c62XXXX' \
--header 'Content-Type: application/json' \
--data-raw '{
    "ingestion_type": "json",
    "delete": true,
    "primary_key": "column1",
    "records": [
        {
            "column1": "ID100"
        }
    ]
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
url | false | URL to a valid publicly downloadable CSV.
file | false | Type: file. The file to upload.
name | false | Name of the dataset/file.
description | false | Description of the dataset/file.
incremental_update | false | Indicates if the data being passed is for incremental updates only.
delete | false | Indicates if the data being passed contains row IDs to delete.
primary_key | false | if incremental_update = true or delete = true | name of the primary key column


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
        "description": "For Report 1",
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
limit | false | Maximum number of records per page.
page | false | Page number to retrieve.
sort_key | false | name, created_at, num_rows
sort_order | false | Allowed values: `desc`, `asc`.


## Create a merged dataset

This endpoint creates a merged dataset with given definition

```shell
curl --location 'https://v3.polymersearch.com/api/v1/datasets/merged' \
--header 'x-api-key: XXeca66c-21f3-XX39-b407-64e00c62XXXX' \
--header 'Content-Type: application/json' \
--data '{
    "name": "Merged dataset name here",
    "original_file_id": "66bcaafdde015d4d43494a45",
    "relations": [
        {
            "left_file_column": "r__opportunitystage",
            "file_id": "66bcaafdde015d4d43494a41",
            "right_file_column": "cp__oppstageid",
            "columns": [
                "cp__oppstageid"
            ],
            "prefix": "opportunitystage"
        },
        {
            "left_file_column": "r__company",
            "file_id": "66bcaafdde015d4d43494a68",
            "right_file_column": "cp__companyid",
            "columns": [
                "a__companyname",
                "a__companyowner",
                "a__companystate"
            ]
        },
        {
            "left_file_column": "cp__oppid",
            "file_id": "66bcaafdde015d4d43494a49",
            "right_file_column": "r__opportunity",
            "columns": '*'
        },
        {
            "left_file_id": "66bcaafdde015d4d43494a49",
            "left_file_column": "r__person",
            "file_id": "66bcaafdde015d4d43494a44",
            "right_file_column": "cp__personid",
            "columns": [
                "a__personcountry",
                "a__personname"
            ]
        }
    ],
    "columns": [
        "l__opppipelineid__opppipelinename",
        "a__oppsource",
        "d__oppcreatedat",
        "f__oppusdvalue",
        "f__oppvalue",
        "r__lead"
    ],
    "cadence_in_minutes": 5
}'
```


> The above command returns JSON structured like this:

```json
{
    "task_id": "65c3249d63a20b6727a11127"
}
```

### HTTP Request

`POST https://v3.polymersearch.com/api/v1/datasets/merged`

### Body content

Field | Mandatory | Description
--------- | ------- | -----------
name | true | Must be a string with a minimum length of 3 characters and a maximum of 80 characters. Represents the name of the dataset.
description | false | A string providing a description of the dataset.
original_file_id | true | Dataset ID of the main file
relations | true | An array of relation objects. Each object must contain `left_file_column`, `file_id`, `right_file_column`, and either a string or an array of `columns`.
relations.left_file_id | false | The ID of the left file in the relation
relations.left_file_column | true | The column from the left file that will be used in the relation.
relations.file_id | true | The ID of the left file in the relation
relations.right_file_column | true | The column from the right file that will be used in the relation.
relations.columns | true | Either a string ('*') to represent all columns, or an array of strings representing the specific columns to be used. Columns must be unique.
relations.prefix | true | A string that only contains alphabetic characters. It acts as a prefix for related columns.
columns | true | Either a string * representing all columns, or an array of unique strings specifying the columns to be included in the result.
cadence_in_minutes | true | An integer value representing the cadence in minutes, which must be at least 1.
