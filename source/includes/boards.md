# Board

The Boards API enables the creation of boards and blocks, each containing charts and visualizations that can be shared independently. You can embed specific visualizations into your site. Boards can be composed of multiple blocks, with each block representing a distinct visualization. Blocks can be created manually, or you can utilize the auto-generated blocks feature to assemble a board with a single click.


## Create Board

> Example 1: Create a basic board with 2 blocks

```shell
curl --location --request POST 'https://v3.polymersearch.com/api/v1/board' \
--header 'x-api-key: {{apikey}}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Sample Board 1",
    "file_ids": [
        "65b50541d83d1e4d42c7fbe0"
    ],
    "sharing": "public",
    "advanced_sharing":
    {
        "allow_global_filters_for_viewers": false,
        "allow_block_based_filters_for_viewers": true
    },
    "filters":
    {},
    "blocks": [
    {
        "type": "kpi",
        "metric": "time_spent_in_days",
        "operation": "SUM",
        "date": "solved_at",
        "date_range": "last 90 days",
        "goal": 1000,
        "file_id": "65b50541d83d1e4d42c7fbe0",
        "comp_date_range": "previous month"
    },
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
        },
        "show_totals": false,
        "file_id": "65b50541d83d1e4d42c7fbe0"
    }
    ]
}'
```


> The above command returns JSON structured like this:

```json
{
    "launch_url": "https://v3.polymersearch.com/b/6409bc2ae761d55b4630989b",
    "id": "6409bc2ae761d55b4630989b"
}
```

### HTTP Request

`POST https://v3.polymersearch.com/api/v1/board`

### Body content

Field | Mandatory | Description
--------- | ------- | -----------
name | true | Type: String<br />Name of the board
description | false | Type: String<br />Description of the board
file_ids | true | Type: List[String]<br />Dataset IDs to be associated with the board.
blocks | true | Type: List [Blocks Object] <br />
sharing | false | Desired sharing status for the board (public, private). Default: private
advanced_sharing | false | Controls sharing settings for the board.
advanced_sharing.allow_global_filters_for_viewers | false | Type: Boolean<br /> Allows viewers to apply global filters.
advanced_sharing.allow_block_based_filters_for_viewers | false | Type: Boolean<br /> Allows viewers to apply block-based filters.
branding.logoUrl | false | URL of the logo.
branding.logoLink | false | URL to redirect when the logo is clicked.
colors | false | Type: List<br />List of color codes to be used in view preview mode.
auto_generated | false | Type: Boolean<br /> Auto generate the board (populate with blocks based on our AI engine)
slug | false | Used for constructing a custom board URL. Length must be between 3 and 32 characters.
background_color | false | Valid CSS color name (eg. white, blue), or valid hexadecimal color code (eg. #ff5733)
notifications | false | Type: notifications Object<br />Settings for board digest email
filter_settings | false | Type: filter_settings Object<br />Columns to be shown on global filters per dataset


## notifications Object

> Example 1

```json
{
    "schedule":
    {
        "cadence": "daily",
        "hours": 9,
        "day": 1
    },
    "recipients": ["myemail@gmail.com"],
    "disabled": false
}
```


### Notes

- `schedule.cadence`: Defines the frequency of the schedule, which can be `daily`, `weekly`, or `monthly`.
- `schedule.hours`: Specifies the hour of the day for the schedule, ranging from `0` to `23`.
- `schedule.day`: Defines the day of the week, with values from `0` (Sunday) to `6` (Saturday).
- `schedule.monthly_schedule`: Required only for a `monthly` cadence. Accepts `last_day_of_month` or `first_day_of_month`.
- `recipients`: A list of email addresses to which notifications will be sent.
- `disabled`: A flag that, when set, disables the email notifications.



## filter_settings Object

> Example 1

```json
{
    "65b50541d83d1e4d42c7fbe0":
    {
        "columns":
        {
            "spend":
            {},
            "campaign_status":
            {
                "allowed_values": [
                    "active",
                    "pending"
                ]
            }
        }
    }
}
```

> Exemple 2

```json
{
    "65b50541d83d1e4d42c7fbe0":
    {
        "allow_all_columns": true,
        "columns":
        {
            "campaign_status":
            {
                "allowed_values": [
                    "active",
                    "pending"
                ]
            }
        }
    }
}
```

### Notes

- `65b50541d83d1e4d42c7fbe0` is the `file_id`.
- `65b50541d83d1e4d42c7fbe0.columns` refers to the list of columns that can be included in global filters.
- `65b50541d83d1e4d42c7fbe0.columns.spend` indicates that all values from the spend column are permitted in the global filters.
- `65b50541d83d1e4d42c7fbe0.columns.campaign_status.allowed_values` specifies that only the `active` and `pending` values from the `campaign_status` column are allowed in global filters.
- `65b50541d83d1e4d42c7fbe0.allow_all_columns` means all columns from the dataset will be available in global filters, except for the `campaign_status` column, which will only display `active` and `pending` values.


## Blocks Object


### Header Block
```json
{
    "type": "header",
    "heading": "heading1",
    "subheading": "sadsfsdfdsfd sub",
    "alignment": "left",
    "size": "large",
    "background": "gradient-f"
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type | String | Yes |header
heading | String | Yes | Mainheading on the block
subheading | String | Yes | Subheading on the block
alignment | String | No | Any value from `left`, `center`, `right`
size | String | No | Any value from `small`, `medium`, `large`
background | String | No | Any value from `transparent`, `white`, `grey`, `black`, `gradient-a`, `gradient-b`, `gradient-c`, `gradient-d`, `gradient-e`, `gradient-f`


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
    "y_axis_log": true,
    "show_annotations": true,
    "show_stacked": false,
    "file_id": "65b50541d83d1e4d42c7fbe0"
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes |bar
file_id |String |Yes | Dataset ID to drive this block
x_axis |List | One of the `x_axis` or `x_axis_multiple` is required | Valid column name
x_axis_multiple | List | One of the `x_axis` or `x_axis_multiple` is required | Object, Min length: 2, Max length: 10. <br > **name**: Valid column <br > **operation**: Any value from `COUNT`, `COUNT_UNIQUE`, `SUM`, `AVERAGE`, `STDDEV`, `VARIANCE`, `MAX`, `MIN`
y_axis | String| Yes| Valid column name
operation | String| No | Any value from `COUNT`, `COUNT_UNIQUE`, `SUM`, `AVERAGE`, `STDDEV`, `VARIANCE`, `MAX`, `MIN`
sort | Object | No | **type**: `total` (Total), `raw` (Raw Order), `count` (Count), `value` (x-axis tags) <br > **operation**: Any  value from `asc`, `desc`
slice | String| No| Valid column name
show_annotations | Boolean| No | Annotate each segment by its value
show_stacked | Boolean| No | Show as stack. Default: `true`
is_percentage | Boolean| No | Show as percentage
y_axis_log | Boolean| No | Use logarithmic scale for Y-Axis
exclude_empty_string | Boolean| No | Exclude [EMPTY] strings. Default: `true`
width_in_columns | Integer| No | Any value from 1 to 6. Default: 3
height | Integer| No | Any value from 2 to 3. Default: 2
filters | Object| No | Filter Object
title | String| No | Custom heading
show_explanation | Boolean| No | Show explanation under title


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
    "show_annotations": true,
    "show_stacked": false,
    "file_id": "65b50541d83d1e4d42c7fbe0"
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String | Yes |column
file_id |String |Yes | Dataset ID to drive this block
x_axis | String| Yes| Valid column name
y_axis | String | One of the `y_axis` or `y_axis_multiple` is required | Valid column name
y_axis_multiple | List | One of the `y_axis` or `y_axis_multiple` is required | Object, Min length: 2, Max length: 10. <br > **name**: Valid column <br > **operation**: Any value from `COUNT`, `COUNT_UNIQUE`, `SUM`, `AVERAGE`, `STDDEV`, `VARIANCE`, `MAX`, `MIN`
operation | String| No | Any value from `COUNT`, `COUNT_UNIQUE`, `SUM`, `AVERAGE`, `STDDEV`, `VARIANCE`, `MAX`, `MIN`
sort | Object | No | **type**: total (Total), raw (Raw Order), count (Count), value (x-axis tags) <br > **operation**: Any value from `asc`, `desc`
slice | String| No| Valid column name
show_annotations | Boolean| No | Annotate each segment by its value
show_stacked | Boolean| No | Show as stack. Default: `true`
is_percentage | Boolean| No | Show as percentage
x_axis_log | Boolean| No | Use logarithmic scale for X-Axis
exclude_empty_string | Boolean| No | Exclude [EMPTY] strings. Default: `true`
width_in_columns | Integer| No | Any value from 1 to 6. Default: 3
height | Integer| No | Any value from 2 to 3. Default: 2
filters | Object| No | Filter Object
title | String| No | Custom heading
show_explanation | Boolean| No | Show explanation under title


### SCATTER PLOT Chart
```json
{
    "type": "scatter",
    "x_axis": "spend",
    "y_axis": "cost_per_initiate_checkout",
    "operation": "SUM",
    "x_axis_log": true,
    "file_id": "65b50541d83d1e4d42c7fbe0"
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes |scatter
file_id |String |Yes | Dataset ID to drive this block
x_axis | String| Yes| Valid number column name
y_axis |String |Yes | Valid number column name
operation | String| Yes| Any value from `COUNT`, `COUNT_UNIQUE`, `SUM`, `AVERAGE`, `STDDEV`, `VARIANCE`, `MAX`, `MIN`
slice | String| No| Valid column name
x_axis_log | Boolean| No | Use logarithmic scale for X-Axis
y_axis_log | Boolean| No | Use logarithmic scale for Y-Axis
exclude_empty_string | Boolean| No | Exclude [EMPTY] strings. Default: `true`
width_in_columns | Integer| No | Any value from 1 to 6. Default: 3
height | Integer| No | Any value from 2 to 3. Default: 2
filters | Object| No | Filter Object
title | String| No | Custom heading
show_explanation | Boolean| No | Show explanation under title


### TIMESERIES Chart
```json
{
    "type": "timeseries",
    "x_axis": "date",
    "operation": "SUM",
    "y_axis_log": true,
    "exclude_empty_string": false,
    "group_by": "quarter",
    "is_area": true,
    "file_id": "65b50541d83d1e4d42c7fbe0"
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes |timeseries
file_id |String |Yes | Dataset ID to drive this block
x_axis | String| Yes| valid date column name
y_axis |String | No | Valid number column name
y_axis_multiple | List | No | Object, Min length: 2, Max length: 10. <br > **name**: Valid number column <br > **operation**: Any value from `COUNT`, `COUNT_UNIQUE`, `SUM`, `AVERAGE`, `STDDEV`, `VARIANCE`, `MAX`, `MIN`
slice | String| No| Valid column name
is_area | Boolean| No | Use area chart
y_axis_log | Boolean| No | Use logarithmic scale for Y-Axis
exclude_empty_string | Boolean| No | Exclude [EMPTY] strings. Default: `true`
group_by | String| No | Any value from day, week, month, quarter, year
width_in_columns | Integer| No | Any value from 1 to 6. Default: 3
height | Integer| No | Any value from 2 to 3. Default: 2
filters | Object| No | Filter Object
title | String| No | Custom heading
show_explanation | Boolean| No | Show explanation under title


### HEATMAP Chart
```json
{
    "type": "heatmap",
    "y_axis": "account_currency",
    "operation": "SUM",
    "exclude_empty_string": false,
    "show_annotations": true,
    "file_id": "65b50541d83d1e4d42c7fbe0"
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes |heatmap
file_id |String |Yes | Dataset ID to drive this block
y_axis |String |Yes | Valid column name
x_axis | String| No| Valid column name
operation | String| Yes| Any value from `COUNT`, `COUNT_UNIQUE`, `SUM`, `AVERAGE`, `STDDEV`, `VARIANCE`, `MAX`, `MIN`
metric | String| No| Valid column name
show_annotations | Boolean| No | Annotate each segment by its value
exclude_empty_string | Boolean| No | Exclude [EMPTY] strings. Default: `true`
width_in_columns | Integer| No | Any value from 1 to 6. Default: 3
height | Integer| No | Any value from 2 to 3. Default: 2
filters | Object| No | Filter Object
title | String| No | Custom heading
show_explanation | Boolean| No | Show explanation under title


### LINEPLOT Chart
```json
{
    "type": "lineplot",
    "x_axis": "spend",
    "y_axis": "link_click",
    "operation": "SUM",
    "file_id": "65b50541d83d1e4d42c7fbe0"
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes |lineplot
file_id |String |Yes | Dataset ID to drive this block
y_axis |String | One of the `y_axis` or `y_axis_multiple` is required | Valid column name
y_axis_multiple | List | One of the `y_axis` or `y_axis_multiple` is required | Object, Min length: 2, Max length: 10. <br > **name**: Valid column <br > **operation**: Any value from `COUNT`, `COUNT_UNIQUE`, `SUM`, `AVERAGE`, `STDDEV`, `VARIANCE`, `MAX`, `MIN`
x_axis | String| Yes| Valid column name
operation | String| Yes| Any value from `COUNT`, `COUNT_UNIQUE`, `SUM`, `AVERAGE`, `STDDEV`, `VARIANCE`, `MAX`, `MIN`
slice | String| No| Valid column name
y_axis_log | Boolean| No | Use logarithmic scale for Y-Axis
exclude_empty_string | Boolean| No | Exclude [EMPTY] strings. Default: `true`
width_in_columns | Integer| No | Any value from 1 to 6. Default: 3
height | Integer| No | Any value from 2 to 3. Default: 2
filters | Object| No | Filter Object
title | String| No | Custom heading
show_explanation | Boolean| No | Show explanation under title


### PIE Chart
```json
{
    "type": "pie",
    "x_axis_multiple": [
    {
        "name": "status"
    }],
    "exclude_empty_string": false,
    "show_annotations": true,
    "file_id": "65b50541d83d1e4d42c7fbe0"
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes |pie
file_id |String |Yes | Dataset ID to drive this block
x_axis_multiple |List |Yes |Object, Min length: 1, Max length: 2. <br > **name**: Valid column
y_axis_multiple |List |No |Object, Min length: 1, Max length: 1. <br > **name**: Valid number column <br > **operation**: Any value from `COUNT`, `COUNT_UNIQUE`, `SUM`, `AVERAGE`, `STDDEV`, `VARIANCE`, `MAX`, `MIN`
show_annotations | Boolean| No | Annotate each segment by its value
exclude_empty_string | Boolean| No | Exclude [EMPTY] strings. Default: `true`
width_in_columns | Integer| No | Any value from 1 to 6. Default: 3
height | Integer| No | Any value from 1 to 3. Default: 2
filters | Object| No | Filter Object
title | String| No | Custom heading
show_explanation | Boolean| No | Show explanation under title


### OUTLIER
```json
{
    "type": "outlier",
    "metric": "spend",
    "operation": "COUNT",
    "exclude_empty_string": false,
    "influencing_columns": [
        "ad_name"
    ],
    "file_id": "65b50541d83d1e4d42c7fbe0"
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes |outlier
file_id |String |Yes | Dataset ID to drive this block
metric |String |Yes | Valid number column name
operation | String| Yes| Any value from `COUNT`, `COUNT_UNIQUE`, `SUM`, `AVERAGE`, `STDDEV`, `VARIANCE`, `MAX`, `MIN`
influencing_columns |List |Yes |Influencing Columns - list of Valid column names. Min length: 1, Max length: 6
results_type |String |No |Show results - Any value from `count`, `below_average_only`, `above_average_only`, `top_and_bottom_outliers`, `above_and_below_average`
show_results_column | Boolean| No | Show Results Column
exclude_empty_string | Boolean| No | Exclude [EMPTY] strings
width_in_columns | Integer| No | Any value from 1 to 6. Default: 3
height | Integer| No | Any value from 1 to 3. Default: 2
filters | Object| No | Filter Object
title | String| No | Custom heading
lower_better | Boolean| No |  Indicates if a lower value is better.
show_explanation | Boolean| No | Show explanation under title


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
    "show_results_column": false,
    "file_id": "65b50541d83d1e4d42c7fbe0"
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes |roi
file_id |String |Yes | Dataset ID to drive this block
max_metric |String |Yes | Metric to Maximize (Return) - valid number column name
max_operation | String| Yes| Any value from `COUNT`, `COUNT_UNIQUE`, `SUM`, `AVERAGE`, `STDDEV`, `VARIANCE`, `MAX`, `MIN`
min_metric |String |Yes | Metric to Minimize (Investment) - valid number column name
min_metric | String| Yes| Any value from `COUNT`, `COUNT_UNIQUE`, `SUM`, `AVERAGE`, `STDDEV`, `VARIANCE`, `MAX`, `MIN`
influencing_columns |List |Yes | Influencing Columns - list of valid column names. Min length: 1, Max length: 6
show_results_column | Boolean| No | Show Results Column
show_percentage | Boolean| No | Show ROI as Percentage
exclude_empty_string | Boolean| No | Exclude [EMPTY] strings
width_in_columns | Integer| No | Any value from 1 to 6. Default: 3
height | Integer| No | Any value from 1 to 3. Default: 2
filters | Object| No | Filter Object
title | String| No | Custom heading
lower_better | Boolean| No | Indicates if a lower value is better.
show_explanation | Boolean| No | Show explanation under title


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
    "columns": ["ad_name"],
    "file_id": "65b50541d83d1e4d42c7fbe0"
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes |pivot
file_id |String |Yes | Dataset ID to drive this block
metrics |List |Yes |Object, Min length: 1, Max length: 10. <br > **metric**: Valid column <br > **operation**: Any value from `COUNT`, `COUNT_UNIQUE`, `SUM`, `AVERAGE`, `STDDEV`, `VARIANCE`, `MAX`, `MIN`
rows |List |Yes |Rows - list of Valid column names. Min length: 1, Max length: 1
columns |List |Yes |Columns - list of Valid column names. Min length: 1, Max length: 1
show_row_totals | Boolean| No | Show Row Totals
show_column_totals | Boolean| No | Show Column Totals
show_percentage | Boolean| No | Show Percentage, Default: `True`
sort_by_row_tags | String| No | Sort rows by tag value. Any  value from `ASC`, `DESC`
column_manual_order | List| No | Sort columns by column tags. List of tag values
sort_by_counts |Object |No | **column_index**: index of the column given in columns <br > **metric_index**: index of the column given in metrics <br > **order**: Any  value from `ASC`, `DESC`
width_in_columns | Integer| No | Any value from 1 to 6. Default: 3
height | Integer| No | Any value from 1 to 3. Default: 2
filters | Object| No | Filter Object
title | String| No | Custom heading
pin_totals | Boolean| No | Pin Totals
show_explanation | Boolean| No | Show explanation under title


### KPI BLOCK
```json
{
    "type": "kpi",
    "metric": "impressions",
    "operation": "SUM",
    "date": "date",
    "date_range": "last 90 days",
    "goal": 4000000,
    "file_id": "65b50541d83d1e4d42c7fbe0"
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes |kpi
file_id |String |Yes | Dataset ID to drive this block
metric |List |Yes | Valid date column name
operation | String| Yes| Any value from `COUNT`, `COUNT_UNIQUE`, `SUM`, `AVERAGE`, `STDDEV`, `VARIANCE`, `MAX`, `MIN`
date | String| No| Valid date column name
date_range | String| No| Any value from 'last day', 'last 7 days', 'last 14 days', 'last 30 days', 'last 90 days', 'last 6 months', 'last 12 months, 'this month', 'this week', 'last week', 'week from monday', 'this quarter', 'this year', 'week to date', 'month to date', 'quarter to date', 'year to date', 'previous week', 'previous month', 'previous quarter', 'previous year', custom
comp_date_range | String| No| Any value from 'previous period', 'previous week', 'previous month', 'previous querter', 'previous year', 'custom'
goal |Number |No |
exclude_empty_string | Boolean| No | Exclude [EMPTY] strings
width_in_columns | Integer| No | Any value from 1 to 6. Default: 1
height | Integer| No | Any value from 1 to 3. Default: 1
filters | Object| No | Filter Object
show_explanation | Boolean| No | Show explanation under title


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
    },
    "file_id": "65b50541d83d1e4d42c7fbe0"
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes | data-table
file_id |String |Yes | Dataset ID to drive this block
columns |List |Yes | Valid column name
values |List |Yes |Object, Min length: 1, Max length: 10. <br > **column**: Valid column <br > **operation**: Any value from `COUNT`, `COUNT_UNIQUE`, `SUM`, `AVERAGE`, `STDDEV`, `VARIANCE`, `MAX`, `MIN`
sort |Object |Yes |Object <br > **column**: Valid column <br > **order**: Any value from `ASC`, `DESC`
exclude_empty_string | Boolean| No | Exclude [EMPTY] strings
show_totals | Boolean| No | Show Column Totals
width_in_columns | Integer| No | Any value from 1 to 6. Default: 3
height | Integer| No | Any value from 1 to 3. Default: 2
filters | Object| No | Filter Object
title | String| No | Custom heading
show_explanation | Boolean| No | Show explanation under title
hide_title | Boolean| No | Hide title


### Gallery Block
```json
{
    "type": "gallery",
    "is_aggregate": true,
    "aggregate":
    {
        "metrics": [
        {
            "name": "Checkouts initiated",
            "operation": "VARIANCE"
        }],
        "base_column": "Ad name"
    },
    "image_column": "Media url",
    "layout": "expanded",
    "appearance": "fit",
    "enable_card_modal": true,
    "sections": [
    {
        "columns": [
            "Impressions"
        ],
        "title": "Section 1"
    }],
    "file_id": "66e3f70cb399ce00086ba8b9"
}
```

```json
{
    "type": "gallery",
    "is_aggregate": false,
    "card_columns": [
        "Reach",
        "Thruplays"
    ],
    "image_column": "Media url",
    "layout": "expanded",
    "appearance": "fit",
    "enable_card_modal": true,
    "link_label": "Click here to visit",
    "file_id": "66e3f70cb399ce00086ba8b9"
}
```

Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes | gallery
file_id |String |Yes | Dataset ID to drive this block
is_aggregate |Boolean |Yes | true for `Summarized`, false for `Raw`
aggregate.metrics |List |No |Object, Min length: 1, Max length: 10. <br > **name**: Valid column <br > **operation**: Any value from `COUNT`, `COUNT_UNIQUE`, `SUM`, `AVERAGE`, `STDDEV`, `VARIANCE`, `MAX`, `MIN`, `MEDIAN`, `MODE`
aggregate.base_column |Boolean |Yes for  `Summarized` | Valid column
card_columns |List |No | Valid column
image_column |String |Yes | Valid image/video column
layout | String | No | Any value from `expanded`, `normal`, `condensed`
appearance | String | No | Any value from `fit`, `fill`
headline_column |String |No | Valid column
description_column |String |No | Valid column
link_column |String |No | Valid column
link_label |String |No | Link label
enable_card_modal | Boolean |No| Enable modal on click
sections |Yes |No |Object, Min length: 1, Max length: 10. <br > **columns**: Valid column name <br > **title**: Section title
title | String| No | Custom heading
width_in_columns | Integer| No | Any value from 1 to 6. Default: 3
height | Integer| No | Any value from 1 to 3. Default: 2
filters | Object| No | Filter Object
enable_search_sort | Boolean |No| Enable searching and sorting
hide_title | Boolean| No | Hide title


### RICH TEXT
```json
{
    "type": "rich-text-insight",
    "html": "<p><strong>This is just a header</strong></p><p><i>Add blocks of <u>your choice</u></i></p>"
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes | rich-text-insight
html |String |Yes | HTML text
width_in_columns | Integer| No | Any value from 1 to 6. Default: 3
height | Integer| No | Any value from 1 to 3. Default: 1
hide_title | Boolean| No | Hide title


### IMAGE BLOCK
```json
{
    "type": "image",
    "appearance": "fit",
    "url": "https://cdn-v3-dev.polymerdev.com/assets/logo-4743e3c9.svg"
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes |image
appearance |String |Yes |Any value from `fit`,`fill`
url |String |Yes |Any valid public image URL
width_in_columns | Integer| No | Any value from 1 to 6. Default: 3
height | Integer| No | Any value from 1 to 3. Default: 2
title | String| No | Custom heading


### MAP BLOCK
```json
{
    "type": "map",
    "base_column": "country",
    "metrics": [
        {
            "name": "annual_revenue",
            "operation": "AVERAGE"
        }
    ],
    "file_id": "66b9d4ece653ad0008f8ce90"
}
```
Field | Datatype | Mandatory | Desc
------ | ------ | ------ | --------
type |String |Yes |map
file_id |String |Yes | Dataset ID to drive this block
base_column |String |Yes | Valid column name that can be used for plotting on map
metrics |List |Yes |Object, Min length: 1, Max length: 10. <br > **name**: Valid column <br > **operation**: Any value from `COUNT`, `COUNT_UNIQUE`, `SUM`, `AVERAGE`, `STDDEV`, `VARIANCE`, `MAX`, `MIN`
width_in_columns | Integer| No | Any value from 1 to 6. Default: 3
height | Integer| No | Any value from 2 to 3. Default: 2
title | String| No | Custom heading
hide_title | Boolean| No | Hide title


### Field: filters
Allowed values: object

The following filters can be applied

- Date Columns: Filter using dynamic date ranges, such as "last 30 days," "last year," etc.
- Numerical Columns: Filter using ranges, such as "amount between 25 to 45."
- Categorical Columns (Text Search):
    - Include specific values, e.g., "payment mechanism including cash and demand draft."
    - Exclude specific values, e.g., "payment mechanism excluding cash."

Example payload
`
{
    "65b50541d83d1e4d42c7fbe0":
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


## Edit Board

> Example 1: Edit board with blocks

```shell
curl --location --request PUT 'https://v3.polymersearch.com/api/v1/board/63f36125bfc81986e3cbd2c3' \
--header 'x-api-key: {{apikey}}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "blocks": [
    {
        "type": "timeseries",
        "x_axis": "payment_mechanism",
        "y_axis": "Submission Date",
        "slice": "amount"
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

> Example 2: Edit board with blocks and name

```shell
curl --location --request PUT 'https://v3.polymersearch.com/api/v1/board/63f36125bfc81986e3cbd2c3' \
--header 'x-api-key: {{apikey}}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Edited Board Name",
    "blocks": [
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
    "launch_url": "https://v3.polymersearch.com/b/6409bc2ae761d55b4630989b",
    "id": "6409bc2ae761d55b4630989b"
}
```

### HTTP Request

`PUT https://v3.polymersearch.com/api/v1/board/:board_id`

### URL Params

Field | Mandatory | Description
--------- | ------- | -----------
board_id | true | Type: String<br />Board ID


### Body content

Field | Mandatory | Description
--------- | ------- | -----------
name | false | Type: String<br />Name of the board
description | false | Type: String<br />Description of the board
blocks | false | Type: List [Blocks Object] <br />
sharing | false | Desired sharing status for the dataset (public, private). Default: private
advanced_sharing | false | control sharing settings for board
advanced_sharing.allow_global_filters_for_viewers | false | Type: Boolean<br /> Allows viewers to apply global filters.
advanced_sharing.allow_block_based_filters_for_viewers | false | Type: Boolean<br /> Allows viewers to apply block-based filters.
branding.logoUrl | false | URL of the logo.
branding.logoLink | false | URL to redirect when the logo is clicked.
colors | false | Type: List<br /> List of color codes to be used in view preview mode.
slug | false | Used for constructing a custom board URL. Length must be between 3 and 32 characters.
background_color | false | Valid CSS color name (eg. white, blue), or valid hexadecimal color code (eg. #ff5733 )
notifications | false | Type: notifications Object<br />Settings for board digest email
filter_settings | false | Type: filter_settings Object<br />Columns to be shown on global filters per dataset

### Blocks Object
Same as described on Create Board request
Note: Make sure you pass all the blocks inside `blocks` key

### notifications Object
Same as described on Create Board request
Note: Make sure you pass all the blocks inside `notifications` key


## Fetch Boards

> Response

```json
{
    "data": [
        {
            "_id": "63f36125bfc81986e3cbd2c3",
            "created_at": "2023-02-20T12:01:41.730Z",
            "updated_at": "2023-02-20T12:01:41.730Z",
            "uid": "abf3a195-4135-4471-9d24-ab2acde3e45a",
            "user_id": "636e0856759be7e1f00cfa0f",
            "file_id": "63d8248de061fa0d2023f20a",
            "name": "board - 1",
            "description": "For Daily reporting on Ads",
            "sharing": "public",
            "is_template": "false"
        },
        {
            "_id": "6409bb0be045c05b1fccb721",
            "created_at": "2023-03-09T10:55:07.578Z",
            "updated_at": "2023-03-09T10:55:07.578Z",
            "uid": "52f0ecfa-9545-4a0b-8e7f-8d47c1aefcb9",
            "user_id": "636e0856759be7e1f00cfa0f",
            "file_id": "6409b295e0eb635a29d8c8f7",
            "name": "Board with advanced_sharing",
            "sharing": "public",
            "advanced_sharing": {
                "allow_global_filters_for_viewers": false,
                "allow_block_based_filters_for_viewers": true
            }
        },
        {
            "_id": "6409bc2ae761d55b4630989b",
            "created_at": "2023-03-09T10:59:54.313Z",
            "updated_at": "2023-03-09T10:59:54.313Z",
            "uid": "7ce8918b-441e-4ee1-8977-970b47ea9b68",
            "user_id": "636e0856759be7e1f00cfa0f",
            "file_id": "6409b295e0eb635a29d8c8f7",
            "name": "Board with advanced_sharing11",
            "sharing": "public",
            "advanced_sharing": {
                "allow_global_filters_for_viewers": false,
                "allow_block_based_filters_for_viewers": true
            }
        }
    ],
    "limit": 10,
    "page": 1,
    "sort_key": "created_at",
    "sort_order": "asc"
}
```

### HTTP Request

`GET https://v3.polymersearch.com/api/v1/boards`



## Delete Board

> Response

```json
{
   "success": true
}
```

### HTTP Request

`DELETE https://v3.polymersearch.com/api/v1/board/:board_id`

### URL Params

Field | Mandatory | Description
--------- | ------- | -----------
board_id | true | Type: String<br />Board ID