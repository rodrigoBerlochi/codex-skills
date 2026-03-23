# Interface Design for Testability

Good interfaces make testing natural.

1. Accept dependencies instead of constructing them internally.

```typescript
// Testable
function processOrder(order, paymentGateway) {}

// Hard to test
function processOrder(order) {
  const gateway = new StripeGateway();
}
```

2. Prefer returning results over mutating hidden state when practical.

```typescript
// Easier to test
function calculateDiscount(cart): Discount {}

// Harder to inspect
function applyDiscount(cart): void {
  cart.total -= discount;
}
```

3. Keep the surface area small.

- Fewer methods means fewer behaviors to cover.
- Fewer parameters means simpler setup.
