# When to Mock

Mock at system boundaries only:

- External APIs
- Databases when a real test database is not practical
- Time and randomness
- File system interactions when isolation matters

Do not mock:

- Your own modules
- Internal collaborators
- Code you control and can run directly in tests

## Designing for Mockability

Use dependency injection at boundaries.

```typescript
// Easy to mock
function processPayment(order, paymentClient) {
  return paymentClient.charge(order.total);
}

// Hard to mock
function processPayment(order) {
  const client = new StripeClient(process.env.STRIPE_KEY);
  return client.charge(order.total);
}
```

Prefer specific SDK-style interfaces over generic fetch wrappers.

```typescript
// GOOD
const api = {
  getUser: (id) => fetch(`/users/${id}`),
  getOrders: (userId) => fetch(`/users/${userId}/orders`),
  createOrder: (data) => fetch('/orders', { method: 'POST', body: data }),
};

// BAD
const api = {
  fetch: (endpoint, options) => fetch(endpoint, options),
};
```

Specific boundary functions make test setup simpler and reduce conditional mock logic.
