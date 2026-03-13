# Collection API Reference

**Version 2.0.1** | **Status: Active**

---

The Collection API provides programmatic, read-only access to the catalog of artworks and artists. This RESTful API returns data in JSON format and is designed to support academic research, external application development, and internal curatorial tools.

## Authentication & Limits

The Collection API is open for public `GET` requests and does not require an API key for basic querying. All requests must be made over HTTPS. Plain HTTP requests are refused.

To ensure infrastructure stability, unauthenticated requests are strictly governed by the following limits:

* **Rate Limit:** 60 requests per minute per IP address.
* **Pagination Limit:** Maximum 100 objects per response payload.

Exceeding the rate limit will result in a `429 Too Many Requests` response. Enterprise clients requiring higher throughput must append an `X-Client-ID` header to bypass standard throttling.

---

## Endpoints

### 01. List Artworks
Retrieve a paginated list of artworks in the collection.

**`GET /artworks`**

#### Query Parameters

| Parameter | Type | Required | Description | Default |
| :--- | :--- | :--- | :--- | :--- |
| `page` | Integer | No | The page number to retrieve. | `1` |
| `limit` | Integer | No | The number of results per page (Max: 100). | `20` |
| `department` | String | No | Filter by curatorial department. | `null` |
| `has_image` | Boolean | No | Filter for works with digitized public domain images. | `false` |

#### Example Request

```bash
curl -X GET "[https://api.moma.org/v2/artworks?department=Photography&limit=2](https://api.moma.org/v2/artworks?department=Photography&limit=2)" \
  -H "Accept: application/json"
```

#### Example Response (200 OK)

```json
{
  "pagination": {
    "total": 14205,
    "page": 1,
    "limit": 2
  },
  "data": [
    {
      "id": 4362,
      "title": "Migrant Mother, Nipomo, California",
      "artist": "Dorothea Lange",
      "date": "1936",
      "department": "Photography"
    },
    {
      "id": 8921,
      "title": "Moonrise, Hernandez, New Mexico",
      "artist": "Ansel Adams",
      "date": "1941",
      "department": "Photography"
    }
  ]
}
```

---

### 02. Retrieve Specific Artwork
Retrieve detailed, singular metadata for an artwork using its unique system identifier.

**`GET /artworks/{id}`**

#### Path Parameters

| Parameter | Type | Required | Description |
| :--- | :--- | :--- | :--- |
| `id` | Integer | **Yes** | The unique `ObjectID` assigned at ingestion. |

#### Example Request

```bash
curl -X GET "[https://api.moma.org/v2/artworks/4362](https://api.moma.org/v2/artworks/4362)" \
  -H "Accept: application/json"
```

#### Example Response (200 OK)

```json
{
  "data": {
    "id": 4362,
    "accession_number": "341.1937",
    "title": "Migrant Mother, Nipomo, California",
    "artist": "Dorothea Lange",
    "date": "1936",
    "medium": "Gelatin silver print",
    "dimensions": "11 1/8 x 8 9/16\" (28.3 x 21.8 cm)",
    "department": "Photography",
    "url": "[https://www.moma.org/collection/works/4362](https://www.moma.org/collection/works/4362)"
  }
}
```

---

## Error Handling

The API utilizes standard HTTP status codes to indicate the success or failure of a request. When an error occurs, the response body will contain a standardized JSON payload outlining the issue.

#### Example Error Response (404 Not Found)
```json
{
  "error": {
    "code": 404,
    "type": "ResourceNotFoundError",
    "message": "Artwork with ObjectID 999999 does not exist in the catalog."
  }
}
```

#### Status Codes

| Code | Status | Resolution |
| :--- | :--- | :--- |
| `200` | OK | Request succeeded. |
| `400` | Bad Request | The request was malformed. Verify query parameters and syntax. |
| `404` | Not Found | The requested resource (`ObjectID`) does not exist in the catalog. |
| `429` | Too Many Requests | Rate limit exceeded. Pause requests for 60 seconds. |
| `500` | Internal Server Error | Upstream catalog sync failure. Check system status. |