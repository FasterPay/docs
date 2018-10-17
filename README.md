# About FasterPay
[FasterPay](https://auth.passport.io/?client_id=fasterpay) is the leading digital payments ewallet for globally monetizing digital goods and services. Paymentwall assists game publishers, dating sites, rewards sites, SaaS companies and many other verticals to monetize their digital content and services. 
Merchants can plugin Paymentwall's API to accept payments from over 100 different methods including credit cards, debit cards, bank transfers, SMS/Mobile payments, prepaid cards, eWallets, landline payments and others. 

To sign up for a Paymentwall Merchant Account, [click here](https://my.passport.io/account/).

# Integration
To give best customers expirence and ease out the development efforts FasterPay can be integrated in two ways.

##Option 1: Pay Button
Here if you pass three details that is Amount, Product description and Success URL where the user will be redirected after completion of the trasnction. you can show them one payment button to intitiate FasterPay transaction. Payment button is a javscript which will collect all the details and pass it on FasterPay.  

## Code Samples 
<code> <script src="https://pay.fasterpay.com/pay.js"
          amount="99.99"
          currency="USD"
          description="Your Product Name"
          merchant="82b0c8a40c5d73ea08420816ec448d30"
          success_url=""
          size="lg">    // Small-sm, Medium-md
      </script></code>

Button size can be Small, Medium and large and that can be managed by passing diffrent size codes.
    
##Option 2: Custom Integration
Custome integration allows you to redirect your customer directly to our FasterPay Page. They can login nad 