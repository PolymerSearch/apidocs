# Rate Limiting

Embrace the Power of Rate Limiting with Polymer APIs!

To ensure fair usage and maintain optimal performance, rate limiting is applied to all Polymer APIs. Here's what you need to know:

Each API key has a generous limit of 100 requests per hour. Once this limit is reached, any subsequent requests will receive an HTTP Status 429 - Too Many Requests response.

To keep you informed and in control, the response headers provide valuable rate-limiting details:

- X-RateLimit-Limit: This header reveals the total number of requests allowed within a one-hour time window.
- X-RateLimit-Remaining: Stay on top of your request count with this header, which shows the number of requests you have left for the current time window.
- X-RateLimit-Reset: Plan your actions accordingly with this header, as it indicates the remaining time in UTC epoch seconds before the rate limit resets.

At the moment, rate limiting is not enforced on a per-user basis. However, please note that future updates may introduce per-user rate limits.

Embrace the balance between power and fairness with Polymer APIs' rate limiting. Let's build a better, more efficient API ecosystem together!
