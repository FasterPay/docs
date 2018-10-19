# About FasterPay
[FasterPay](https://www.fasterpay.com) is introducing the Simpler, Faster, Global, Better E-Wallet.

# Prerequisite

Before Starting the project please sign up at [business.fasterpay.com](https://business.fasterpay.com).  After providing the Business Details please take a note of below details:

● Your API Keys(Public Key, Private Key) [Here](https://business.fasterpay.com/dashboard/#/integration-doc)

● If you are not using an E-commerce plugin then make sure you have hosted a success page and you have the URL where customer will get redirected after success transaction.

# Integration

To give best customers experience and ease out the development efforts FasterPay can be integrated in two simple ways. FasterPay is designed to help merchants to monetize the projects with minimum possible efforts.


**Option 1: Pay Button**

Here you can make payments by passing minimum details like Amount, Product description and Success URL, Success URL is the URL where the customer will be redirected after completion of the transaction. you can show them one payment button to initiate FasterPay transaction. Payment button is a JavaScript which will collect all the details and pass it on FasterPay.  

## Code Samples 
 
```
<script src="https://pay.fasterpay.com/pay.js"
          amount="99.99"
          currency="USD"
          description="Your Product Name"
          merchant="82b0c8a40c5d73ea08420816ec448d30" //Publick Key
          success_url=""
          size="lg">    // Small-sm, Medium-md
      </script>
```
      

Button size can be Small, Medium and large and that can be managed by passing different size codes.
    

**Option 2: Custom Integration**

Custom integration allows you to redirect your customer directly to our FasterPay Page. It is a browser to browser call where on selecting FasterPay option inside the checkout page of merchant website their customer can be redirected to FasterPay.

**Method**

HTTP POST

**URL**

https://pay.fasterpay.com/payment/form

**Parameters**

| Field | Required | Description | Example |
|---|---|---|---|
| amount | Yes | Payment amount in xxxx.yy format | 9999.99 |
| currency | Yes | Payment currency in ISO 4217 format | EUR |
| api_key | Yes | Your Public Key | xxxxyyyy |
| merchant_order_id | Yes | Your identifier of the payment, pass-through parameter | order_12345 |
| description | Yes | Product description | Golden Ticket |
| success_url | No | Where a user should be redirected after successful paymentn | https://mycompany.com/thankyou |
| hash | No | Security hash calculated using your Private Key for preventing changing the parameters. Calculation algorithm is described below | xxxyyyy |
                
**Calculation algorithm for hash:**


hash = SHA256("PARAM_NAME_1=PARAM_VALUE_1&PARAM_NAME_2=PARAM_VALUE_2&PARAM_NAME_3=PARAM_VALUE_3&PARAM_NAME_4=PARAM_VALUE_4&PARAM_NAME_5=PARAM_VALUE_5&PARAM_NAME_6=PARAM_VALUE_6Private_Key")

Sample Hash parameters String (amount=10&api_key=Your API Key&currency=USD&description=testing_product&merchant_order_id=Unique ID&success_url=Merchant Hosted URLYour Project Private key) should be sorted alphabetically by the parameter name prior to hash calculation.
```
    <?php
    $params = ksort($parameters);
    $hash = hash('sha256', http_build_query($parameters) . $private_key);
    ?>
```

## Sample HTML Post Form

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2//EN">
 <html>
     <head>
         <meta HTTP-EQUIV="Content-Type" CONTENT="text/html;CHARSET=iso-8859-1">
 </head>
  <body>
    <form align="center" method="post" action="https://pay.fasterpay.com/payment/form">
       <input type="hidden" id="amount" name="amount" value="10" />
       <input type="hidden" id="currency" name="currency" value="USD" />
       <input type="hidden" id="api_key" name="api_key" value="Your API Key" />
       <input type="text" id="merchant_order_id" name="merchant_order_id" value="test_123" />
       <input type="text" id="description" name="description" value="testing_product" />        
       <input type="hidden" name="success_url" value="http://www.kushal.com" />
       <input type="hidden" id="hash" name="hash" value="f389594dd1a789a88715b00cd80567dd4df405c281fc1e41d2628883b72ccc38" />
       <input type="Submit" value="Pay Now"/>
     </form> 
    </body>
 </html> 
```
# 2. Listen to FasterPay Pingbacks.

Pingback request is sent from our servers to your Pingback listener script where we communicate to your server regarding the details about payment transactions so that your server can process the pingback automatically and deliver the goods to the respective users. To know more in details [click here](https://docs.paymentwall.com/reference/pingback-home)

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
        "lastname": "Smith",
        "username": "john-smith@my.passport.io",
        "country": "TR",
        "email": "john.smith@email.com"
      }
    }
```