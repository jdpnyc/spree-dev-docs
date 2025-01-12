# Authenticating requests

Storefront API requires authorization only for certain actions associated with user account (e.g. updating saved addresses) or manipulating cart and checkout.

### Generating OAuth token

To obtain a token, send the following `POST` request to `/spree_oauth/token`

```
{
  "grant_type": "password",
  "username": "user@example.com",
  "password": "xxx"
}
```

In the response, you'll receive a token to pass in `Authorization: Bearer {token}` header when making requests to the Storefront API.

### Refreshing OAuth token

OAuth tokens obtained via the previous step are valid only for a specific time. To refresh it, use the refresh token that comes together with the bearer token.

To refresh a token, send the following `POST` request to `/spree_oauth/token`

```
{
  "grant_type": "refresh_token",
  "refresh_token": "xxx"
}
```

In the response, you'll receive a new bearer token to use when accessing the API.

### Using X-Spree-Order-Token header (for Guest Checkout)

Endpoints under `/api/v2/storefront/cart` and `/api/v2/storefront/checkout` paths also allow interactions without bearer token, which allows building guest checkouts.

When you first create a cart via `POST /api/v2/storefront/cart`, you'll receive a response containing an empty cart. This response also contains a `token` field.&#x20;

You can store this token in the frontend session and pass it in a `X-Spree-Order-Token: {token}` header.&#x20;
