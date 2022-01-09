# Verifying Callback Signatures with Node.js

To work with incoming webhooks, an application that listens on HTTP POST requests sent from Settle is needed. It is also necessary that this application is accessible from the Internet.
This article presents a simple webhooks server example.

> #### Watch Out!
>
> We strongly advise you **NOT** to use ngrok in a production environment.

 

## Dependencies
This example use the [Settle SDK for Node.js](./ZG9jOjM0NzQwMDM1-settle-sdk-node) to handle signing and authorization, and [Express.js](https://expressjs.com/) to create a HTTP endpoint to verify signatures of incoming callbacks from Settle.

Also, for local development purposes, a tunneling service is required. This example uses [ngrok](https://ngrok.com/) and [Node wrapper for ngrok](https://github.com/bubenshchykov/ngrok).

```
npm i settle-sdk-node express ngrok
```

You can download ngrok here: https://ngrok.com/download.

 

## Example
This example is set to use the default demo data included in the Settle SDK for Node.js. To use your own values see the reference docs.

```
const {handler, merchant} = require('settle-sdk-node')
const express = require('express');
const ngrok = require('ngrok');

const app = express();
const dateTime = Date.now();

const customer = '4798765432' // do not use 47 or 00 before country code.
app.use(handler('sandbox'))

app.post('/', (req, res, next) => {
    console.log('Settle says: ', req.body);
    res.sendStatus(200);
});

app.listen(9000, () => console.log('Node.js server started on port 9000.'));

(async function () {
    let callbackUri = await ngrok.connect({addr: 9000});
    callbackUri = callbackUri + '/';

    merchant.payment.request.create({
        "action": "SALE",
        "allow_credit": true,
        "amount": 10000,
        "currency": "NOK", // Use the currency approved for your merchant.
        "customer": customer,
        "pos_id": "443435",
        "pos_tid": `tid_${dateTime}`,
        "text": "Bananas",
        "success_return_uri": "https://www.youtube.com/watch?v=wCkerYMffMo",
        "failure_return_uri": "https://www.youtube.com/watch?v=NlR4lv4Gvqk&t=1s",
        "callback_uri": callbackUri
    })
        .then(success => {
                console.log(success);
                let content = JSON.parse(success.content);
                // console.log(content.id)
                tid = content.id
            }, failure => {
                console.log(failure);
            }
        );
})();
```

### Usage

```bash title="Start the server with"
node index.js
```

This starts the server and tells ngrok to listen on port 9000.