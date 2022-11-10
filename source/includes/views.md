# Views API

With views API you can create beautiful charts without creating the full Polymer app. Embed in your site a manually selected chart for your data, or let our powerful AI determine what are the best charts for your data.

## Create View

> Example 1: Create basic view with all non AI charts

```shell
curl --location --request POST 'https://api.polymersearch.com/v1/datasets/6278c1c221fb918ae401c228/view' \
--header 'x-api-key: {{apikey}}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "My View Name",
    "charts": [
        {
            "type": "pie",
            "x_axis": "payment_mechanism",
            "slice": "Submission Date",
            "calculation": "sum"
        },
        {
            "type": "bar",
            "x_axis": "Fee Month",
            "y_axis": "amount",
            "slice": "Submission Date",
            "calculation": "average"
        }
    ]
}'
```

> Example 2: Create basic view with all AI charts

```shell
curl --location --request POST 'https://api.polymersearch.com/v1/datasets/6278c1c221fb918ae401c228/view' \
--header 'x-api-key: {{apikey}}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "AI view",
    "charts": [
        {
            "type": "ai"
        },
        {
            "type": "ai"
        },
        {
            "type": "ai"
        }
    ]
}'
```

> Example 3: Create basic view with all AI and non AI charts

```shell
curl --location --request POST 'https://api.polymersearch.com/v1/datasets/6278c1c221fb918ae401c228/view' \
--header 'x-api-key: {{apikey}}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "AI View",
    "charts": [
        {   
            "type": "heatmap",
            "x_axis": "Fee Month",
            "y_axis": "amount",
            "calculation": "max"
        },
        {
            "type": "ai"
        },
        {
            "type": "ai"
        },
        {
            "type": "ai"
        }
    ]
}'
```


> The above command returns JSON structured like this:

```json
{
    "launch_url": "https://app.polymersearch.com/views/e793422c-71bf-4043-8363-5e5a4f551fc1",
    "uid": "e793422c-71bf-4043-8363-5e5a4f551fc1"
}
```

### HTTP Request

`POST https://api.polymersearch.com/v1/datasets/:id/view`

### URL Params

Field | Mandatory | Description
--------- | ------- | -----------
id | true | Type: String<br />Dataset ID


### Body content

Field | Mandatory | Description
--------- | ------- | -----------
name | true | Type: String<br />Name of the view
charts | true | Type: List [Chart Object] <br />
sharing | false | Desired sharing status for the dataset (public, private, password-protected). Default: private
password | false | Required only in case of sharing: password-protected, Validation: min 6 characters.

### Chart Object

### Field: type
Mandatory: true

Allowed values:

- bar 
- column
- scatter 
- timeseries
- heatmap
- lineplot
- pie
- dependencywheel
- rich-text-insight
- ai 

<br >


### Field: x_axis 
Mandatory
`if type in ai or rich-text-insight then not allowed 
if type is dependencywheel
then not required for other types it is required`

Allowed values: valid column name
<br >


### Field: y_axis
Mandatory
`if type in ai or rich-text-insight then not allowed
if type is pie then not required 
for other types it is required`

Allowed values: valid column name
<br >


### Field: slice
Mandatory
`if type in ai or rich-text-insight then not allowed
for other types it is not required`

Allowed values: valid column name
<br >


### Field: filters
Mandatory
`if type in ai or rich-text-insight then not allowed
for other types it is not required`

 
Allowed values: object

Following filters can be applied

- Filter date columns with dynamic date range like last 30 days, last year etc
- Filter numerical columns with ranges like amount between 25 to 45.
- Text search in categorical columns like payment mechanism including cash and demand draft.
- Text search in categorical columns like payment mechanism excluding cash

Example payload
`
{
    "Submission Date": [
    {
        "value": "last 30 days"
    }],
    "amount": [
    {
        "value": [
            10,
            20
        ]
    }],
    "Payment Mechanism": [
    {
        "value": "cash",
        "operation": "INCLUDING"
    }]
}
`

Following filter will be read as 

`Submission Date within last 30 days 
AND 
amount between range 10 to 20 
AND
Payment Mechanism INCLUDING cash`

Possible dynamic date ranges:

- last day
- last 7 days
- last 30 days
- last 90 days
- last 6 months
- last 12 months


Possible operations:

- INCLUDING
- EXCLUDING

<br>


### Field: calculation
Mandatory

`if type in ai or rich-text-insight then not allowed
for other types it is required`

Allowed values:

- count 
- sum
- average
- stddev
- variance
- max
- min 

<br>

### Field: width 
Mandatory: False

Allowed values:

- one-third 
- two-thirds
- full

Default value: full
<br>


### Field: html 
`if type is rich-text-insight then required
> for other types it is not allowed`

<br>


## Edit View

> Example 1: Edit view with all non AI charts

```shell
curl --location --request PUT 'https://api.polymersearch.com/v1/datasets/views/dc2507ac-5e5d-456f-897f-e8ae23544b59' \
--header 'x-api-key: {{apikey}}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "charts": [
        {
            "type": "timeseries",
            "x_axis": "payment_mechanism",
            "y_axis": "Submission Date",
            "slice": "amount",
            "calculation": "sum"
        },
        {
            "type": "bar",
            "x_axis": "Fee Month",
            "y_axis": "amount",
            "slice": "Submission Date",
            "calculation": "min"
        }
    ]
}'
```

> Example 2: Edit view with all non AI charts and name

```shell
curl --location --request PUT 'https://api.polymersearch.com/v1/datasets/views/dc2507ac-5e5d-456f-897f-e8ae23544b59' \
--header 'x-api-key: {{apikey}}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Edited View Name",
    "charts": [
        {
            "type": "bar",
            "x_axis": "payment_mechanism",
            "y_axis": "Submission Date",
            "slice": "amount",
            "calculation": "sum"
        },
        {
            "type": "bar",
            "x_axis": "Fee Month",
            "y_axis": "amount",
            "slice": "Submission Date",
            "calculation": "min"
        }
    ]
}'
```

> The above command returns JSON structured like this:

```json
{
    "launch_url": "https://app.polymersearch.com/views/dc2507ac-5e5d-456f-897f-e8ae23544b59",
    "uid": "dc2507ac-5e5d-456f-897f-e8ae23544b59"
}
```

### HTTP Request

`PUT https://api.polymersearch.com/v1/datasets/views/:view_uid`

### URL Params

Field | Mandatory | Description
--------- | ------- | -----------
view_uid | true | Type: String<br />View UID


### Body content

Field | Mandatory | Description
--------- | ------- | -----------
name | false | Type: String<br />Name of the view
charts | false | Type: List [Chart Object] <br />
sharing | false | Desired sharing status for the dataset (public, private, password-protected). Default: private
password | false | Required only in case of sharing: password-protected, Validation: min 6 characters.

### Charts Object
Same as described on Create View request
Note: Make sure you pass all the charts inside `charts` key



## GET Views

> Response

```json
{
    "data": [
    {
        "uid": "40d4b950-78bb-4d6c-8b06-9fd20dbdf704",
        "name": "component test Group view 1 4",
        "sharing": "password-protected",
        "launch_url": "https://app.polymersearch.com/views/6278c1c221fb918ae401c228/40d4b950-78bb-4d6c-8b06-9fd20dbdf704",
        "file_id": "6278c1c221fb918ae401c228",
        "user_id": "61ee36cf2ac79ae07f539bcf",
        "created_at": "2022-09-13T10:35:28.349Z",
        "updated_at": "2022-09-13T10:54:02.214Z"
    },
    {
        "uid": "d85a90ec-ed66-432f-bdfa-488bf298ad7e",
        "name": "component test Group view 1 3",
        "sharing": "password-protected",
        "launch_url": "https://app.polymersearch.com/views/6278c1c221fb918ae401c228/d85a90ec-ed66-432f-bdfa-488bf298ad7e",
        "file_id": "6278c1c221fb918ae401c228",
        "user_id": "61ee36cf2ac79ae07f539bcf",
        "created_at": "2022-09-13T10:33:30.863Z",
        "updated_at": "2022-09-13T10:33:30.863Z"
    }],
    "limit": 10,
    "page": 1,
    "sort_key": "created_at",
    "sort_order": "desc"
}
```

### HTTP Request

`GET https://api.polymersearch.com/v1/datasets/views`



## DELETE View

> Response

```json
{
   "success": true
}
```

### HTTP Request

`DELETE https://api.polymersearch.com/v1/datasets/views/:view_uid`

### URL Params

Field | Mandatory | Description
--------- | ------- | -----------
view_uid | true | Type: String<br />View UID