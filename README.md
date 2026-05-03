# UPS

UPS (United Parcel Service) is a Fortune 500 global logistics company specializing in package delivery and supply chain management. UPS provides a comprehensive REST API platform with OAuth 2.0 authentication covering shipping, tracking, rating, address validation, pickup scheduling, paperless international documents, and time-in-transit estimation.

**Developer Portal:** https://developer.ups.com/
**API Catalog:** https://developer.ups.com/catalog
**Getting Started:** https://developer.ups.com/get-started

## APIs

| API | Description |
|---|---|
| [UPS Shipping API](openapi/ups-shipping-openapi.yml) | Comprehensive shipping API covering OAuth, rating, shipment creation, tracking, address validation, pickup, and time-in-transit |

## OpenAPI Specifications

| Spec | Description |
|---|---|
| [ups-shipping-openapi.yml](openapi/ups-shipping-openapi.yml) | UPS REST API covering OAuth, rating, shipping, tracking, address validation, pickup, and paperless documents |

## Spectral Rules

| Ruleset | Description |
|---|---|
| [ups-rules.yml](rules/ups-rules.yml) | Spectral ruleset enforcing UPS API conventions including OAuth auth, PascalCase wrappers, and path patterns |

## Naftiko Capabilities

### Shared Definitions

| File | APIs Covered |
|---|---|
| [shared/ups-shipping.yaml](capabilities/shared/ups-shipping.yaml) | UPS Shipping API (rates, shipments, tracking, address validation, pickup, transit times) |

### Workflow Capabilities

| Workflow | Description | Tools |
|---|---|---|
| [shipping-and-logistics.yaml](capabilities/shipping-and-logistics.yaml) | End-to-end shipping and logistics — rate shopping, shipment creation, tracking, address validation, pickup, and transit times | 9 tools |

## JSON Schemas

| Schema | Description |
|---|---|
| [ups-shipment-schema.json](json-schema/ups-shipment-schema.json) | UPS shipment including tracking number, service, addresses, package, label, and charges |

## JSON Structure

| Structure | Description |
|---|---|
| [ups-shipment-structure.json](json-structure/ups-shipment-structure.json) | Field-level documentation for the UPS Shipment resource |

## JSON-LD

| Context | Description |
|---|---|
| [ups-context.jsonld](json-ld/ups-context.jsonld) | Linked data context mapping UPS resources to schema.org (ParcelDelivery, PostalAddress, PriceSpecification) |

## Examples

| Example | Description |
|---|---|
| [ups-track-shipment-example.json](examples/ups-track-shipment-example.json) | GET /track/v1/details/{trackingNumber} response |
| [ups-shop-rates-example.json](examples/ups-shop-rates-example.json) | POST /rating/v1/Shop request and response |

## Vocabulary

| File | Description |
|---|---|
| [ups-vocabulary.yml](vocabulary/ups-vocabulary.yml) | Domain vocabulary for UPS shipping and logistics including tracking numbers, service codes, address classification, and OAuth concepts |

## Links

- **Website:** https://www.ups.com
- **Developer Portal:** https://developer.ups.com
- **API Catalog:** https://developer.ups.com/catalog
- **Getting Started:** https://developer.ups.com/get-started

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
