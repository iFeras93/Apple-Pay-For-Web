# Apple-Pay-For-Web
Integration with apple pay for web using js

----------------

using the apple reference pages here https://developer.apple.com/reference/applepayjs

----------------
Steps:
Follow the steps on this page to set up and configure Apple Pay.

Before you start
Before you get started with Apple Pay, you need the following:

- An Apple Developer account. https://developer.apple.com/programs/enroll/
- A domain with a valid SSL certificate (meaning your domain should start with https test it using https://www.ssllabs.com/ssltest).
- Access to a Secure Shell (SSH) terminal.
- Access to your server's files, so you can upload files to your server.



# Configure Apple Pay

### Step 1: Create your merchant IDs in your Apple Pay Developer account
( [Tutorial](https://www.youtube.com/watch?v=tyleAQpV3pg) )

> We recommend that you create separate merchant IDs for your test environment and for your live/production environment.

- In your Apple Developer account, go to the Add Merchant IDs section, select Merchant IDs and select Continue.
- Add a useful description, like "_merchant id for test environment_".
- Type your desired merchant ID name in the Identifier section. We recommend that you use a descriptive name to indicate both the domain and the environment you will use it in, like "_merchant.com.mywebsite.sandbox_".

### Step 2: Create a Payment Processing Certificate

A payment processing certificate is associated with your merchant identifier and used to encrypt payment information. The payment processing certificate expires every 25 months. If the certificate is revoked, you can recreate it.

use this link to create the certificate: ( [Apple Help](https://help.apple.com/developer-account/#/devbfa00fef7?sub=devf31990e3f) )

- In the Apple Pay Payment Processing Certificate section (make sure you're not in the Apple Pay Merchant Identity Certificate section), select Create Certificate.
- Respond No to the question about processing in China and select Continue.
- Upload the .csr file from earlier and select Continue.
- Select Download to get your .cer file.
- When you have completed the instructions from Apple, add the merchant identity certificate to your keychain.
- Export the certificate from your keychain as a p12 file.

> For _Payfort_ you will convert the downloaded certificate to p12 file and upload it into apple pay setting tab inside you account.


### Step 3: Validate your domain

- Log in to your Apple Developer account, go to the Merchant IDs list section and select the merchant ID you created in step 1.
- Under the Merchant Domains section, select Add Domain.
- Enter your domain and select Save.
- Select Download and you'll get a .txt file.
> Upload this file to your server so it's accessible at the following location (replacing yourdomain.com with the URL of your domain): https://yourdomain.com/.well-known/apple-developer-merchantid-domain-association.txt. To do this, create a folder called .well-known in the root directory of your website and put the .txt file in that folder.

- Once you've uploaded the file, select Verify.


### Step 4: Create your Apple Pay certificates
( [Tutorial](https://www.youtube.com/watch?v=3jcQ4qkR8xU) )

> Use your Mac Keychain or you teminal to create the certificate

- Open a terminal and create a .csr and .key file using this command:

```
openssl req -out uploadMe.csr -new -newkey rsa:2048 -nodes -keyout certificate_sandbox.key
```

- In the prompt, enter your details, and when asked for a password, leave it blank and select Enter. You will get a .csr and .key file. Keep the .key file at hand.

- Sign in to your Apple Developer account, go to the Merchant IDs list section and select the merchant ID you created in step 1.

- Under the Apple Pay Merchant Identity Certificate section (make sure you're not in the Apple Pay Payment Processing Certificate section), select Create Certificate.

- Upload the .csr file you just created from your terminal. It should be called uploadMe.csr if you copy-pasted the command.

- Select Continue and then Download to get your .cer file. It will probably be named merchant_id.cer.

- Convert this .cer file into a .pem file so you can use it in your code. Enter the following command in your terminal:

```
openssl x509 -inform der -in merchant_id.cer -out certificate_sandbox.pem
```


upload the certificates to you site and this certificate used to verifying 

#### h4 Once you've completed the integration steps, you will be able to display the Apple Pay button and validate an Apple Pay Session (required for the web version).

Referances:
- [Checkout.com](https://www.checkout.com/docs/payments/payment-methods/wallets/apple-pay/set-up-apple-pay)
- [Moyasar.com](https://moyasar.com/docs/tutorials/apple-pay-setup/)
- [norfolkmustard/ApplePayJS](https://github.com/norfolkmustard/ApplePayJS)

