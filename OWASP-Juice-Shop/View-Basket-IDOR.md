# OWASP Juice Shop - View Basket Challenge (IDOR)

## Objective

Understand how the shopping basket API works and test whether it properly enforces access control.

## Recon

While interacting with the checkout process, I noticed the following API request:

```http
GET /rest/basket/6
```

Based on the endpoint name, I assumed that `6` represented the Basket ID.

## Hypothesis

If the application relies only on the Basket ID without verifying ownership, changing the ID might allow access to another user's shopping basket.

## Testing

I modified the request from:

```http
GET /rest/basket/6
```

to:

```http
GET /rest/basket/5
```

## Result

The server returned a different shopping basket containing:

- Basket ID
- User ID
- Products
- Product Quantity

This successfully solved the Juice Shop challenge:

> **View another user's shopping basket**

## Key Takeaways

- Always understand the application's workflow before testing.
- Pay close attention to IDs exposed in API endpoints.
- Build a hypothesis before modifying requests.
- This challenge demonstrates the basics of **Broken Access Control (IDOR)**.
