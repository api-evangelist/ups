# UPS GraphQL Schema

## Overview

This GraphQL schema represents the UPS Developer Kit REST API surface — covering shipping, tracking, rating, address validation, pickup scheduling, and related logistics operations. UPS exposes its capabilities through OAuth 2.0 authenticated REST endpoints at `https://onlinetools.ups.com/api`. This schema provides a conceptual GraphQL layer over those capabilities.

**Provider:** UPS (United Parcel Service)
**Developer Portal:** https://developer.ups.com/
**API Catalog:** https://developer.ups.com/catalog
**GitHub:** https://github.com/UPS-API
**Base URL:** https://onlinetools.ups.com/api
**Authentication:** OAuth 2.0 (client credentials or authorization code)

## Schema Source

The schema was derived from the UPS Developer Kit documentation, the UPS Shipping OpenAPI specification, and the UPS GitHub organization. It covers the following functional areas:

- **Shipment** — Create, manage, and cancel shipments; generate labels
- **Tracking** — Real-time package tracking, activity history, status codes
- **Rating** — Rate shopping, negotiated rates, surcharges
- **Pickup** — Schedule pickups and locate drop locations
- **Returns** — Return services and return address management
- **Freight / LTL** — Less-than-truckload freight shipments and pickups
- **MyChoice** — Consumer delivery preference management
- **QuantumView** — Subscription-based visibility data feeds
- **Labels** — Label generation in HTML, GIF, EPL, ZPL formats
- **Authentication** — API keys and OAuth tokens

## Core Types (70+)

| Type | Category | Description |
|------|----------|-------------|
| `Shipment` | Shipping | Top-level shipment record |
| `ShipmentDetails` | Shipping | Detailed shipment attributes |
| `ShipmentRequest` | Shipping | Input for creating a shipment |
| `ShipmentResponse` | Shipping | Response after shipment creation |
| `TrackingNumber` | Tracking | A UPS tracking number |
| `TrackingActivity` | Tracking | Individual tracking scan event |
| `TrackingStatus` | Tracking | Current status of a tracked package |
| `TrackingResponse` | Tracking | Full tracking API response |
| `Package` | Packaging | A single package within a shipment |
| `PackageDetails` | Packaging | Extended package attributes |
| `PackageResult` | Packaging | Per-package result from shipment API |
| `PackageWeight` | Packaging | Weight value and unit |
| `PackageDimensions` | Packaging | Length, width, height and unit |
| `PackageReferenceNumber` | Packaging | Customer reference attached to a package |
| `ReferenceNumber` | General | Generic reference number |
| `ServiceCode` | Service | UPS service code (e.g., `01` = Next Day Air) |
| `ServiceDescription` | Service | Human-readable service description |
| `PackagingType` | Packaging | Packaging type code and description |
| `IndicatorType` | General | Boolean indicator with a type code |
| `Label` | Labels | Generated shipping label |
| `LabelSpec` | Labels | Label format and method specification |
| `LabelFormat` | Labels | Format code (GIF, EPL, ZPL, etc.) |
| `LabelMethod` | Labels | Label delivery method |
| `HTMLImage` | Labels | HTML-encoded label image |
| `GIFImage` | Labels | GIF binary label image |
| `EPLImage` | Labels | EPL (Eltron) label image |
| `ZPLImage` | Labels | ZPL (Zebra) label image |
| `ShipFrom` | Address | Origin address for a shipment |
| `ShipTo` | Address | Destination address for a shipment |
| `ReturnService` | Returns | Return service type |
| `ReturnAddress` | Returns | Address for return shipments |
| `AlternateDelivery` | Delivery | Alternate delivery location |
| `MyChoice` | Delivery | UPS MyChoice consumer delivery preferences |
| `Signature` | Delivery | Signature capture record |
| `SignatureType` | Delivery | Type of signature required |
| `DeliveryConfirmation` | Delivery | Delivery confirmation options |
| `Insurance` | Value Services | Insurance option on a package |
| `InsuredValue` | Value Services | Declared value amount and currency |
| `COD` | Value Services | Cash on delivery option |
| `CODValue` | Value Services | COD amount and currency |
| `CODPaymentType` | Value Services | COD payment method type |
| `RateRequest` | Rating | Input for a rate quote request |
| `RateResponse` | Rating | Rate quote response |
| `RateDetail` | Rating | Individual rate line item |
| `NegotiatedRate` | Rating | Account-negotiated rate |
| `Surcharge` | Rating | Additional charge applied to a shipment |
| `SurchargeCode` | Rating | Surcharge type code |
| `QuantumView` | Visibility | QuantumView data feed record |
| `QVSubscription` | Visibility | QuantumView subscription configuration |
| `QVShipment` | Visibility | Shipment record within a QV feed |
| `LabelRecovery` | Labels | Retrieve a previously generated label |
| `PickupCreation` | Pickup | Schedule a pickup request |
| `DropLocation` | Pickup | UPS drop-off location |
| `ServiceCenter` | Pickup | UPS service/customer center |
| `FreightShipment` | Freight | LTL freight shipment |
| `FreightPickup` | Freight | LTL freight pickup request |
| `LTLService` | Freight | Less-than-truckload service option |
| `APIKey` | Auth | UPS Developer API key |
| `Token` | Auth | OAuth 2.0 access token |
| `Webhook` | Events | Webhook endpoint registration |
| `Address` | Address | Generic postal address |
| `Contact` | Address | Person or company contact |
| `Phone` | Address | Phone number |
| `Money` | General | Currency amount |
| `Weight` | General | Weight with unit |
| `Dimensions` | General | Physical dimensions with unit |
| `TimeInTransit` | Rating | Estimated transit time |
| `ServiceAvailability` | Service | Service availability for a route |
| `AddressValidation` | Address | Address validation result |
| `AddressCandidate` | Address | Suggested corrected address |
| `VoidShipment` | Shipping | Void/cancel shipment request and response |
| `ManifestRequest` | Shipping | End-of-day manifest request |
| `ManifestResponse` | Shipping | End-of-day manifest response |
| `LocatorRequest` | Pickup | Request to find nearby UPS locations |
| `LocatorResponse` | Pickup | Response with nearby UPS locations |
| `AccessPointLocation` | Pickup | UPS Access Point location details |
| `Commodity` | Freight | Freight commodity description |
| `HandlingUnit` | Freight | Freight handling unit |

## Queries

- `trackPackage(trackingNumber: String!): TrackingResponse`
- `getRate(request: RateRequest!): RateResponse`
- `validateAddress(address: Address!): AddressValidation`
- `findLocations(request: LocatorRequest!): LocatorResponse`
- `getTimeInTransit(shipFrom: Address!, shipTo: Address!, weight: Weight!): TimeInTransit`
- `getLabelRecovery(trackingNumber: String!): LabelRecovery`
- `getServiceAvailability(origin: Address!, destination: Address!): [ServiceAvailability]`
- `getQuantumView(subscription: String!, dateRange: String): [QVShipment]`
- `getDropLocations(address: Address!, radius: Int): [DropLocation]`
- `getPickupWindow(address: Address!, serviceDate: String!): PickupCreation`

## Mutations

- `createShipment(request: ShipmentRequest!): ShipmentResponse`
- `voidShipment(shipmentId: String!): VoidShipment`
- `createPickup(request: PickupCreation!): PickupCreation`
- `cancelPickup(confirmationNumber: String!): Boolean`
- `createFreightShipment(request: FreightShipment!): FreightShipment`
- `createFreightPickup(request: FreightPickup!): FreightPickup`
- `subscribeQuantumView(subscription: QVSubscription!): QVSubscription`
- `registerWebhook(webhook: Webhook!): Webhook`
- `deleteWebhook(webhookId: String!): Boolean`
- `submitManifest(request: ManifestRequest!): ManifestResponse`

## Authentication

UPS APIs use OAuth 2.0. Obtain a client ID and secret from the UPS Developer Portal, then exchange them for a bearer token:

```
POST https://onlinetools.ups.com/security/v1/oauth/token
Content-Type: application/x-www-form-urlencoded
Authorization: Basic <base64(client_id:client_secret)>

grant_type=client_credentials
```

Use the returned `access_token` as `Authorization: Bearer <token>` on all API calls.

## References

- UPS Developer Portal: https://developer.ups.com/
- API Catalog: https://developer.ups.com/catalog
- Getting Started: https://developer.ups.com/get-started
- GitHub: https://github.com/UPS-API
- OpenAPI Spec: https://raw.githubusercontent.com/api-evangelist/ups/refs/heads/main/openapi/ups-shipping-openapi.yml
