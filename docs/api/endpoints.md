# Endpoints

**Version 2.0.1** | **Status: Active**

---

The MoMA API utilizes dedicated endpoints to manage your authentication tokens and verify access scopes. You must route all authentication requests through the `/v1/auth/` path.

### Generate an Access Token
Exchange your client credentials for a temporary bearer token to access protected data endpoints. Tokens are valid for 3600 seconds (1 hour).

**Endpoint:** `POST /v1/auth/token`

**Request Body:**
```json
{
  "client_id": "YOUR_CLIENT_ID",
  "client_secret": "YOUR_CLIENT_SECRET",
  "grant_type": "client_credentials"
}
```

### Verify Key Status
Check the validity, operational scope, and expiration timeline of your current API key without triggering a data query.

**Endpoint:** `GET /v1/auth/verify`

**Headers:**
`Authorization: Bearer <YOUR_API_KEY>`

**Success Response (200 OK):**
```json
{
  "status": "active",
  "scopes": ["read:artworks", "read:exhibitions"],
  "expires_at": "2026-12-31T23:59:59Z"
}
```