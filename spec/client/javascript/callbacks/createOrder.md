# Create Order

Callback used to create an order id, for any case involving a purchase.

This callback will be invoked whenever the user takes an action which requires an order context, e.g.

- Clicking a payment button
- Submitting card fields

## Examples

### Create order from client

```javascript
const createOrder = (data, actions) => {
    return actions.order.create({
        purchase_units: [{
            amount: {
                value: '0.01'
            }
        }]
    });
}
```

### Create order from server

```javascript
const createOrder = (data, actions) => {
    return fetch('/api/paypal/order', {
        method: 'POST'
    }).then(res => {
        return res.json();
    }).then(json => {
        return json.orderID;
    });
};
```

## Types

```typescript
type CreateOrder = (
    data : CreateOrderData,
    actions : CreateOrderActions
) => OrderID | Promise<OrderID>;

type CreateOrderData = {
    fundingSource : FUNDING
};

type CreateOrderActions = {
    order : {
        create : ({
            // See https://developer.paypal.com/docs/api/orders/v2/#orders_create
        }) => OrderID
    }
};

type OrderID = string;
```

## Notes

- Following params must match those passed to SDK:
  - [`currency`](../initialization.md#currency)
  - [`intent`](../initialization.md#intent)
- When using `actions.order.create`, these parameters are inherited from global SDK options.
