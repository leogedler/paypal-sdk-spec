## Step-by-step single card fields with custom button integration

### Basic integration

#### 1. Add the JS SDK script tag

```HTML
<script src="https://www.paypal.com/sdk/js?client-id=test&components=card-fields&intent=capture"><script>
```

#### 2. Create container elements for the fields and the button

```HTML
    <div id="card-field-container"></div>

    <button id="button" type="button">Pay now</button>
```

```js
    const cardContainer = container.querySelector("#card-field-container");
    const button = buttonContainer.querySelector("#button");
```

#### 3. Initialize cardFields component passing createOder and onApprove and call render

```js
    const cardField = paypal.CardFields({
        createOrder: (data, actions) => {
            return actions.order.create({

                // Pass in the order object

            })
        },
        onApprove: (data) => {
            console.log("Payment Approved: ", data, actions);
            const { orderID } = data;

            // Capture the order in your server with order ID `orderID`
        },
        onChange: ({ isValid, errors }) => {
          console.log('onchange: ', isValid, errors);
        },
    }).render(cardContainer);

```

#### 4. Add click listener to custom button

```js
    button.addEventListener("click", () => {

        cardField.submit().then(() => {

            // Success

        }).catch((error) => {

            // Handle error

        });
    });
```