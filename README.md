**Table of Contents**
- [About FasterPay](#about-fasterpay)
- [Prerequisite](#prerequisite)
- [Integration](#integration)
    - [Pay Button Integration](#pay-button-integration)
        - [Pay Button Integration Parameters](#pay-button-integration-parameters)
        - [Pay Button Integration Example](#pay-button-integration-example)
    - [Custom Integration](#custom-integration)
        - [Custom Integration Parameters](#custom-integration-parameters)
        - [Custom Integration Example](#custom-integration-example)
        - [Hash Calculation Algorithm](#hash-calculation-algorithm)
- [Pingbacks](#pingbacks)

## About FasterPay

[FasterPay](https://www.fasterpay.com) is introducing the Simpler, Faster, Global, E-Wallet for your business.

## Prerequisite

Before integrating FasterPay, please **Sign Up** at **[https://business.fasterpay.com](https://business.fasterpay.com)** and complete your **Business Model** and **Business Profile**. After your **Business Model** and **Business Profile** are verified you can follow the **[Integration Documentation](https://business.fasterpay.com/dashboard/#/integration-doc)**.

**Please note that the verification process might take around 24h.**

## Integration

FasterPay could be integrated by using the **[Pay Button Integration](#pay-button-integration)** or **[Custom Integration](#custom-integration)**.

### Pay Button Integration

Pay Button is a simple way to integrate FasterPay widget by adding the script to your page and providing the required parameters from the table below.

#### Pay Button Integration Parameters

| Parameter   | Required | Description                                                                             | Example                                |
| ----------- | -------- | --------------------------------------------------------------------------------------- | -------------------------------------- |
| src         | Yes      | FasterPay pay.js library                                                                | https://pay.fasterpay.com/pay.js       |
| amount      | Yes      | Payment amount in 0000.00 format                                                        | 42.00                                  |
| currency    | Yes      | Payment currency in [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) format | USD                                    |
| description | Yes      | Product description                                                                     | Your product description               |
| merchant    | Yes      | Public key                                                                              | rg2ji4cwmqmxpe3hbkt6j9rydvx748jm       |
| success_url | No       | Success page URL                                                                        | https://yourcompanywebsite.com/success |
| size        | No       | Pay Button size ("sm", "md" or "lg")                                                    | lg                                     |

#### Pay Button Integration Example

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>FasterPay Pay Button Integration</title>
</head>
<body>
    <script
        src="https://pay.fasterpay.com/pay.js"
        amount="42.00"
        currency="USD"
        description="Your product description"
        merchant="rg2ji4cwmqmxpe3hbkt6j9rydvx748jm"
        success_url="https://yourcompanywebsite.com/success"
        size="lg">
    </script>
</body>
</html>
```

### Custom Integration

Custom Integration allows you to redirect your customer directly to the FasterPay widget. It is a browser to browser call where on selecting FasterPay option on the checkout page of your website the customer is redirected to the FasterPay widget.

#### Custom Integration Parameters

| Parameter         | Required | Description                                                                             | Example                                |
| ----------------- | -------- | --------------------------------------------------------------------------------------- | -------------------------------------- |
| amount            | Yes      | Payment amount in 0000.00 format                                                        | 42.00                                  |
| currency          | Yes      | Payment currency in [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) format | USD                                    |
| description       | Yes      | Product description                                                                     | Your product description               |
| api_key           | Yes      | Public key                                                                              | rg2ji4cwmqmxpe3hbkt6j9rydvx748jm       |
| merchant_order_id | Yes      | Identifier of the payment                                                               | order_1                                |
| email             | No       | Email                                                                                   | john.doe@email.com                     |
| first_name        | No       | First name                                                                              | John                                   |
| last_name         | No       | Last name                                                                               | Doe                                    |
| city              | No       | City                                                                                    | Anytown                                |
| zip               | No       | ZIP                                                                                     | 00000                                  |
| success_url       | No       | Success page URL                                                                        | https://yourcompanywebsite.com/success |
| hash              | No       | [Hash](#hash-calculation-algorithm)                                                     | rg2ji4cwmqmxpe3hbkt6j9rydvx748jm       |

#### Custom Integration Example

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>FasterPay Custom Integration</title>
</head>
<body>
    <form action="https://pay.fasterpay.com/payment/form" method="post">
        <input type="hidden" name="amount" value="42">
        <input type="hidden" name="currency" value="USD">
        <input type="hidden" name="description" value="Your product description">
        <input type="hidden" name="api_key" value="rg2ji4cwmqmxpe3hbkt6j9rydvx748jm">
        <input type="hidden" name="merchant_order_id" value="order_1">
        
        <input type="hidden" name="email" value="john.doe@email.com">
        <input type="hidden" name="first_name" value="John">
        <input type="hidden" name="last_name" value="Doe">
        <input type="hidden" name="city" value="Anytown">
        <input type="hidden" name="zip" value="00000">
        <input type="hidden" name="success_url" value="https://yourcompanywebsite.com/success">
        <input type="hidden" name="hash" value="rg2ji4cwmqmxpe3hbkt6j9rydvx748jm">

        <button type="submit">Pay</button>
    </form>
</body>
</html>
```

#### Hash Calculation Algorithm

hash = SHA256("PARAM_NAME_1=PARAM_VALUE_1&PARAM_NAME_2=PARAM_VALUE_2&PARAM_NAME_3=PARAM_VALUE_3&PARAM_NAME_4=PARAM_VALUE_4&PARAM_NAME_5=PARAM_VALUE_5&PARAM_NAME_6=PARAM_VALUE_6Private_Key")

Sample Hash parameters String (amount=10&api_key=Your API Key&currency=USD&description=testing_product&merchant_order_id=Unique ID&success_url=Merchant Hosted URLYour Project Private key) should be sorted alphabetically by the parameter name prior to hash calculation.

```
<?php
$params = ksort($parameters);
$hash = hash('sha256', http_build_query($parameters) . $private_key);
?>
```

## Pingbacks

Pingback request is sent from our servers to your Pingback listener script where we communicate to your server regarding the details about payment transactions so that your server can process the pingback automatically and deliver the goods to the respective users.

**Authentication**

Header

X-ApiKey: $YOUR_PRIVATE_KEY

**Method**

HTTP POST

**URL**

Your Pingback URL

**Expected Body in Pingback Response**

```
{  
   "event": "payment",
   "payment_order": {
      "id": 1005002001,
      "merchant_order_id": "w146138485",
      "status": "successful",
      "paid_amount": 5,
      "paid_currency": "USD",
      "merchant_net_revenue": 4.23,
      "merchant_rolling_reserve": 0.25,
      "fees": 0.52,
      "date": {
         "date": "2018-04-25 12:15:07.000000",
         "timezone_type": 3,
         "timezone": "UTC"
      }
   },
   "user": {
      "firstname": "John",
      "lastname": "Doe",
      "username": "john-doe@my.passport.io",
      "country": "TR",
      "email": "john.doe@email.com"
   }
}
```
