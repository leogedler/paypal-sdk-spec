# On Approve Order

Callback used to signal buyer approval of a purchase, e.g.

- Successfully entering a card and submitting it
- Clicking on a button and approving a payment

## Examples

### Get order details from client

```javascript
const onApprove = (data, actions) => {
    return actions.order.get().then(details => {
        // Display details to buyer
    });
}
```

### Capture order from client

```javascript
const onApprove = (data, actions) => {
    return actions.order.capture().then(() => {
        // Show a success page
    });
}
```

### Authorize order from client

```javascript
const onApprove = (data, actions) => {
    return actions.order.authorize().then(() => {
        // Show a success page
    });
}
```

### Capture order from server

```javascript
const onApprove = (data, actions) => {
    return fetch('/api/paypal/order/capture', {
        method: 'POST',
        body: JSON.stringify({
            orderID: data.orderID
        })
    }).then(res => {
        return res.json();
    }).then(json => {
        // Show a success page
    });
};
```

### Authorize order from server

```javascript
const onApprove = (data, actions) => {
    return fetch('/api/paypal/order/authorize', {
        method: 'POST',
        body: JSON.stringify({
            orderID: data.orderID
        })
    }).then(res => {
        return res.json();
    }).then(json => {
        // Show a success page
    });
};
```

## Types

```typescript
type OnApprove = (
    data : OnApproveData,
    actions : OnApproveActions
) => undefined | Promise<undefined>

type OnApproveData = {
    orderID : string,
    payerID? : string
};

type OnApproveActions = {
    order : {
        get : () =>
            Promise<GetOrderResponse>,
        capture : (CaptureOrderOptions) =>
            Promise<CaptureOrderResponse>,
        authorize : (AuthorizeOrderOptions) =>
            Promise<AuthorizeOrderResponse>,
    }
};

type GetOrderResponse = {};
type CaptureOrderOptions = {};
type CaptureOrderResponse = {};
type AuthorizeOrderOptions = {};
type AuthorizeOrderResponse = {};
```

### References

- [GetOrderResponse](https://developer.paypal.com/docs/api/orders/v2/#orders-get-response);
- [CaptureOrderOptions](https://developer.paypal.com/docs/api/orders/v2/#orders_capture);
- [CaptureOrderResponse](https://developer.paypal.com/docs/api/orders/v2/#orders-capture-response);
- [AuthorizeOrderOptions](https://developer.paypal.com/docs/api/orders/v2/#orders_authorize);
- [AuthorizeOrderResponse](https://developer.paypal.com/docs/api/orders/v2/#orders-authorize-response);
