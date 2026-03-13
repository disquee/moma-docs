# Authentication & Limits

**Version 2.0.1** | **Status: Active**

---

The API utilizes standard HTTP status codes to indicate the success or failure of a request. When an error occurs, the response body will contain a standardized JSON payload outlining the issue.

## Example Error Response (404 Not Found)

```json
{
  "error": {
    "code": 404,
    "type": "ResourceNotFoundError",
    "message": "Artwork with ObjectID 999999 does not exist in the catalog."
  }
}
```

## Status Codes

| Code | Status | Resolution |
| :--- | :--- | :--- |
| `200` | OK | Request succeeded. |
| `400` | Bad Request | The request was malformed. Verify query parameters and syntax. |
| `404` | Not Found | The requested resource (`ObjectID`) does not exist in the catalog. |
| `429` | Too Many Requests | Rate limit exceeded. Pause requests for 60 seconds. |
| `500` | Internal Server Error | Upstream catalog sync failure. Check system status. |