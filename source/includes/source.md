# Source

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

## Snowflake - Sync Data (Manually)

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



## Connect a new Google BigQuery connector

```shell
curl --location --request POST 'https://v3.polymersearch.com/api/auth/googlebigquery/connection' \
--header 'accept: application/json, text/plain, */*' \
--header 'x-api-key: {{apikey}}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Prod Instance",
    "keyfilejson": {
        "type": "service_account",
        "project_id": "big-query-prod",
        "private_key_id": "XXe9cXX420ff6fb15XX8e8c182ebecb7XXd986XX",
        "private_key": "-----BEGIN PRIVATE KEY-----\nMIIEvQIXXDANBgkqhkiG9w0BAQEFAASCBKcwggSjAgEAAoIBAQDF5P97cajuuShb\nHYipN28BEmVb5/CTR2PspHcZjmMZagUz9CYY8eXlW27G+mPJP0NlP/SIeC4AnfV6XXXA0pnE6Sce9DquBDMGKA0ceisT8i6+DipZrLOwMS+TZhvKa73z7Lhm6QxzpeYfXV0\nXTDPZtyO6eK7UUSj1X+u6/1kSMPJfuGzJ4AP/KISeVyde+lCt/7CChfPzdlY5YfW\nuExA3xxqab8M9JPc+vK0S1aBpdJ+Q4ueczeVJRyb0bxR+zVREGSOLyjWcgvpT+xW\n1C4C52vvtRZ8YISvd29PFzuFxqNGVn9TwfQ98Cp6zo0gzFODtwzf7uaDk/bsNU7c\nQKqLtZ8LAgMBAAECggEAEJDAyiaTi5g4RphMTk3zntVZYr4hp1J8jNyfk6YVqZT0\nZorzfXcSVYa32TQwkjIXhCw8XgghYa/XUqVf3w0H5ImAzYUm8s7E6l72qSXsmaoZ\npCSSpzf/wCZisjt9CAV85eHPdtPiYMNvx5PdeB8WK2hssF13L3e5vnzGs1Rb/0vX\n8jDxZN4HOGm+kxQgQWpmb3ear4vtRot67QC0Ih3oZg71AWvjeTSZVXqGPF/a60HX\nwj7b7UceNNxop8JdRKm3AgmEH23en2kPUPCNlKD696cD5D3ffn8bs27ZL6Bv2k+T\nYe6rr9AdBn/gb5yUwzv8vjqxc+FEfMTtFmLcz5E5sQKBgQDy2L+pB2UvT9Gg7PKW\n/1XmpBZAbla5plvMxIVtiCKRSwPGlpPT5NxcoqdJ1h2s1igM2+AtPRMYXw5cxIaS\nCiSHmcFqTrvAKUqMYgN00tar9jSf5BgE4E/MVxcKbkCQ6fZnmVb417P36Xvuw2De\notB37sMOoKBVABDPE5HNGAbOPQKBgQDQnPQ5sMvlETFYuRcGaJc0frt2u2fHksVk\ncJIy3ZltigJuyQZ1oPKCj0R+lQkREo9EtKO89+Su18DIWkOXqAfInupUjuYT4ULA\XXRXUM8QrjmLiTMCO9eXXXv7KzQ0/3Ktg4gmsX14uUuHqFAOI/CV7KOPeYHc7v8X1a\nw70uiMX+5wKBgQDjOHrcJNdAFWcHM60oK3CshQts7dCnlEiAp8BQY/g0CgRWY72d\nnZ2x716nb3gEp7yBi5mNun+LZiWCFz/ylRro5axbU5XXXNoD0BF71WqXK57BnCH9\nLgR8JWChmdc/wCmVdZwy6WCyrfwPwXXX4IM796KEJprFd1tnjZ2QcikaT4QKBgE+Z\nxDsLMhH7CHhRT+7bE+8s+H0qr0Pgxj84ESElm3jHs3vwau2Rd1fIMRuX5LjF+zL9\nNolRkcoBe4c3ohkJPccYlFOlnzcwuhbBqhNBGqWTzcIkGU8g+xv6DccHRUkL6StO\n4Gxdi944sk9z8eCZw7ioGhnKLf8yh2GN1O8fs2U7AoGAfgPaYo1dHKz2R39SB6iz\nMv48I+oREuMC/3lU3YXLmDgyl1zx5ZhoJGeJ8deqLeomW+rhK02G7XXIApuA5pcrh\nl+R7N0jd/J1byQvcO+wXXXX6rvmF+UoDzdpzd9cCorj/WCVKysk60D8m1mukD4Gi\nbfgX2aIe5N5NIkvZUh7b1v0=\n-----END PRIVATE KEY-----\n",
        "client_email": "account-1@big-query-test-X456XX.iam.gserviceaccount.com",
        "client_id": "1XX14060XX125196033XX",
        "auth_uri": "https://accounts.google.com/o/oauth2/auth",
        "token_uri": "https://oauth2.googleapis.com/token",
        "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
        "client_x509_cert_url": "https://www.googleapis.com/robot/v1/metadata/x509/tXXXcount-1%40big-quXXy-teXX-4456XX.iam.gserviceaccount.com",
        "universe_domain": "googleapis.com"
    }
}'
```

### HTTP Request

`POST https://v3.polymersearch.com/api/auth/googlebigquery/connection`


### Body content

| Field                                              | Mandatory | Data Type | Description                                                                                          |
|----------------------------------------------------|-----------|-----------|------------------------------------------------------------------------------------------------------|
| name                                               | true      | String    | Desired name of the connector.     
| keyfilejson                                               | true      | String    | Key file JSON for service account.     


## Edit an Existing Google BigQuery connector

```shell
curl --location --request PATCH 'https://v3.polymersearch.com/api/auth/googlebigquery/:sourceid/connection' \
--header 'x-api-key: {{apikey}}' \
--header 'Content-Type: application/json' \
--data '{
    "name": "Staging Instance",
    "keyfilejson": {
        "type": "service_account",
        "project_id": "big-query-prod",
        "private_key_id": "XXe9cXX420ff6fb15XX8e8c182ebecb7XXd986XX",
        "private_key": "-----BEGIN PRIVATE KEY-----\nMIIEvQIXXDANBgkqhkiG9w0BAQEFAASCBKcwggSjAgEAAoIBAQDF5P97cajuuShb\nHYipN28BEmVb5/CTR2PspHcZjmMZagUz9CYY8eXlW27G+mPJP0NlP/SIeC4AnfV6XXXA0pnE6Sce9DquBDMGKA0ceisT8i6+DipZrLOwMS+TZhvKa73z7Lhm6QxzpeYfXV0\nXTDPZtyO6eK7UUSj1X+u6/1kSMPJfuGzJ4AP/KISeVyde+lCt/7CChfPzdlY5YfW\nuExA3xxqab8M9JPc+vK0S1aBpdJ+Q4ueczeVJRyb0bxR+zVREGSOLyjWcgvpT+xW\n1C4C52vvtRZ8YISvd29PFzuFxqNGVn9TwfQ98Cp6zo0gzFODtwzf7uaDk/bsNU7c\nQKqLtZ8LAgMBAAECggEAEJDAyiaTi5g4RphMTk3zntVZYr4hp1J8jNyfk6YVqZT0\nZorzfXcSVYa32TQwkjIXhCw8XgghYa/XUqVf3w0H5ImAzYUm8s7E6l72qSXsmaoZ\npCSSpzf/wCZisjt9CAV85eHPdtPiYMNvx5PdeB8WK2hssF13L3e5vnzGs1Rb/0vX\n8jDxZN4HOGm+kxQgQWpmb3ear4vtRot67QC0Ih3oZg71AWvjeTSZVXqGPF/a60HX\nwj7b7UceNNxop8JdRKm3AgmEH23en2kPUPCNlKD696cD5D3ffn8bs27ZL6Bv2k+T\nYe6rr9AdBn/gb5yUwzv8vjqxc+FEfMTtFmLcz5E5sQKBgQDy2L+pB2UvT9Gg7PKW\n/1XmpBZAbla5plvMxIVtiCKRSwPGlpPT5NxcoqdJ1h2s1igM2+AtPRMYXw5cxIaS\nCiSHmcFqTrvAKUqMYgN00tar9jSf5BgE4E/MVxcKbkCQ6fZnmVb417P36Xvuw2De\notB37sMOoKBVABDPE5HNGAbOPQKBgQDQnPQ5sMvlETFYuRcGaJc0frt2u2fHksVk\ncJIy3ZltigJuyQZ1oPKCj0R+lQkREo9EtKO89+Su18DIWkOXqAfInupUjuYT4ULA\XXRXUM8QrjmLiTMCO9eXXXv7KzQ0/3Ktg4gmsX14uUuHqFAOI/CV7KOPeYHc7v8X1a\nw70uiMX+5wKBgQDjOHrcJNdAFWcHM60oK3CshQts7dCnlEiAp8BQY/g0CgRWY72d\nnZ2x716nb3gEp7yBi5mNun+LZiWCFz/ylRro5axbU5XXXNoD0BF71WqXK57BnCH9\nLgR8JWChmdc/wCmVdZwy6WCyrfwPwXXX4IM796KEJprFd1tnjZ2QcikaT4QKBgE+Z\nxDsLMhH7CHhRT+7bE+8s+H0qr0Pgxj84ESElm3jHs3vwau2Rd1fIMRuX5LjF+zL9\nNolRkcoBe4c3ohkJPccYlFOlnzcwuhbBqhNBGqWTzcIkGU8g+xv6DccHRUkL6StO\n4Gxdi944sk9z8eCZw7ioGhnKLf8yh2GN1O8fs2U7AoGAfgPaYo1dHKz2R39SB6iz\nMv48I+oREuMC/3lU3YXLmDgyl1zx5ZhoJGeJ8deqLeomW+rhK02G7XXIApuA5pcrh\nl+R7N0jd/J1byQvcO+wXXXX6rvmF+UoDzdpzd9cCorj/WCVKysk60D8m1mukD4Gi\nbfgX2aIe5N5NIkvZUh7b1v0=\n-----END PRIVATE KEY-----\n",
        "client_email": "account-1@big-query-test-X456XX.iam.gserviceaccount.com",
        "client_id": "1XX14060XX125196033XX",
        "auth_uri": "https://accounts.google.com/o/oauth2/auth",
        "token_uri": "https://oauth2.googleapis.com/token",
        "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
        "client_x509_cert_url": "https://www.googleapis.com/robot/v1/metadata/x509/tXXXcount-1%40big-quXXy-teXX-4456XX.iam.gserviceaccount.com",
        "universe_domain": "googleapis.com"
    }
}'
```

### HTTP Request

`PATCH https://v3.polymersearch.com/api/auth/googlebigquery/:sourceid/connection`


### Body content

| Field                                              | Mandatory | Data Type | Description                                                                                          |
|----------------------------------------------------|-----------|-----------|------------------------------------------------------------------------------------------------------|
| name                                               | false      | String    | Desired name of the connector.     
| keyfilejson                                               | false      | String    | Key file JSON for service account.


## Import data using newly connected Google BigQuery

```shell
curl --location 'https://v3.polymersearch.com/api/googlebigquery/67861f640bd21e00099d0cc8' \
--header 'x-api-key: {{apikey}}' \
--header 'Content-Type: application/json' \
--data '{
    "name": "D-13-jan-2025-1",
    "query": "SELECT * FROM big-query-test-445609.dataset_test_1.table_test_1",
    "fetch_size": 100,
    "update_settings": {
        "type": "replace"
    }
}'
```

### HTTP Request

`POST https://v3.polymersearch.com/api/googlebigquery/:sourceid`

### Body content

| Field                                              | Mandatory | Data Type | Description                                                                                          |
|----------------------------------------------------|-----------|-----------|------------------------------------------------------------------------------------------------------|
| name                                               | true      | String    | Desired name of the imported dataset.     
| query                                               | true      | String    | Query to execute for data retrieval.
| fetch_size                                               | true      | String    | Maximum number of rows to fetch per pull.     
| update_settings                                               | true      | String    | Settings for data updates.
| update_settings.type                                              | true      | String    | Type of update: `replace`.

> The above command returns JSON structured like this:

```json
{
    "sync_id": "672b2e74a8de3b2585aa9154"
}
```

## Google BigQuery - Sync Data (Manually)

```shell
curl --location 'https://v3.polymersearch.com/api/googlebigquery/sync' \
--header 'x-api-key: {{apikey}}' \
--header 'Content-Type: application/json' \
--data '{
    "source_id": "671a1e74a8de3b2575aa9053",
    "file_id": "671b644ebdcabe4bdd1282b6",
    "full_sync": true
}'
```

### HTTP Request

`POST https://v3.polymersearch.com/api/googlebigquery/sync`

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
