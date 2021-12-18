# Testing Checklist

Before you can go live with your integration you need to ensure it is fully tested and production worthy.

After all, we are dealing with money and sensitive data. What you should test varies depending on your integration and use cases. Below we’ve made a general checklist that should apply to all integrations, as well as integration-specific checklists.


## General Go-Live Checklist

Regardless of integration type and use case, we recommend that you check at least the following before you switch from Sandbox to Production:

1. Click test your end-to-end user journey.
2. Test with all device categories (mobile phone, tablet, desktop).
3. Where there are options, test all the alternatives:
    1. QR code or button.
    2. Phone number entry.
4. If you do AUTH, ensure you have logic in place to CAPTURE as well as being able to optionally REAUTH and RELEASE.
5. Make sure you support REFUND (both full and partial).
6. Ensure you have graceful error handling.
7. Ensure you can deal with multiple simultaneous customers:
    1. Do you use static or dynamic [Shortlink](/merchant-api/b3A6MTUzOTU0Mjk-merchant-shortlink-create) / QR Code?
    2. Do you use Argstring appended to [Shortlink](/merchant-api/b3A6MTUzOTU0Mjk-merchant-shortlink-create) / QR Code?

####

## Client-Side code

In addition to the General go-live checklist, for client-side code we recommend that you check at least the following before you switch from Sandbox to Production:

> #### More info coming soon.

####

## Server-Side code

In addition to the General go-live checklist, for server-side code we recommend that you check at least the following before you switch from Sandbox to Production:

> #### More info coming soon.