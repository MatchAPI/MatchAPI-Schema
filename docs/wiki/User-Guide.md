# MatchAPI User Guide

## Purpose

MatchAPI is a JSON Schema-based format for describing financial messaging APIs in a structured, machine-readable way.

A MatchAPI dictionary can describe message models, data types, fields, components, groups, references, variants, classifiers, documentation, additional data, and change history.

The format is intended to be protocol-neutral. It can be used for FIX-style protocols, proprietary binary protocols, JSON-based APIs, and other financial messaging interfaces.

## Basic document structure

A MatchAPI dictionary has the following root structure:

```json
{
  "$schema": "https://matchapi.org/schema/matchapi-core-1.0.0.json",
  "name": "Example API",
  "version": "1.0.0",
  "content": {
    "dataTypes": [],
    "fields": [],
    "components": [],
    "groups": [],
    "messages": []
  }
}
```

Only `name`, `version`, and `content` are required by the core schema.

## Metadata

The optional `metadata` object can describe the API publication.

Supported metadata properties are:

- `title`;
- `description`;
- `creator`;
- `publisher`;
- `contributor`;
- `rights`;
- `format`;
- `source`;
- `conformsTo`.

Example:

```json
{
  "metadata": {
    "title": "Example Trading API",
    "publisher": "Example Exchange",
    "description": "Machine-readable dictionary for the Example Trading API"
  }
}
```

## Data types

Data types describe the value model used by fields and composite members.

Supported data type kinds are:

```text
primitive, derived, enum, array, composite, bitset
```

### Primitive data type

```json
{
  "name": "String",
  "type": "primitive"
}
```

### Derived data type

```json
{
  "name": "Price",
  "type": "derived",
  "baseTypeRef": {
    "name": "Decimal"
  }
}
```

### Enum data type

```json
{
  "name": "SideCode",
  "type": "enum",
  "valuesTypeRef": {
    "name": "String"
  },
  "values": [
    {
      "name": "Buy",
      "value": "1"
    },
    {
      "name": "Sell",
      "value": "2"
    }
  ]
}
```

## Fields

A field represents a named value in an API.

A field definition requires `name` and `typeRef`.

Example:

```json
{
  "name": "ClOrdID",
  "typeRef": {
    "name": "String"
  }
}
```

Fields can also express constraints, such as value ranges, length constraints, regex patterns, fixed byte lengths, character sets, padding, and references to length or qualifier fields.

## Messages

A message describes a protocol message.

Example:

```json
{
  "name": "NewOrderSingle",
  "msgType": "D",
  "msgCategory": "application",
  "direction": "in",
  "content": [
    {
      "refType": "field",
      "refKey": {
        "name": "ClOrdID"
      },
      "presence": "required"
    }
  ]
}
```

Message direction is expressed from the API's point of view:

| Direction | Meaning |
|---|---|
| `in` | Message sent from the client to the API |
| `out` | Message sent from the API to the client |
| `both` | Message used in both directions |

## Components

A component is a reusable complex structure.

Example:

```json
{
  "name": "Instrument",
  "content": [
    {
      "refType": "field",
      "refKey": {
        "name": "Symbol"
      },
      "presence": "required"
    }
  ]
}
```

A message, component, or group may reference a component using:

```json
{
  "refType": "component",
  "refKey": {
    "name": "Instrument"
  }
}
```

## Groups

A group describes a repeating structure.

Example:

```json
{
  "name": "NoPartyIDs",
  "headerRef": {
    "name": "NoPartyIDs"
  },
  "minInstances": 0,
  "content": [
    {
      "refType": "field",
      "refKey": {
        "name": "PartyID"
      },
      "presence": "required"
    }
  ]
}
```

A group reference may specify `minInstances` and `maxInstances`.

## Content composition and ordering

Complex elements may specify:

| Property | Values | Meaning |
|---|---|---|
| `contentComposition` | `allOf`, `oneOf` | Whether all child definitions apply or exactly one applies |
| `contentOrdering` | `ordered`, `unordered` | Whether child elements must appear in the defined order |

Defaults:

| Property | Default |
|---|---|
| `contentComposition` | `allOf` |
| `contentOrdering` | `ordered` |

## References and keys

References use `refKey` or type-specific reference properties such as `typeRef`, `baseTypeRef`, `valuesTypeRef`, and `elementsTypeRef`.

A reference may use `uuid`, `id`, `name`, and `variant`.

The `keys` section defines how elements are uniquely identified and referenced.

If a primary key is omitted, the default for most element types is:

```text
name + variant
```

Enumerated values default to:

```text
primary key: name
alternate key: value
```

For details and examples, see [[References and Keys|References-and-Keys]].

## Variants

Elements may have a `variant` property. If omitted, the default variant is `base`.

Use variants when the same logical element has different forms in different use cases.

## Classifiers

The optional `classifiers` object can define:

- `variants`;
- `categories`;
- `sections`.

These help organise dictionaries for documentation, navigation, and tooling.

## Documentation entries

Elements may include documentation entries.

Example:

```json
{
  "documentation": [
    {
      "role": "summary",
      "text": "Client order identifier.",
      "contentType": "text/plain",
      "language": "en"
    }
  ]
}
```

## Additional data

Elements may include implementation-specific data through `additionalData`.

Example:

```json
{
  "additionalData": [
    {
      "role": "internalMapping",
      "data": "Order.ClientOrderId"
    }
  ]
}
```

The `data` value is a string. If structured data is needed, it should be encoded as a string by the producing application.

## Change log

Elements may include a `changeLog`.

Example:

```json
{
  "changeLog": [
    {
      "changeType": "updated",
      "version": "1.1.0",
      "changeScope": "definitional",
      "timestamp": "2026-01-15T10:00:00Z",
      "description": "Updated field length constraint."
    }
  ]
}
```

## Practical consumption model

A consumer should usually:

1. Validate the dictionary against the JSON Schema.
2. Load `content.dataTypes`.
3. Load `content.fields` and resolve `typeRef`.
4. Load `content.components` and resolve child references.
5. Load `content.groups` and resolve child references.
6. Load `content.messages` and resolve child references.
7. Apply classifier, documentation, additional data, and change log information as needed.

## Implementation note

MatchAPI is a data format. It does not mandate a specific programming language, runtime, validator, or documentation generator.

## Related pages

- [[Getting Started|Getting-Started]]
- [[Core Concepts|Core-Concepts]]
- [[Consumer Guide|Consumer-Guide]]
- [[Publisher Guide|Publisher-Guide]]
- [[Validation]]
