# View

With views API you can create charts and data segments and share them with the world instead of exposing the complete Polymer site. Embed in your site a manually selected chart for your data, or let our powerful AI determine what are the best charts for your data.

## Create View

> Example 1: Create a basic view with all non-AI charts

```shell
curl --location --request POST 'https://api.polymersearch.com/v1/datasets/6278c1c221fb918ae401c228/view' \
--header 'x-api-key: {{apikey}}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "My View Name",
    "charts": [
    {
        "type": "pie",
        "x_axis_multiple": [
        {
            "name": "payment_mechanism"
        }]
        "slice": "Submission Date"
    },
    {
        "type": "bar",
        "x_axis": "Fee Month",
        "y_axis": "amount",
        "slice": "Submission Date",
        "operation": "AVERAGE"
    }]
}'
```

> Example 2: Create a basic view with all AI charts

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
    }]
}'
```

> Example 3: Create a basic view with all AI and non-AI charts

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
        "operation": "MAX"
    },
    {
        "type": "ai"
    },
    {
        "type": "ai"
    },
    {
        "type": "ai"
    }]
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

## Chart Object

### AI Chart
```json
{
    "type": "ai"
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes |ai
width | Boolean| No | Any value from one-third , two-thirds, full. Default: full



### Bar Chart
```json
{
    "type": "bar",
    "x_axis_multiple": [
    {
        "name": "spend",
        "operation": "SUM"
    },
    {
        "name": "Clicks (all)",
        "operation": "COUNT"
    }],
    "y_axis": "campaign_status",
    "operation": "SUM",
    "y_axis_log": true,
    "show_annotations": true,
    "show_stacked": false
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes |bar
x_axis |List | one of the x_axis or x_axis_multiple is required | valid column name
x_axis_multiple | List | one of the x_axis or x_axis_multiple is required | Object, Min length: 2, Max length: 10. <br > **name**: valid column <br > **operation**: Any value from COUNT, SUM, AVERAGE, STDDEV, VARIANCE, MAX, MIN
y_axis | String| Yes| valid column name
operation | String| No | Any value from COUNT, SUM, AVERAGE, STDDEV, VARIANCE, MAX, MIN
sort | Object | No | **type**: total (Total), raw (Raw Order), count (Count), value (x-axis tags) <br > **operation**: Any  value from asc, desc
slice | String| No| valid column name
show_annotations | Boolean| No | Annotate each segment by its value
show_stacked | Boolean| No | Show as stack. Default: true
is_percentage | Boolean| No | Show as percentage
y_axis_log | Boolean| No | Use logarithmic scale for Y-Axis
exclude_empty_string | Boolean| No | Exclude [EMPTY] strings. Default: true
width | Boolean| No | Any value from one-third , two-thirds, full. Default: full
filters | Object| No | Filter Object
title | String| No | Custom heading


### Column Chart
```json
{
    "type": "column",
    "x_axis": "campaign_status",
    "y_axis_multiple": [
    {
        "name": "spend",
        "operation": "SUM"
    },
    {
        "name": "Clicks (all)",
        "operation": "COUNT"
    }],
    "operation": "SUM",
    "show_annotations": true,
    "show_stacked": false
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String | Yes |column
x_axis | String| Yes| valid column name
y_axis | String | one of the y_axis or y_axis_multiple is required | valid column name
y_axis_multiple | List | one of the y_axis or y_axis_multiple is required | Object, Min length: 2, Max length: 10. <br > **name**: valid column <br > **operation**: Any value from COUNT, SUM, AVERAGE, STDDEV, VARIANCE, MAX, MIN
operation | String| No | Any value from COUNT, SUM, AVERAGE, STDDEV, VARIANCE, MAX, MIN
sort | Object | No | **type**: total (Total), raw (Raw Order), count (Count), value (x-axis tags) <br > **operation**: Any  value from asc, desc
slice | String| No| valid column name
show_annotations | Boolean| No | Annotate each segment by its value
show_stacked | Boolean| No | Show as stack. Default: true
is_percentage | Boolean| No | Show as percentage
x_axis_log | Boolean| No | Use logarithmic scale for X-Axis
exclude_empty_string | Boolean| No | Exclude [EMPTY] strings. Default: true
width | Boolean| No | Any value from one-third , two-thirds, full. Default: full
filters | Object| No | Filter Object
title | String| No | Custom heading


### SCATTER PLOT Chart
```json
{
    "type": "scatter",
    "x_axis": "spend",
    "y_axis": "cost_per_initiate_checkout",
    "operation": "SUM",
    "x_axis_log": true
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes |scatter
x_axis | String| Yes| valid column name
y_axis |String |Yes |valid column name
operation | String| Yes| Any value from COUNT, SUM, AVERAGE, STDDEV, VARIANCE, MAX, MIN
slice | String| No| valid column name
x_axis_log | Boolean| No | Use logarithmic scale for X-Axis
y_axis_log | Boolean| No | Use logarithmic scale for Y-Axis
exclude_empty_string | Boolean| No | Exclude [EMPTY] strings. Default: true
width | Boolean| No | Any value from one-third , two-thirds, full. Default: full
filters | Object| No | Filter Object
title | String| No | Custom heading


### TIMESERIES Chart
```json
{
    "type": "timeseries",
    "x_axis": "date",
    "operation": "SUM",
    "y_axis_log": true,
    "exclude_empty_string": false,
    "group_by": "quarter",
    "is_area": true
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes |timeseries
x_axis | String| Yes| valid column name
y_axis |String | No |valid column name
y_axis_multiple | List | No | Object, Min length: 2, Max length: 10. <br > **name**: valid column <br > **operation**: Any value from COUNT, SUM, AVERAGE, STDDEV, VARIANCE, MAX, MIN
operation | String| Yes| Any value from COUNT, SUM, AVERAGE, STDDEV, VARIANCE, MAX, MIN
slice | String| No| valid column name
is_area | Boolean| No | Use area chart
y_axis_log | Boolean| No | Use logarithmic scale for Y-Axis
exclude_empty_string | Boolean| No | Exclude [EMPTY] strings. Default: true
group_by | String| No | Any value from day, week, month, quarter, year
width | Boolean| No | Any value from one-third , two-thirds, full. Default: full
filters | Object| No | Filter Object
title | String| No | Custom heading


### HEATMAP Chart
```json
{
    "type": "heatmap",
    "y_axis": "account_currency",
    "operation": "SUM",
    "exclude_empty_string": false,
    "show_annotations": true
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes |heatmap
y_axis |String |Yes |valid column name
x_axis | String| No| valid column name
operation | String| Yes| Any value from COUNT, SUM, AVERAGE, STDDEV, VARIANCE, MAX, MIN
slice | String| No| valid column name
show_annotations | Boolean| No | Annotate each segment by its value
exclude_empty_string | Boolean| No | Exclude [EMPTY] strings. Default: true
width | Boolean| No | Any value from one-third , two-thirds, full. Default: full
filters | Object| No | Filter Object
title | String| No | Custom heading


### LINEPLOT Chart
```json
{
    "type": "lineplot",
    "x_axis": "spend",
    "y_axis": "link_click",
    "operation": "SUM"
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes |lineplot
y_axis |String | one of the y_axis or y_axis_multiple is required |valid column name
y_axis_multiple | List | one of the y_axis or y_axis_multiple is required | Object, Min length: 2, Max length: 10. <br > **name**: valid column <br > **operation**: Any value from COUNT, SUM, AVERAGE, STDDEV, VARIANCE, MAX, MIN
x_axis | String| Yes| valid column name
operation | String| Yes| Any value from COUNT, SUM, AVERAGE, STDDEV, VARIANCE, MAX, MIN
slice | String| No| valid column name
y_axis_log | Boolean| No | Use logarithmic scale for Y-Axis
exclude_empty_string | Boolean| No | Exclude [EMPTY] strings. Default: true
width | Boolean| No | Any value from one-third , two-thirds, full. Default: full
filters | Object| No | Filter Object
title | String| No | Custom heading


### PIE Chart
```json
{
    "type": "pie",
    "x_axis_multiple": [
    {
        "name": "status"
    }],
    "exclude_empty_string": false,
    "show_annotations": true
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes |pie
x_axis_multiple |List |Yes |Object, Min length: 1, Max length: 2. <br > **name**: valid column
y_axis_multiple |List |No |Object, Min length: 1, Max length: 1. <br > **name**: valid column <br > **operation**: Any value from COUNT, SUM, AVERAGE, STDDEV, VARIANCE, MAX, MIN
show_annotations | Boolean| No | Annotate each segment by its value
exclude_empty_string | Boolean| No | Exclude [EMPTY] strings. Default: true
width | Boolean| No | Any value from one-third , two-thirds, full. Default: full
filters | Object| No | Filter Object
title | String| No | Custom heading


### OUTLIERS
```json
{
    "type": "outliers",
    "metric": "spend",
    "operation": "COUNT",
    "exclude_empty_string": false,
    "influencing_columns": [
        "ad_name"
    ]
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes |outliers
metric |String |Yes |valid column name
operation | String| Yes| Any value from COUNT, SUM, AVERAGE, STDDEV, VARIANCE, MAX, MIN
influencing_columns |List |Yes |Influencing Columns - list of valid column names. Min length: 1, Max length: 6
results_type |String |No |Show results - Any value from count, below_average_only, above_average_only, top_and_bottom_outliers, above_and_below_average
show_results_column | Boolean| No | Show Results Column
exclude_empty_string | Boolean| No | Exclude [EMPTY] strings
width | Boolean| No | Any value from one-third , two-thirds, full. Default: full
filters | Object| No | Filter Object
title | String| No | Custom heading


### ROI CALCULATOR
```json
{
    "type": "roi",
    "max_metric": "impressions",
    "max_operation": "AVERAGE",
    "min_metric": "spend",
    "min_operation": "MAX",
    "influencing_columns": [
        "ad_name",
        "campaign_name"
    ],
    "show_results_column": false
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes |roi
max_metric |String |Yes |Metric to Maximize (Return) - valid column name
max_operation | String| Yes| Any value from COUNT, SUM, AVERAGE, STDDEV, VARIANCE, MAX, MIN
min_metric |String |Yes |Metric to Minimize (Investment) - valid column name
min_metric | String| Yes| Any value from COUNT, SUM, AVERAGE, STDDEV, VARIANCE, MAX, MIN
influencing_columns |List |Yes |Influencing Columns - list of valid column names. Min length: 1, Max length: 6
show_results_column | Boolean| No | Show Results Column
show_percentage | Boolean| No | Show ROI as Percentage
exclude_empty_string | Boolean| No | Exclude [EMPTY] strings
width | Boolean| No | Any value from one-third , two-thirds, full. Default: full
filters | Object| No | Filter Object
title | String| No | Custom heading


### PIVOT TABLE
```json
{
    "type": "pivot",
    "metrics": [
    {
        "metric": "spend",
        "operation": "SUM"
    }],
    "rows": [
        "account_currency"
    ],
    "columns": ["ad_name"]
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes |pivot
metrics |List |Yes |Object, Min length: 1, Max length: 10. <br > **metric**: valid column <br > **operation**: Any value from COUNT, SUM, AVERAGE, STDDEV, VARIANCE, MAX, MIN
rows |List |Yes |Rows - list of valid column names. Min length: 1, Max length: 1
columns |List |Yes |Columns - list of valid column names. Min length: 1, Max length: 1
show_row_totals | Boolean| No | Show Row Totals
show_column_totals | Boolean| No | Show Column Totals
show_percentage | Boolean| No | Show Percentage, Default: True
sort_by_row_tags | String| No | Sort rows by tag value. Any  value from ASC, DESC
column_manual_order | List| No | Sort columns by column tags. List of tag values
sort_by_counts |Object |No | **column_index**: index of the column given in columns <br > **metric_index**: index of the column given in metrics <br > **order**: Any  value from ASC, DESC
width | Boolean| No | Any value from one-third , two-thirds, full. Default: full
filters | Object| No | Filter Object
title | String| No | Custom heading


### KPI BLOCK
```json
{
    "type": "kpi",
    "metric": "impressions",
    "operation": "SUM",
    "date": "date",
    "date_range": "last 90 days",
    "goal": 4000000
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes |kpi
metric |List |Yes |valid column name
operation | String| Yes| Any value from COUNT, SUM, AVERAGE, STDDEV, VARIANCE, MAX, MIN
date | String| No| valid date column name
date_range | String| No| Any value from 'last day', 'last 7 days', 'last 14 days', 'last 30 days', 'last 90 days', 'last 6 months', 'last 12 months, 'this month', 'this week', 'last week', custom
date_range_custom | List| No| If date_range is selected as custom. [START_DATE_EPOCH_SECONDS, END_DATE_EPOCH_SECONDS]
comp_date_range | String| No| Any value from 'previous period', 'custom'
comp_date_range_custom | List| No| If comp_date_range is selected as custom. [START_DATE_EPOCH_SECONDS, END_DATE_EPOCH_SECONDS]
goal |Number |No |
exclude_empty_string | Boolean| No | Exclude [EMPTY] strings
width | Boolean| No | Any value from one-third , two-thirds, full. Default: full
filters | Object| No | Filter Object


### DATA TABLE
```json
{
    "type": "data-table",
    "columns": [
        "ticket_group"
    ],
    "values": [
    {
        "column": "time_spent_in_minutes",
        "operation": "SUM"
    }],
    "sort":
    {
        "column": "time_spent_in_minutes",
        "order": "DESC"
    }
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes |data-table
columns |List |Yes |valid column name
values |List |Yes |Object, Min length: 1, Max length: 10. <br > **column**: valid column <br > **operation**: Any value from COUNT, SUM, AVERAGE, STDDEV, VARIANCE, MAX, MIN
sort |Object |Yes |Object <br > **column**: valid column <br > **order**: Any value from ASC, DESC
exclude_empty_string | Boolean| No | Exclude [EMPTY] strings
show_column_totals | Boolean| No | Show Column Totals
width | Boolean| No | Any value from one-third , two-thirds, full. Default: full
filters | Object| No | Filter Object
title | String| No | Custom heading


### RICH TEXT
```json
{
    "type": "rich-text-insight",
    "html": "<p><strong>This is just a header</strong></p><p><i>Add blocks of <u>your choice</u></i></p>"
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes |rich-text-insight
html |String |Yes |HTML text
width | Boolean| No | Any value from one-third , two-thirds, full. Default: full


### Field: filters
Allowed values: object

The following filters can be applied

- Filter date columns with dynamic date range like last 30 days, last year, etc.
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

The following filter will be read as 

`Submission Date within last 30 days 
AND 
amount between range 10 to 20 
AND
Payment Mechanism INCLUDING cash`

Possible dynamic date ranges:

- last day
- last 7 days
- last 14 days
- last 30 days
- last 90 days
- last 6 months
- last 12 months
- last week
- this week
- this month


Possible operations:

- INCLUDING
- EXCLUDING


## Edit View

> Example 1: Edit view with all non-AI charts

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
        "operation": "SUM"
    },
    {
        "type": "bar",
        "x_axis": "Fee Month",
        "y_axis": "amount",
        "slice": "Submission Date",
        "operation": "MIN"
    }]
}'
```

> Example 2: Edit view with all non-AI charts and name

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
        "operation": "SUM"
    },
    {
        "type": "bar",
        "x_axis": "Fee Month",
        "y_axis": "amount",
        "slice": "Submission Date",
        "operation": "MIN"
    }]
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
