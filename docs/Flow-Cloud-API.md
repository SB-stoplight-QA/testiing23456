---
stoplight-id: tf79ts6r01zo9
---

# Cloud API for eBike Flow app
_Cloud API for eBike Flow app_ provides riders read-only access to their data, collected via the eBike Flow app.

## eBike Profile API
With _eBike Profile API_, riders gain insights on their eBike data like detailed specifications, configurations and changes.

This API requires a rider login via [SingleKey ID](https://singlekey-id.com/de/home/), `Authorization Code OAuth 2 Flow`.

## Activity Records API
The _Activity Records API_ allows riders to query past activities which have been recorded using the eBike Flow app. It provides access to activity details as well as a comprehensive activity summary after a ride is successfully finished.

This API requires a rider login via [SingleKey ID](https://singlekey-id.com/de/home/), `Authorization Code OAuth 2 Flow`.

## Getting started

### Prerequisites
There are two prerequsites in order to use _Cloud API for eBike Flow app_:
1. Partners need to get in touch with their responsible Bosch contact first to request an OAuth client, which represents your requesting client application.
2. Riders need to install the eBike Flow app on their smartphone and follow the registration and pairing process using a [SingleKey ID](https://singlekey-id.com/de/home/). Need help? Please follow this [documentation](https://www.bosch-ebike.com/en/products/ebike-flow-app).

### How does it work?
#### eBike Profile API & Activity Records API
- The eBike Flow app collects data from a smart system eBike and sends it to the Bosch cloud. _eBike Profile API_ and _Activity Records API_ enables riders to access their data, for example via a partner app or website. The following picture shows the data flow:

  ```mermaid
  flowchart LR      
    eb["Smart System eBike #128690;"] --> app["eBike Flow app #128241;"];
    app --> api["eBike Profile API<br>Activity Records API<br>#9729;"];
    api --> partner[Partner custom solution];
  ```

- In order to make successful API requests riders need a valid OpenID Connect Access Token (JWT), which must be obtained through SingleKey ID using the `Authorization Code OAuth 2 Flow`. Refer to the individual API documentation for security scheme details.
- Riders are asked once for consent to grant a partner client application access to their eBike data.
