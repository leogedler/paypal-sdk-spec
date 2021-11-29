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
        createOrder: (data, actions) => {

            // Create the order in your server and return the order id

            return fetch('/api/paypal/order/create/', {
                method: 'post'
            }).then((res) => {
                return res.json();
            }).then((orderData) => {
                return orderData.id;
            });

        },
        onApprove: (data, actions) => {
            console.log("Payment Approved: ", data, actions);
            const { orderID } = data;

            // Capture the order in your server with order ID `orderID`

            return fetch(`/api/paypal/order/${orderID}/capture/`, {
                method: 'post'
            }).then((res) => {
                return res.json();
            }).then((orderData) => {

                // Handle Successful transaction

            }).catch((error) => {
                
                // Handle error

            });
        },
    });
```

#### 4. Initialize card fields components calling render for each field and passing the styles object

```js

    const customStyles = {
        height: "60px",
        padding: "10px",
        fontSize: "18px",
        fontFamily: '"Open Sans", sans-serif',
        transition: "all 0.5s ease-out",
        "input.invalid": {
            color: "red",
        },
    };

    cardFields.NumberField({
        style: customStyles,
        onChange: ({isValid, errors}) => {
            console.log('onchange number: ', isValid, errors);
        }
    }).render(cardNumberContainer);

    cardFields.CVVField({
        style: customStyles,
        onChange: ({isValid, errors}) => {
            console.log('onchange cvv: ', isValid, errors);
        }
    }).render(cardCvvContainer);

    cardFields.ExpiryField({
        style: customStyles,
        onChange: ({isValid, errors}) => {
            console.log('onchange expiry: ', isValid, errors);
        }
    }).render(cardExpiryContainer);
```

#### 5. Add click listener to custom button

```js
    button.addEventListener('click', () => {

        cardField.submit().then(() => {

            // Success

        }).catch((error) => {

            // Handle error

        });
    });
```