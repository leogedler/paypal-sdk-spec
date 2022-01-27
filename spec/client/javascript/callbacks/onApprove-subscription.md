# On Approve Subscription

Callback used to signal buyer approval of a subscription.

## Examples

### Get subscription details from client

```javascript
const onApprove = (data, actions) => {
    return actions.subscription.get().then(details => {
        // Display details to buyer
    });
}
```

### Activate subscription from client

```javascript
const onApprove = (data, actions) => {
    return actions.subscription.activate().then(() => {
        // Show a success page
    });
}
```

### Activate subscription from server

```javascript
const onApprove = (data, actions) => {
    return fetch('/api/paypal/subscription/activate', {
        method: 'POST',
        body: JSON.stringify({
            subscriptionID: data.subscriptionID
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
    subscriptionID : string
};

type OnApproveActions = {
    subscription : {
        get : () =>
            Promise<GetSubscriptionResponse>,
        activate : (ActivateSubscriptionOptions) =>
            Promise<ActivateSubscriptionResponse>
    }
};

type GetSubscriptionResponse = {};
type ActivateSubscriptionResponse = {};
```

### References

- [GetSubscriptionResponse](__TBD__);
- [ActivateSubscriptionResponse](__TBD__);
