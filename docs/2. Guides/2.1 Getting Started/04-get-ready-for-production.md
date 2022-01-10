# Getting ready for Production

## 1. Sign up and log in to the Settle Business Portal

1. Go to https://business.settle.eu/signup/

2. Fill in the following information:

    - Country of Business
    - Given name
    - Surname

3. Click the `Proceed` button

4. Next, fill in the following information:

    - Phone number
    - Email address
    - Choose a password

4. Confirmations

Confirm that you have read, understood and agree
to the [Settle for Business Agreement](https://business.sandbox.settle.eu/static/pdf/MerchantAgreement.pdf) and [Privacy Policy](https://settle.eu/privacy-policy/), and that you agree to be bound by the Settle Merchant Agreement and/or confirm that you have the authority to bind any legal entity that you are representing.

6. Click the `Sign up` button.

####

## 2. Describe your Business

1. To complete your registration we need your company details.

    - Company Number
    - Legal Name of Company
    - Who owns the company

2. Click the `Register` company button.

####

## 3. Create you first Shop

Once your company has been registered you must set up at least one Shop.

> #### Note
>
> `Company` may also be referred to as `Legal Entity` or `Merchant`. It all means the formal, legal party that enters into the Merchant Agreement, who owns the bank account that will receive settlements, and the party that legally provides the products or services to Customers. Each Legal Entity must have at least one Shop configured with Settle. The concept of a Shop in our system enables a Company to have many different places and ways to do business.

  ##### 1. Fill in the following information:
  - Shop Name
  - Shop Type
  - Shop Location

    > #### Note
    >
    > You can also upload your Shop logo and provide additional information that is used across the Settle experience for your Customers. If you have existing software or hardware that is provided by one of our Integration Partners, you can select it from the drop-down. Doing so will create a relationship in our system between your Shop and the Integration Partner, enabling them to assist you in further configurations and enable Settle in the software or hardware they provide.

  ##### 2. Click the `Create your shop` button.

####

## 4. Create API Credentials

Once you have signed up in our production environment you need to create API Credentials for your Merchant.

1. Navigate to the Business Portal and follow the instructions below.

    1. In the menu on the left click Integration and then Add key.
    2. In the pop up window, give this key a name (for example ‘Test key’) and choose what type of API authentication method you want to use. You can choose to authenticate using keys you generate yourself. Keys that Settle generates for you, or simply a shared secret.

        > #### Note
        >
        > Some API calls require a higher level of authentication than a shared secret, so we recommend using RSA2(SHA256) Signature keys for all API calls.

    
##### RSA2(SHA256) Signature keys: RSA2 key value

To add a new RSA2 signature, take one of the following steps:

- Prepare an RSA2 key pair and click `Add Key` > `Use your own API keys` > `Add` to upload the public key.
- Click `Add Key` > `Generate API Keys` > `Add`.

####

## 5. Download the Settle Consumer App

We highly recommend you test your integration from a Customer perspective.

> #### Note
>
> A common mistake is to use production applications with Sandbox and vice versa. There is no interoperability between environments. Make sure you test with the Sandbox mobile app and in the Sandbox environment before you also test production equivalents of both server and client side. If you don't have access to the production mobile app due to jurisdictional limitations, please seek help from the community or our experts to make sure you get an end-to-end test run in a contained production environment before you go live.

