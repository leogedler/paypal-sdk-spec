# Create Billing Agreement

Callback used to create an billing agreement token, for any case involving a billing agreement.

This callback will be invoked whenever the user takes an action which requires a billing context, e.g.

- Clicking a payment button

## Examples

### Create billing agreement from server

```javascript
const createBillingAgreement = (data, actions) => {
    return fetch('/api/paypal/billing-agreement', {
        method: 'POST'
    }).then(res => {
        return res.json();
    }).then(json => {
        return json.billingToken;
    });
};
```

## Types

```typescript
type CreateBillingAgreement = (
    data : CreateBillingAgreementData,
    actions : CreateBillingAgreementActions
) => BillingToken | Promise<BillingToken>;

type CreateBillingAgreementData = {
    fundingSource : FUNDING
};

type CreateBillingAgreementActions = {

};

type BillingToken = string;
```
