# Create Subscription

Callback used to create a subscription id, for any case involving a subscription.

This callback will be invoked whenever the user takes an action which requires a subscription context, e.g.

- Clicking a payment button

## Examples

### Create subscription from client

```javascript
const createSubscription = (data, actions) => {
    return actions.subscription.create({
        __TBD__: 'TBD'
    });
}
```

### Create subscription from server

```javascript
const createSubscription = (data, actions) => {
    return fetch('/api/paypal/subscription', {
        method: 'POST'
    }).then(res => {
        return res.json();
    }).then(json => {
        return json.subscriptionID;
    });
};
```

## Types

```typescript
type CreateSubscription = (
    data : CreateSubscriptionData,
    actions : CreateSubscriptionActions
) => SubscriptionID | Promise<SubscriptionID>;

type CreateSubscriptionData = {
    fundingSource : FUNDING
};

type CreateSubscriptionActions = {
    subscription : {
        create : ({
            // See https://developer.paypal.com/docs/subscriptions/integrate/
        }) => SubscriptionID
    }
};

type SubscriptionID = string;
```
