# On Approve Tokenize/Vault

Callback used to signal buyer approval of a tokenization/vault

## Examples

### Send Payment Method Token to server

```javascript
const onApprove = (data, actions) => {
    return fetch('/api/paypal/token/save', {
        method: 'POST',
        body: JSON.stringify({
            paymentMethodToken: data.paymentMethodToken
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
    paymentMethodToken : string
};

type OnApproveActions = {

};
```
