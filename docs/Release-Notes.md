---
stoplight-id: iwiy2dmnjhlcl
---

# Release Notes

## February 2026
### February 9

- Moved eBike Model Ingestion API and eBike Model API draft to cluster _Cloud API for eBike product data_.

## January 2026
### January 27

- Updated notice of deprecation and sunset of the ConnectModule Configuration API v1. API will be **sunset on 31.03.2026 23:59:59**.

### January 13

- Added registration and deregistration examples to the eBike Registration API v1.

## December 2025
### December 17

- General availability of ConnectModule Configuration API v2. Without ConnectModule ownerships (use eBike Registration API instead) and `OEM_BIKE_ID` query parameter of the ConnectModule discovery endpoint.
- Added ConnectModule Configuration API v2 draft for upcoming features.

### December 10

- General availability of eBike Registration API v1.

## November 2025
### November 19

- Added eBike Registration API v1 draft to cluster _Cloud API for eBike Registration_.

## October 2025
### October 24

- Added drafts of eBike Model API and Commerce API to cluster _Cloud API for eBike Flow App_.

### October 17
- Released Notification API v1.2.0 with support for BikeTraceabilityStatus notifications.
- Sunset of Supply Chain Data API v1.

### October 6
- Released Notification API v1.1.0 with support for BikeProfile notifications.
- Released ConnectModule Configuration API v1.1.0. New feature `DISABLE_MOTOR_SUPPORT`.

## July 2025
### July 31
- Released eBike Profile API v1.3.0 with additional driveUnit datapoints like walkAssistConfiguration, rearWheelCircumferenceUser, maximumAssistanceSpeed, activeAssistModes and powerOnTime.
### July 25

- General availability of Supply Chain Data API v2.
- Added notice of deprecation and sunset of the Supply Chain Data API v1. API will be **sunset on 15.10.2025 23:59:59**.

### July 16

- Added ConnectModule Configuration API v2 draft for upcoming features.

## June 2025
### June 25

- Added notice of deprecation and sunset of the ConnectModule Configuration API v1. API will be **sunset on 31.12.2025 23:59:59**.

## March 2025
### March 13

- Updated Supply Chain Data API (v1.2.0). Included touchpoints for first activity of Flow app and added modelId to OEM properties of bike traceabilities. Added productionLine property, marked productionLineId as deprecated and updated the description.

## December 2024
### December 10

- General availability of Cloud API for ConnectModule (ConnectModule Configuration API v1.0.0 and ConnectModule Notification API v1.0.0).

## October 2024
### October 29

- Supply Chain Data API v1.0.0. Pilot phase started.

## October 2024
### October 7

- Renamed API catagories to _Cloud API for eBike Flow App_, _Cloud API for ConnectModule_ and _Cloud API for eBike product data_.
- Added new draft API (Supply Chain Data API) for category _Cloud API for product data_.

## June 2024
### June 21

- ConnectModule Configuration API draft. Added endpoints to manage Bosch ConnectModule ownership and to discover ConnectModule master data.

## May 2024
### May 17

- Service Book API draft has been removed. Still interested? Please get in touch with us.

## December 2023
### December 8

<!-- theme: success -->

> **📢 Major update of Cloud API reference documentation**


- Cloud API is now split into multiple API specifications for more clarity.
- All APIs are categorized and assigned to either Flow/Cloud API, BCM/Cloud API or Data/Cloud API. Just pick and integrate those APIs you need for your use case.
- Additional documentation content available for each category and improved left navigation.
- Introduced API maturity types to help you understand drafts and production APIs.
- Each API provides a hosted mock server to speed up your development. All requests will be validated and responses are generated either statically or dynamically, your choice. Documentation will follow.
- Updated documentation and data examples of ConnectModule and Notification API drafts (BCM/Cloud API).
- Updated Notification API draft - BikeStatus schema (BCM/Cloud API), we extended the schema based on customer request.
- Check out our recently launched Bike Model Ingestion API v1.0.0 (Data/Cloud API), which enables you to upload bike model information to be served by the eBike Flow app.