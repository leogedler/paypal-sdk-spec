## Step-by-step multi card fields integration with custom button

### Basic integration

#### 1. Add the JS SDK script tag

```HTML
<script src="https://www.paypal.com/sdk/js?client-id=test&components=card-fields&intent=capture"></script>
```

#### 2. Create container elements for each field and the custom button

```HTML
    <div id="multi-card-fields">
        <div id="card-number-field-container"></div>
        <div id="card-expiry-field-container"></div>
        <div id="card-cvv-field-container"></div>
        <button id="button" type="button">Submit</button>
    </div>
```

```js
    const cardNumberContainer = document.getElementById('card-number-field-container');
    const cardCvvContainer = document.getElementById('card-cvv-field-container');
    const cardExpiryContainer = document.getElementById('card-expiry-field-container');
    const button = document.getElementById('button');
```

#### 3. Initialize the parent cardFields component and pass in createOrder and onApprove

```js
    const cardFields = paypal.CardFields({
        createOrder: (data, actions) => {

            // Create the order on your server and return the order id

            return fetch('/api/paypal/order/create/', {
                method: 'post'
            }).then((res) => {
                return res.json();
            }).then((orderData) => {
                return orderData.id;
            });

        },
        onApprove: (data, actions) => {
            const { orderID } = data;

            // Capture the order on your server with `orderID`

            return fetch(`/api/paypal/order/${orderID}/capture/`, {
                method: 'post'
            }).then((res) => {
                return res.json();
            }).then((orderData) => {

                console.log("Payment approved and captured: ", orderData);

                // Handle successful transaction

            }).catch((error) => {
                
                // Handle error

            });
        },
    });
```

#### 4. Initialize card fields components, call render for each field, and pass in the styles object

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
        cardFields.submit().then(() => {

            // Success

        }).catch((error) => {

            // Handle error

        });
    });
```