# Authentication & Limits

**Version 2.0.1** | **Status: Active**

---

## Authentication Limits & Quotas

To ensure platform stability and fair data access across the ecosystem, the MoMA API enforces strict rate limiting tied to your authentication credentials. Limits are enforced on a rolling 60-minute window based on your API key.

### Rate Limit Tiers

| Access Tier | Quota (Rolling 60m) | Eligibility Requirements |
| :--- | :--- | :--- |
| **Standard** | 1,000 requests | Default for public researchers, students, and educators. |
| **Enterprise** | 50,000 requests | Requires approved partner, institutional, or commercial status. |

### Rate Limit Headers
Every authenticated response includes standard HTTP headers detailing your current usage status. We strongly recommend engineering your application's logic to monitor and respect these headers to avoid service interruption.

* `X-RateLimit-Limit`: The maximum number of requests permitted in the current window.
* `X-RateLimit-Remaining`: The number of requests remaining before a throttle is applied.
* `X-RateLimit-Reset`: The time at which the current rate limit window resets (in UTC epoch seconds).

### Exceeding Limits
If your application exhausts its allocated quota, the authentication gateway will reject subsequent requests and return a `429 Too Many Requests` status code. 

**Error Response (429):**
```json
{
  "error": "rate_limit_exceeded",
  "message": "You have exceeded your API rate limit. Please retry after the timestamp indicated in the Retry-After header.",
  "retry_after": 1678883400
}
```