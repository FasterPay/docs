# About FasterPay
[FasterPay](https://auth.passport.io/?client_id=fasterpay) is introducing the new standard of a digital payments solution. FasterPay offers merchants from all areas and of all sizes exclusive features not found with any other digital payment solution such as:

● Multiple currency processing, storing and receiving.

● Quick and cheap withdrawals to any bank account.

● Competitive rates.

● Easy integration.

Alongside serving your business its essential needs such as:

● Recurring billing

● Mass payouts to individual and suppliers.

● Risk tools included in your account.

● 24/7 customer service.


# Prerequisite

Before Starting the project please make sure you had created a Faster Pay account and submitted all required documents with details. If not done yet please [click here](https://my.passport.io/account/).After setting up the account please take a note of below details :

● Your API Keys(Publick Key, Private Key)[ Direct URL to reach the page]

● You have hosted a success page and you have the URL where Customer will get redirected after success transaction.

# Integration

To give best customers expirence and ease out the development efforts FasterPay can be integrated in two simple options. FasterPay is designed to fit inside any website and help merchants to monetise the projects with minimum possible efforts.


**Option 1: Pay Button**

Here if you pass details like Amount, Product description and Success URL, that much will be suffisgient. Sucess URL is the URL where the user will be redirected after completion of the trasnction. you can show them one payment button to intitiate FasterPay transaction. Payment button is a javscript which will collect all the details and pass it on FasterPay.  

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
      

Button size can be Small, Medium and large and that can be managed by passing diffrent size codes.
    

**Option 2: Custom Integration**

Custome integration allows you to redirect your customer directly to our FasterPay Page. It is a browser to browser call where on selcting FasterPay option inside the checkout page of merchant website their customer will be redirected to FasterPay Page.

**Method**

HTTP POST

**URL**

https://pay.fasterpay.com/payment/form

**Parameters**

<table _ngcontent-c17="" class="data-table">
                    <thead _ngcontent-c17="">
                    <tr _ngcontent-c17="">
                        <th _ngcontent-c17="">Field</th>
                        <th _ngcontent-c17="">Required</th>
                        <th _ngcontent-c17="">Description</th>
                        <th _ngcontent-c17="">Example</th>
                    </tr>
                    </thead>

                    <tbody _ngcontent-c17="">
                    <!----><tr _ngcontent-c17="">
                        <td _ngcontent-c17="">amount</td>
                        <td _ngcontent-c17="">Yes</td>
                        <td _ngcontent-c17="">Payment amount in xxxx.yy format</td>
                        <td _ngcontent-c17="">9999.99</td>
                    </tr><tr _ngcontent-c17="">
                        <td _ngcontent-c17="">currency</td>
                        <td _ngcontent-c17="">Yes</td>
                        <td _ngcontent-c17="">Payment currency in ISO 4217 format</td>
                        <td _ngcontent-c17="">EUR</td>
                    </tr><tr _ngcontent-c17="">
                        <td _ngcontent-c17="">api_key</td>
                        <td _ngcontent-c17="">Yes</td>
                        <td _ngcontent-c17="">Your Public Key</td>
                        <td _ngcontent-c17="">xxxxyyyy</td>
                    </tr><tr _ngcontent-c17="">
                        <td _ngcontent-c17="">merchant_order_id</td>
                        <td _ngcontent-c17="">Yes</td>
                        <td _ngcontent-c17="">Your identifier of the payment, pass-through parameter</td>
                        <td _ngcontent-c17="">order_12345</td>
                    </tr><tr _ngcontent-c17="">
                        <td _ngcontent-c17="">description</td>
                        <td _ngcontent-c17="">Yes</td>
                        <td _ngcontent-c17="">Product description</td>
                        <td _ngcontent-c17="">Golden Ticket</td>
                    </tr><tr _ngcontent-c17="">
                        <td _ngcontent-c17="">success_url</td>
                        <td _ngcontent-c17="">No</td>
                        <td _ngcontent-c17="">Where a user should be redirected after successful payment</td>
                        <td _ngcontent-c17="">https://mycompany.com/thankyou</td>
                    </tr><tr _ngcontent-c17="">
                        <td _ngcontent-c17="">hash</td>
                        <td _ngcontent-c17="">No</td>
                        <td _ngcontent-c17="">Security hash calculated using your Private Key for preventing changing the parameters. Calculation algorithm is described below</td>
                        <td _ngcontent-c17="">xxxyyyy</td>
                    </tr>
                    </tbody>
                </table>
                
**Calculation algorithm for hash:**


hash = SHA256("PARAM_NAME_1=PARAM_VALUE_1PARAM_NAME_2=PARAM_VALUE_2PARAM_NAME_3=PARAM_VALUE_3...PRIVATE_KEY")
The additional parameters (e.g. PARAM_NAME_1=PARAM_VALUE_1PARAM_NAME_2=PARAM_VALUE_2) should be sorted alphabetically by the parameter name prior to hash calculation.
```
    <?php
    $params = ksort($parameters);
    $hash = hash('sha256', http_build_query($parameters) . $private_key);
    ?>
```

# 2. Listen to FasterPay Pingbacks.

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
