# Rate Limiting

All Polymer APIs enforce rate limiting. Each API key is allowed up to 100 requests per hour. Once the rate limit is reached, the server will respond with HTTP Status 429 - Too Many Requests.

Rate-limiting details are included in the response headers:

- **X-RateLimit-Limit**: The maximum number of requests allowed per hour.
- **X-RateLimit-Remaining**: The number of requests remaining in the current time window.
- **X-RateLimit-Reset**: The time remaining before the rate limit resets, in UTC epoch seconds.

Currently, rate limiting is not applied on a per-user basis, but this may be introduced in future updates.
