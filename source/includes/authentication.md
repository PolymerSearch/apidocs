# Authentication

Polymer API uses API keys to allow access to our endpoints. You can register a new API key inside user settings in the API Keys section.

You can create as many API Keys as you want and name them. Once you don't want to use it, you can disable or remove it from the dashboard.

You must include the API key in all requests to the server. There are two ways to include it:

As a query parameter: `?api_key=&your_api_key`

As a header: `X-API-KEY: &your_api_key`

<aside class="success">You must replace `&your_api_key with` your personal API key.</aside>