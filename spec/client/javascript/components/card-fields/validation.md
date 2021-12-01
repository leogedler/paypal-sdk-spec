# Validation

## Single card field

### Vanilla Javascript

```javascript
paypal.CardFields({
    onChange: (data) => {
        cardContainer.className = data.isValid ? 'valid' : 'invalid';
    }
}).render(cardContainer);
```

### React

```javascript
const App = () => {
    const [ isValid, setValid ] = useState();

    const onChange = (data) => {
        setValid(data.isValid);
    };

    return (
        <div class="card-field-container" className={ isValid ? 'valid' : 'invalid' }>
            <PayPalCardFields onChange={ onChange } />
        </div>
    );
}
```

## Multiple card fields

### Vanilla Javascript

```javascript
const cardFields = paypal.CardFields();

cardFields.NumberField({
    onChange: (data) => {
        cardNumberContainer.className = data.isValid ? 'valid' : 'invalid';
    }
}).render(cardNumberContainer);

cardFields.CVVField({
    onChange: (data) => {
        cardCvvContainer.className = data.isValid ? 'valid' : 'invalid';
    }
}).render(cardCvvContainer);

cardFields.ExpiryField({
    onChange: (data) => {
        cardExpiryContainer.className = data.isValid ? 'valid' : 'invalid';
    }
}).render(cardExpiryContainer);
```

### React

```javascript
const App = () => {
    const [ numberValid, setNumberValid ] = useState();
    const [ cvvValid, setCVVValid ] = useState();
    const [ expiryValid, setExpiryValid ] = useState();

    const onChangeNumber = (data) => {
        setNumberValid(data.valid);
    };

    const onChangeCVV = (data) => {
        setCVVValid(data.valid);
    };

    const onChangeExpiry = (data) => {
        setExpiryValid(data.valid);
    };

    return (
        <PayPalCardFields>
            <div id="card-number-field-container" className={ numberValid ? 'valid' : 'invalid' }>
                <PayPalCardNumberField onChange={ onChangeNumber } />
            </div>
            <div id="card-cvv-field-container" className={ cvvValid ? 'valid' : 'invalid' }>
                <PayPalCardCVVField onChange={ onChangeCVV } />
            </div>
            <div id="card-expiry-field-container" className={ expiryValid ? 'valid' : 'invalid' }>
                <PayPalCardExpiryField onChange={ onChangeExpiry } />
            </div>
        </PayPalCardFields>
    );
}
```

## See also

- [Styling](./styling.md#style-card-fields)