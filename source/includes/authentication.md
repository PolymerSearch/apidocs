# Authentication

Polymer API uses API keys to allow access to our endpoints. You can register a new API key as a user, inside user settings, on the API Keys section.

Currently you can create as many API Keys as you want and give them a name. Once you don't want to use it you can disable it from the dashboard.

Polymer API expects the API key to be included in all API requests to the server. There are two ways to include it in requests:

As a query parameter: `?api_key=&your_api_key`

As a header: `X-API-KEY: &your_api_key`

## Please note that the "workspace-id" header is optional. It is only necessary when you intend to execute an operation within a workspace other than the default one defined by the APIKEY.

<aside class="success">You must replace `&your_api_key with` your personal API key.</aside>