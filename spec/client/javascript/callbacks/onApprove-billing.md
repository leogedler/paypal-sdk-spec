# On Approve Billing

Callback used to signal buyer approval of a billing agreement

## Examples

### Create Billing Agreement from Server

```javascript
const onApprove = (data, actions) => {
    return fetch('/api/paypal/billing/create', {
        method: 'POST',
        body: JSON.stringify({
            billingToken: data.billingToken
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
    billingToken : string,
    payerID : string
};

type OnApproveActions = {

};
```
