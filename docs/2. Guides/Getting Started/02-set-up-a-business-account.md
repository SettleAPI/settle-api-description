# Set up a business account

## 1. The Settle Business Portal

This self-service portal covers enrolment and administration of a Settle business, such as setting up various pre-made acceptance methods (mainly meant for micro and small businesses) and viewing reports on incoming payments and settlement payouts.

On a technical level, a ‘Business’ may also be referred to as "Legal Entity" which means the formal, legal party that enters into an agreement with Settle, who owns the bank account that will receive settlements and the party that legally provides the products or services to Customers. Each Business must have at least one Shop configured with Settle. The concept of a Shop enables a Company to have many different locations and many different ways to do accept payments, without having to register a new business account.

> #### Example
>
>`ABC Trading Inc` sell shoes online under the brand `Sporty Boots` and all clients know them as `Sporty Boots`, so it makes sense to set up a Settle Shop named Sporty Boots. `Acme Trading Inc` also has a physical shop that is known as `Sporty Boots Outlet` and when they do event-based shoe sales at big sporting events they want to run that sales effort under the name `Sporty Boots at Superbowl`.

####

## 2. Create your Sandbox Account
To develop and test your integration you first need a business account. While no real documentation has to be provided during the sandbox enrollment, data input such as company number may still need to be formatted according to local convention.

> #### Note
>
> To accept payments or use other features of Settle for Business in production, you need to separately sign up in production.

1. Go to https://business.sandbox.settle.eu/signup/

2. Fill in the following information:

    - Country of Business
    - Given name
    - Surname

3. Click the `Proceed` button

4. Next, fill in the following information:

    - Phone number
    - Email address
    - Choose a password

5. Confirm that you have read, understood and agree to the [Settle for Business Agreement](https://business.sandbox.settle.eu/static/pdf/MerchantAgreement.pdf) and [Privacy Policy](https://settle.eu/privacy-policy/)
    and that you agree to be bound by the Settle Merchant Agreement and/or confirm that you have the authority to     bind any legal entity that you are representing.

6. Click the `Sign up` button.


## 3. Describe your Business

1. To complete your registration we need your company details.
    - Company Number
    - Legal Name of Company
    - Who owns the company

    > #### Note
    >
    > While no real documentation has to be provided during the sandbox merchant enrollment, data input such as company number may still need to be formatted properly according to local convention.

2. Click the `Register` company button.


## 4. Create your first Shop

Once your company has been registered you must set up at least one Shop.

1. Fill in the following information:
    - Shop Name
    - Shop Type
    - Shop Location

    > #### Note
    >
    > You can also upload your Shop logo and provide additional information that is used across the Settle experience for your Customers. If you have existing software or hardware that is provided by one of our Integration Partners, you can select it from the drop-down. Doing so will create a relationship in our system between your Shop and the Integration Partner, enabling them to assist you in further configurations and enable Settle in the software or hardware they provide.

2. Click the `Create your shop` button.
 

## 5. Create Sandbox API Credentials

Once you have signed up in our Sandbox environment you need to create API Credentials for your Test Merchant.

1. Navigate to the Sandbox Business Portal and follow the instructions below.

    1. In the menu on the left click Integration and then Add key.
    2. In the pop-up window, give this key a name (for example ‘Test key’) and choose what type of API authentication method you want to use. You can choose to authenticate using keys you generate yourself. Keys that Settle generates for you, or simply a shared secret.

    > #### Note
    >
    > Some API calls require a higher level of authirization than a shared secret, see [API Authentication](../merchant-api/ZG9jOjMyMjU5OTk2-api-authentication) levels for more information.

      #### RSA2(SHA256) Signature keys: RSA2 key value

      To add a new RSA2 signature, take one of the following steps:

      - Prepare an RSA2 key pair and click `Add Key` > `Use your own API keys` > `Add` to upload the public key.
      - Click `Add Key` > `Generate API Keys` > `Add`.