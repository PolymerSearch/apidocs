# Changelog

## August 21, 2024 - V3 APIs
- Added support for background color on boards.
- Introduced control for board digest emails at the workspace level.
- Added control for PolyAI in read-only permissions at the workspace level.

## July 7, 2024 - V3 APIs
- Added support for disabling the share button at the workspace level.
- Introduced support for Image and Map blocks.
- Enhanced board-level advanced sharing options.
- Added timezone support at both the workspace and board levels.

## June 5, 2024 - V3 Board API
- Introduced support for slugs in board and workspace-level APIs.

## May 5, 2024 - V3 Dataset API
- Added support for incremental updates.
- Introduced a skip email flag for workspace invites.

## May 4, 2024 - V3 Workspace APIs
- Added support for custom DNS.

## March 5, 2024 - V3 Board APIs Improvement
- Added support for embed permissions: `board_read_only`, `board_edit`, `workspace_read_only`, `workspace_edit`, `block_level_read_only`.

## January 5, 2024 - V3 Workspace APIs
- Added support for board CRUD APIs with basic chart types: Bar, Column, Pivot, Pie, Timeseries.

## October 5, 2023 - V3 Workspace APIs
- Added support for V3 board embedding via token.

## August 28, 2023 - V3 Workspace APIs
- Added support for workspace members CRUD.

## July 15, 2023 - V3 Workspace APIs
- Added support for workspace CRUD.

## January 6, 2023 - V3 Initial Release
- Released V3 APIs for dataset and board creation.

## February 5, 2022 - Feature Addition
- Added support for JSON and Excel formats in the `/v1/dataset` API.

## September 28, 2021 - Feature Addition
- Added support for the force flag in the `/v1/dataset` API.
- Introduced the Update Dataset API - `PUT /v1/dataset/:id`.

## September 13, 2021 - Feature Addition
- Added support for starting row.

## July 21, 2021 - Initial Release
- Launched the first version of the Polymer public API, including two endpoints to create a Polymer website from a CSV file.
