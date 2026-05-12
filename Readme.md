Here is a better `README.md` you can use:


# MEDIATE Data Models

This repository contains the NGSI-LD data models defined for the MEDIATE project.

The goal of these models is to provide a common and interoperable structure for the messages exchanged between MEDIATE components, including Sentinels, Overwatches, the DSS, the Policy Manager, the Service Manager, the Orchestrator, the Dashboard, and the Sentinel Reconfiguration/Deployment Unit.

The data models follow the NGSI-LD representation style used in FIWARE/Smart Data Models, where:
- entity identifiers are represented using `id`;
- entity types are represented using `type`;
- values are represented as NGSI-LD `Property`;
- references to other entities are represented as NGSI-LD `Relationship`;
- structured payloads are represented as structured `Property.value` objects when they are part of the message content.

For more information and access to the full private repository, refer to:

```text
https://github.com/H2020-MEDIATE/Mediate_Data_Model
```

---

## Repository Structure

Each data model is stored in a dedicated folder.

```text
Mediate_Data_Model/
├── Asset/
├── Overwatch/
├── Sentinel/
├── M1DetectedEventMessage/
├── M2vulnerabilityDataset/
├── M3predefinedConfigurationMetadataMessage/
├── M4dssMainOutputMessage/
├── M5policyEvaluatedCountermeasures/
├── M6userSelectedCountermeasureMessage/
├── M7policyCountermeasureDecision/
├── M8reconfigurationExecutionPlan/
├── M9predefinedSentinelConfiguration/
├── M10sentinelReconfigurationCommand/
├── M11sentinelReconfigurationStatus/
├── M12sentinelHeartbeat/
├── OM1getOverwatchesFullCommand/
├── OM2getSentinelCommand/
├── OM3getAssetCommand/
├── SM2overwatchSecurityStatusUpdatedEvent/
├── SM4sentinelReconfigurationStatusEvent/
├── SM6fleetHealthSummaryEvent/
├── SM7overwatchesFullResponseEvent/
├── SM8sentinelResponseEvent/
├── SM9assetResponseEvent/
└── context.jsonld
```

Each model folder contains:

```text
model.yaml
schema.json
```

| File             | Description                                                                                               |
| ---------------- | --------------------------------------------------------------------------------------------------------- |
| `schema.json`    | JSON Schema describing the structure of the NGSI-LD entity or message.                                    |
| `model.yaml`     | OpenAPI/Smart Data Models-style model used to describe NGSI-LD attributes and generate the context file.  |
| `context.jsonld` | Generated MEDIATE JSON-LD context containing the semantic mapping of MEDIATE entity types and attributes. |

---

## Context File

The repository contains a generated MEDIATE context file:

```text
context.jsonld
```

Whenever a MEDIATE NGSI-LD entity or message instance is created, it should reference the raw context file from this repository.

Example:

```json
{
  "id": "urn:ngsi-ld:mediate:messages:example:001",
  "type": "exampleEntity",
  "timestamp": {
    "type": "Property",
    "value": "2026-03-19T12:00:00Z"
  },
  "@context": [
    "https://raw.githubusercontent.com/H2020-MEDIATE/Mediate_Data_Model_Public/main/context.jsonld",
    "https://uri.etsi.org/ngsi-ld/v1/ngsi-ld-core-context.jsonld"
  ]
}
```

The MEDIATE context should be included together with the ETSI NGSI-LD core context.

If this repository is private, access to the raw context URL requires the appropriate GitHub permissions.

---

## Data Model Categories

The repository includes three main categories of data models.

### Core Registry Entities

These entities represent the registry-managed objects used by the Service Manager.

```text
Asset
Overwatch
Sentinel
```

### MEDIATE Message Models

These models represent the main MEDIATE communication messages.

```text
M1DetectedEventMessage
M2vulnerabilityDataset
M3predefinedConfigurationMetadataMessage
M4dssMainOutputMessage
M5policyEvaluatedCountermeasures
M6userSelectedCountermeasureMessage
M7policyCountermeasureDecision
M8reconfigurationExecutionPlan
M9predefinedSentinelConfiguration
M10sentinelReconfigurationCommand
M11sentinelReconfigurationStatus
M12sentinelHeartbeat
```

### Service Manager Registry Retrieval Messages

These models support request/response interactions between the Orchestrator and the Service Manager.

```text
OM1getOverwatchesFullCommand
OM2getSentinelCommand
OM3getAssetCommand
SM7overwatchesFullResponseEvent
SM8sentinelResponseEvent
SM9assetResponseEvent
```

### Service Manager Event Messages

These models represent event-driven updates published by the Service Manager.

```text
SM2overwatchSecurityStatusUpdatedEvent
SM4sentinelReconfigurationStatusEvent
SM6fleetHealthSummaryEvent
```

---

## Modelling Principles

The MEDIATE data models follow these modelling principles:

### Entity identifiers

Each entity or message has a unique NGSI-LD identifier:

```json
"id": "urn:ngsi-ld:mediate:asset:asset-01"
```

### Entity types

Each model defines a specific NGSI-LD `type`.

Example:

```json
"type": "asset"
```

or:

```json
"type": "fleetHealthSummaryEvent"
```

### Properties

Simple values are represented as NGSI-LD Properties.

```json
"riskLevel": {
  "type": "Property",
  "value": "HIGH"
}
```

### Relationships

References to other MEDIATE entities are represented as NGSI-LD Relationships.

```json
"associatedSentinel": {
  "type": "Relationship",
  "object": "urn:ngsi-ld:mediate:sentinel:sentinel-01"
}
```

### Arrays of relationships

When an attribute references several entities, the Relationship `object` may contain an array of entity identifiers.

```json
"managedAssets": {
  "type": "Relationship",
  "object": [
    "urn:ngsi-ld:mediate:asset:asset-01",
    "urn:ngsi-ld:mediate:asset:asset-02"
  ]
}
```

### Structured properties

When a message contains structured information that is part of the payload and does not need to be represented as a standalone entity, it is modeled as a structured Property.

```json
"status": {
  "type": "Property",
  "value": {
    "state": "completed",
    "result": "success",
    "details": "Configuration applied successfully"
  }
}
```

---

## Usage

To create a MEDIATE NGSI-LD instance:

1. Choose the appropriate data model folder.
2. Use the corresponding `schema.json` to validate the payload structure.
3. Include the generated MEDIATE `context.jsonld` in the `@context`.
4. Include the ETSI NGSI-LD core context.

Example:

```json
"@context": [
  "https://raw.githubusercontent.com/H2020-MEDIATE/Mediate_Data_Model/refs/heads/main/context.jsonld",
  "https://uri.etsi.org/ngsi-ld/v1/ngsi-ld-core-context.jsonld"
]
```

---

## Notes

* The repository is intended to support the definition and validation of MEDIATE NGSI-LD entities and messages.
* The generated `context.jsonld` provides the semantic mapping for MEDIATE-specific terms.
* The `schema.json` files are used for payload validation.
* The `model.yaml` files are used as the OpenAPI-style source for context generation.




