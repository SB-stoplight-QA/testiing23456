---
stoplight-id: fmq4ydwc9xg0h
---

# Cloud API for ConnectModule
The _Cloud API for ConnectModule_ empowers **partners** to manage Bosch ConnectModule (BCM) configurations and notifications through the _ConnectModule Configuration API_ and the _Notification API_.

<!-- theme: info -->

> #### Please note
>
> No rider login required for Cloud API for ConnectModule.

## Getting started

### Prerequisites
In order to use _ConnectModule Configuration API_ and the _Notification API_, please get in touch with your responsible Bosch contact first to request an OAuth client, which represents your requesting client application.

### How does it work?

#### Client authentication
In order to make successful API requests you need a valid OpenID Connect Access Token (JWT), which must be obtained through our OAuth server using the `Client Credentials OAuth 2 Flow`. Refer to the individual API documentation for security scheme details.

#### Configuration steps
1. Activate the BCM for remote configuration, which requires the software version >= `BES3_12` to be flashed beforehand.
2. With the next power-on of the eBike, the BCM automatically connects to the Bosch cloud to receive configurations.
3. [Register](openapi/eBikeRegistration.v1.yaml/paths/~1registrations/post) the BCM using the _[eBike Registration API](openapi/eBikeRegistration.v1.yaml)_ to obtain configuration authorization.
4. [Configure](openapi/bcmConfiguration.v2.yaml/paths/~1connect-modules~1{moduleId}~1features~1{featureType}/put) features using the _[ConnectModule Configuration API](openapi/bcmConfiguration.v2.yaml)_.
5. (Optionally) [Subscribe](openapi/notification.v1.yaml/paths/~1webhooks/post) to event types to receive notifications via webhooks using the _[Notification API](openapi/notification.v1.yaml)_.

#### Runtime behaviour
- Enable BCM features and (optionally) subscribe to notifications through the _ConnectModule Configuration API_ and the _Notification API_:
  ```mermaid
      flowchart LR      
      BCM["Smart System eBike <br> with Bosch ConnectModule #128690;"];          
      api1["ConnectModule Configuration API #9729;"] --> BCM;
      partner[Partner backend] --> api1;
      partner --> api2["Notification API #9729;"];
  ```

- As soon as a BCM feature is enabled it sends data to the Bosch cloud. _Notification API_ pushes it to subscribed partner webhook listeners. The following picture shows the simplified data flow:
  ```mermaid
      flowchart LR      
      BCM["Smart System eBike <br> with Bosch ConnectModule #128690;"];          
      BCM --> api["Notification API #9729;"];
      api --> partner[Partner webhook listener];
  ```

## BCM registrations
Initially the BCM is in an unregistered state and partners must [register](openapi/eBikeRegistration.v1.yaml/paths/~1registrations/post) it providing BCM identifiers to obtain configuration authorization.

Registered bikes and components have to be [de-registered](openapi/eBikeRegistration.v1.yaml/paths/~1registrations~1deregister/post) if they are transferred to other use (e.g. resale). Registration
status may be reset if the hardware or software configuration of the eBike system or ConnectModule is changed.

## BCM configurations
Enabling and disabling BCM features is provided by _[ConnectModule Configuration API](openapi/bcmConfiguration.v2.yaml)_.

The following features are available:


Feature | eBike system software requirements
---------|----------
 `BIKE_STATUS` | `BES3_12`
 `LOCATION_TRACKING` | `BES3_12`
 `DISABLE_MOTOR_SUPPORT` | `BES3_17`

For each feature you have to select a predefinied profile (e.g. `DEFAULT`) which has an impact on the collection and transmission rate of the data.

## BCM notifications
_[Notification API](openapi/notification.v1.yaml)_ uses webhooks for BCM event notifications. Webhooks are push API calls, using the HTTP `POST` method, that notifies your service when an event has happened for your managed BCMs.

#### How to use it?
First provide an internet facing webhook listener, then [create a webhook](openapi/notification.v1.yaml/paths/~1webhooks/post) to subscribe to one or more events.\
In order for your application to be able to receive event notifications, it must:
* Provide one or more internet facing HTTP `POST` endpoint(s) to receive notifications of various [event types](#event-types) in JSON format.
* Verify that the event notification came from Bosch and was not altered or corrupted during transmission. See [Message signature](#message-signature).
* Respond with a HTTP `200` status code.

#### How to create a Webhook?
You can subscribe to one or more types of events, but each event type can be only subscribed once. The subscription is only created when a [test notification](openapi/notification.v1.yaml/components/schemas/WebhookTest) has been sent successfully to the specified URL. Static authentication credentials can be added optionally.

In case of connection failures, _Notification API_ performs 5 retries (after 1, 2, 5, 180 and 480 seconds) for the current event. The event is skipped if the total of retries is reached without success.

#### Message signature
We sign the request payload of each event notification and send it over HTTPS (TLS). The request headers contain the signature and additional information that you have to use to validate the signature.

##### HTTP header
| Header Name | Description |
|:------|:------------|
| X-Bosch-Sig | The Bosch generated asymmetric signature. |
| X-Bosch-Sig-Algo | The algorithm that Bosch used to generate the signature and that you can use to verify the signature. (e.g. SHA-256 with RSA encryption) |
| X-Bosch-Cert-Url | The X509 public key certificate. Download the certificate from this URL and use it to verify the signature. |

##### Signature validation
The following example shows, how to verify the signature using OpenSSL:
- tls-pub.pem - the downloaded public X509 certificate
- sig - the signature from the HTTP request header X-Bosch-Sig
- msg - the notification message from the HTTP request body
```
openssl dgst -sha256 -verify tls-pub.pem -signature sig msg
Verified OK
```

#### Event types
Partners can subscribe to the following event types:
| Event Name | Event Schema | Prerequsites |
|:------|:------------|:------------|
| BIKE_STATUS | [BikeStatus](openapi/notification.v1.yaml/components/schemas/BikeStatus) | `BIKE_STATUS` feature is enabled on the BCM |
| BIKE_PROFILE | [BikeProfile](openapi/notification.v1.yaml/components/schemas/BikeProfile) | Part of the `BIKE_STATUS` feature, which must be enabled on the BCM|
| LOCATION_TRACKING | [LocationTracking](openapi/notification.v1.yaml/components/schemas/LocationTracking) | `LOCATION_TRACKING` feature is enabled on the BCM |
