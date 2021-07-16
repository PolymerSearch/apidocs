# Rate Limiting

All PolymerSearch APIs have rate limiting implemented. A single API key can make up to 100 requests per hour. After reaching the rate limit, HTTP Status 429 - Too Many Requests, will be returned.

Response headers contain rate-limiting details:

X-RateLimit-Limit: Number of requests you can make in an hour
X-RateLimit-Remaining: Number of requests left for the time window
X-RateLimit-Reset: The remaining window before the rate limit resets in UTC epoch seconds

Currently there is no rate limiting per user, but it may be introduced in future updates.