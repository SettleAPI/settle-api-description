---
tags: [API Introduction]
---

# Callbacks

API clients can associate some resources with a `callback_uri` in order to enable asynchronous communication between the client and server.

When certain events occur, Settle can trigger a callback to the specified `callback_uri`. For instance, if the callback URL is an `https://` URL, a `POST` request will be made to the URL. The data sent with the callback is referred to as a **callback message** (or just **message**). The message consists of a **meta** part and an **object** part, the latter containing the actual message data, while the former is meta information about the callback.

> #### Info
>
> You do not have to know everything about callbacks in order to implement an API client. However, all developers should read the [Security considerations](#security-considerations) section.


## Security considerations