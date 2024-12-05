# Source

## Connect a new Snowflake connector

```shell
curl --location --request POST 'https://v3.polymersearch.com/api/auth/snowflake/connection' \
--header 'accept: application/json, text/plain, */*' \
--header 'x-api-key: {{apikey}}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Prod Instance",
    "account": "pjiigbt-tl75318",
    "username": "snowflake-username",
    "password": "snowflake-password"
}'
```

### HTTP Request

`POST https://v3.polymersearch.com/api/auth/snowflake/connection`


### Body content

| Field                                              | Mandatory | Data Type | Description                                                                                          |
|----------------------------------------------------|-----------|-----------|------------------------------------------------------------------------------------------------------|
| name                                               | true      | String    | Desired name of the connector.     
| account                                               | true      | String    | Account of the Snowflake instance.     
| username                                               | true      | String    | Username of the Snowflake instance.     
| password                                               | true      | String    | Password of the Snowflake instance.


## Get all connected sources

```shell
curl --location --request GET 'https://v3.polymersearch.com/api/v1/sources' \
--header 'accept: application/json, text/plain, */*' \
--header 'x-api-key: {{apikey}}'
```

### HTTP Request

`GET https://v3.polymersearch.com/api/v1/sources`

> The above command returns JSON structured like this:

```json
{
    "data": [
        {
            "_id": "671a1e74a8de3b2575aa9053",
            "type": "snowflake",
            "name": "Staging",
            "updated_at": "2024-10-28T07:25:42.693Z",
            "created_at": "2024-10-24T10:16:20.765Z"
        },
        {
            "_id": "671f403c3a1b4f32cd64d421",
            "type": "snowflake",
            "name": "Prod",
            "updated_at": "2024-10-28T07:41:48.090Z",
            "created_at": "2024-10-28T07:41:48.090Z"
        }
    ]
}
```


## Edit an Existing Snowflake connector

```shell
curl --location --request PATCH 'https://v3.polymersearch.com/api/auth/snowflake/:sourceid/connection' \
--header 'x-api-key: {{apikey}}' \
--header 'Content-Type: application/json' \
--data '{
    "name": "Staging Instance",
    "account": "pjiigbt-tl76209",
    "username": "snowflake-username",
    "password": "snowflake-password"
}'
```

### HTTP Request

`PATCH https://v3.polymersearch.com/api/auth/snowflake/:sourceid/connection`


### Body content

| Field                                              | Mandatory | Data Type | Description                                                                                          |
|----------------------------------------------------|-----------|-----------|------------------------------------------------------------------------------------------------------|
| name                                               | false      | String    | Desired name of the connector.     
| account                                               | false      | String    | Account of the Snowflake instance.     
| username                                               | false      | String    | Username of the Snowflake instance.     
| password                                               | false      | String    | Password of the Snowflake instance.                          |



## Delete an existing source

```shell
curl --location --request DELETE 'https://v3.polymersearch.com/api/v1/sources/:sourceid' \
--header 'accept: application/json, text/plain, */*' \
--header 'x-api-key: {{apikey}}'
```

### HTTP Request

`DELETE https://v3.polymersearch.com/api/v1/sources/:sourceid`


> The above command returns JSON structured like this:

```json
{
    "success": true
}
```

### URL Params

Field | Mandatory | Description
--------- | ------- | -----------
id | true | Type: String<br /> _id field from '/v1/sources' response


## Import data using newly connected Snowflake

```shell
curl --location 'https://v3.polymersearch.com/api/snowflake/671a1e74a8de3b2575aa9053' \
--header 'x-api-key: {{apikey}}' \
--header 'Content-Type: application/json' \
--data '{
    "name": "Orders",
    "query": "SELECT * FROM DB1.PUBLIC.ORDERS ",
    "table_name": "ORDERS",
    "fetch_size": 50,
    "schema_name": "PUBLIC",
    "update_settings": {
        "type": "merge",
        "update_at_column": {
            "name": "ORDER_DATE"
        },
        "merge_column_name": "ORDER_ID"
    }
}'
```

### HTTP Request

`POST https://v3.polymersearch.com/api/snowflake/:sourceid`

### Body content

| Field                                              | Mandatory | Data Type | Description                                                                                          |
|----------------------------------------------------|-----------|-----------|------------------------------------------------------------------------------------------------------|
| name                                               | true      | String    | Desired name of the imported dataset.     
| query                                               | true      | String    | Query to execute for data retrieval.
| fetch_size                                               | true      | String    | Maximum number of rows to fetch per pull.     
| update_settings                                               | true      | String    | Settings for data updates.
| update_settings.type                                              | true      | String    | Type of update: `replace`, `merge`, or `append`.
| update_settings.merge_column_name                                              | true      | String    | Column name for merging if type is set to merge.
| update_settings.update_at_column. name                                             | false      | String    | Column for tracking last pulled data; if provided, system fetches data only after the most recent record.


> The above command returns JSON structured like this:

```json
{
    "sync_id": "672b2e74a8de3b2585aa9154"
}
```

## Sync Data (Manually)

```shell
curl --location 'https://v3.polymersearch.com/api/snowflake/sync' \
--header 'x-api-key: {{apikey}}' \
--header 'Content-Type: application/json' \
--data '{
    "source_id": "671a1e74a8de3b2575aa9053",
    "file_id": "671b644ebdcabe4bdd1282b6",
    "full_sync": true
}'
```

### HTTP Request

`POST https://v3.polymersearch.com/api/snowflake/sync`

### Body content

| Field                                              | Mandatory | Data Type | Description                                                                                          |
|----------------------------------------------------|-----------|-----------|------------------------------------------------------------------------------------------------------|
| source_id                                               | true      | String    | Source ID of the dataset to sync.     
| file_id                                               | true      | String    | File ID of the dataset to sync
| full_sync                                               | false      | String    | This will override the update_settings provided with dataset and will fully refresh the data

> The above command returns JSON structured like this:

```json
{
    "sync_id": "672b2e74a8de3b2585aa9154"
}
```
