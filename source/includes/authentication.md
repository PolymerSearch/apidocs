# Authentication

Polymer API uses API keys to authenticate access to its endpoints. You can generate a new API key within your user settings under the "API Keys" section.

You can create multiple API keys, each with a custom name. If you no longer need an API key, you can disable it via the dashboard.

Include your API key in all requests to the Polymer API. There are two supported methods for passing the API key:

As a query parameter: `?api_key=&your_api_key`

As a header: `X-API-KEY: &your_api_key`

## The "workspace-id" header is optional. It is required only when you need to perform operations in a workspace other than the default one associated with your API key.

<aside class="success">Replace `&your_api_key` with your actual API key.</aside>