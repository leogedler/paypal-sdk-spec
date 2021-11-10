## Step-by-step multi card fields with custom button integration

### Basic integration

#### 1. Add the JS SDK script tag

```HTML
<script src="https://www.paypal.com/sdk/js?client-id=test&components=card-fields&intent=capture"><script>
```

#### 2. Create container elements for each fields and the custom button

```HTML
    <div id="multi-transactional-card-field">

        <div id="card-number-field-container"></div>

        <div id="card-expiry-field-container"></div>

        <div id="card-cvv-field-container"></div>

        <button id="button">Submit</button>

    </div>
```

```js
    const cardNumberContainer = container.querySelector('#card-number-field-container');
    const cardCvvContainer = container.querySelector('#card-cvv-field-container');
    const cardExpiryContainer = container.querySelector('#card-expiry-field-container');
    const button = buttonContainer.querySelector('#button');
```

#### 3. Initialize the parent cardFields component passing createOder and onApprove

```js
    const cardFields = paypal.CardFields({
        branded: false,
        createOrder: (data, actions) => {
            return actions.order.create({

                // Pass in the order object

            });
        },
        onApprove: (data, actions) => {
            console.log("Payment Approved: ", data, actions);
            const { orderID } = data;

            // Capture the order in your server with order ID `orderID`
        },
    });
```

#### 4. Initialize card fields components calling render for each field

```js
    cardFields.NumberField({
        onChange: ({valid, errors}) => {
            console.log('onchange number: ', valid, errors);
        }
    }).render(cardNumberContainer);

    cardFields.CVVField({
        onChange: ({valid, errors}) => {
            console.log('onchange cvv: ', valid, errors);
        }
    }).render(cardCvvContainer);

    cardFields.ExpiryField({
        onChange: ({valid, errors}) => {
            console.log('onchange expiry: ', valid, errors);
        }
    }).render(cardExpiryContainer);
```

#### 4. Add click listener to custom button

```js
    button.addEventListener('click', () => {

        cardField.submit().then(() => {

            // Success

        }).catch((error) => {

            // Handle error

        });
    });
```