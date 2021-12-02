## Step-by-step single card fields integration with custom button

### Basic integration

#### 1. Add the JS SDK script tag

```HTML
<script src="https://www.paypal.com/sdk/js?client-id=test&components=card-fields&intent=capture"></script>
```

#### 2. Create container elements for the field and the button

```HTML
    <div id="card-field-container"></div>
    <button id="button" type="button">Pay now</button>
```

```js
    const cardContainer = document.getElementById("card-field-container");
    const button = document.getElementById("button");
```

#### 3. Initialize the cardFields component, pass in createOrder, onApprove, and the styles object, and call render

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

    const cardField = paypal.CardFields({
        style: customStyles,
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
        onApprove: (data) => {
            const { orderID } = data;

            // Capture the order in your server with `orderID`

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
        onChange: ({ isValid, errors }) => {
          console.log('onchange: ', isValid, errors);
        },
    });
    
    cardField.render(cardContainer);

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