# Gateway-documentation
walletmix v_2 Gateway Documentation

### 1. Objective of the document
This document will serve as a guide for developers/merchants who want to integrate Walletmix Payment Gateway for performing real time transaction verification against relevant services or banks. This will assist the merchants to prepare their infrastructure for integration with Walletmix Gateway.

### 2. BasicCallFlow
- To use the payment gateway service merchant need to register Walletmix payment gateway service using a registration form. After successful registration merchant will get a Merchant ID, Access App Key, Service access user name and password provided by Walletmix Limited.
- Customer will place an order like checkout from merchant’s website.
- All transaction related data will be stored in merchant’s database with auto increment unique order_id field. Example: order_id = 105.
- Then Merchant have to check server status to invoke “check-server”.
- Merchant will use the Walletmix Provided Merchant ID, Access App Key, Service access user name, password and that transaction related data to invoke “init-payment- process”. When invoke to “init-payment-process” Merchant will get a response of unique token against transaction related data after authentication & some validation; otherwise the merchant will get an error code and message.
- Merchant will forward a URL using GET method with that token and Customer will confirm the payment.
- After completing success or fail transaction it will forward to merchant callback URL with that token and transaction status.
- Don’t trust this parameters. Merchant will have to again check transaction status to invoke “check-payment” with Merchant ID, Access App Key, Service access user name, password and that token.
- Then merchant will get a response of that transaction status
- Depending on the provided status can be updated in your database with that order_id. Example: order_id = 105

### 3. Check Server Status
###     3.1 Get Server Details
Method: GET
Request URL: http://epay.walletmix.com/check-server
Response:
{"selectedServer": true,"url": "https://epay.walletmix.com/init-payment-process","bank_payment_url":"https://epay.walletmix.com/bank-payment-process"}
