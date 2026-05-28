# MatchAPI Core Concepts

This page describes the main concepts in MatchAPI Core 1.0.0.

## Dictionary

A MatchAPI dictionary is a JSON document describing one financial messaging API.

The schema requires three top-level properties:

| Property | Meaning |
|---|---|
| `name` | Name of the API |
| `version` | Version of the API dictionary |
| `content` | Main API content |

The root object does not allow arbitrary additional properties.

## Content

The `content` object contains the main API model.

It may contain:

| Collection | Contains |
|---|---|
| `messages` | Message definitions |
| `components` | Component definitions |
| `groups` | Repeating group definitions |
| `fields` | Field definitions |
| `dataTypes` | Data type definitions |

## Element identity

Most named elements share common identity and annotation properties.

Common identity properties include:

| Property | Meaning |
|---|---|
| `uuid` | UUID of the element |
| `id` | Protocol-specific identifier, such as a FIX tag |
| `name` | Element name |
| `shortName` | Abbreviated name |
| `displayName` | Human-readable display name |

The `name` property is required for element definitions.

## References

MatchAPI uses reference objects to connect definitions.

A reference may use:

| Property | Meaning |
|---|---|
| `uuid` | UUID of the referenced element |
| `id` | Protocol-specific identifier |
| `name` | Name of the referenced element |
| `variant` | Variant of the referenced element, defaulting to `base` |

The relevant key is defined by the `keys` section. If omitted, most element types default to `name` and `variant` as the primary key.

## Keys

The optional `keys` section defines uniqueness and reference rules for:

- `messages`;
- `components`;
- `groups`;
- `fields`;
- `dataTypes`;
- enumerated `values` inside data types.

A key is an array using one or more of:

```text
uuid, id, name, msgType, variant, value
```

Each key definition has a required `primaryKey` and may also have `alternateKeys`.

The primary key is used for references. Alternate keys are additional uniqueness constraints.

## Data types

MatchAPI Core defines the following data type kinds:

| Type | Description |
|---|---|
| `primitive` | Base primitive type |
| `derived` | Type derived from another type using `baseTypeRef` |
| `enum` | Enumerated type with explicit values |
| `array` | Collection of elements of one type |
| `composite` | Structured type with member elements |
| `bitset` | Bit-level structure, usually for flags or packed values |

### Primitive data type

A primitive data type has:

```json
{
  "name": "String",
  "type": "primitive"
}
```

### Derived data type

A derived type references a base type:

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

An enum data type requires `valuesTypeRef` and `values`:

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

### Array data type

An array type references the element type using `elementsTypeRef` and may indicate whether elements are unique or ordered.

### Composite data type

A composite type contains member definitions in `content`. Each member references a type through `typeRef`.

### Bitset data type

A bitset type defines a fixed number of bits and a list of bitset members. Bitset members may describe single-bit flags or multi-bit ranges.

## Fields

A field definition requires a `typeRef`.

A field may also define constraints or encoding details, including:

- `value`;
- `minValue`;
- `maxValue`;
- `lengthHeaderRef`;
- `valueQualifierRef`;
- `allowOtherValues`;
- `valuePattern`;
- `minLength`;
- `maxLength`;
- `byteLength`;
- `charSet`;
- `terminatingChar`;
- `paddingChar`;
- `paddingSide`.

Field definitions do not contain child elements. They are referenced from messages, components, and groups.

## Components

A component is a reusable complex element. It contains child element references in `content`.

A component may contain references to:

- fields;
- groups;
- other components.

## Groups

A group is a repeating structure.

A group definition may include:

| Property | Meaning |
|---|---|
| `headerRef` | Reference to the group header element |
| `minInstances` | Minimum number of group instances |
| `maxInstances` | Maximum number of group instances |
| `content` | Child element references |

A group reference may also specify `minInstances` and `maxInstances`.

## Messages

A message is a top-level business or session-level message definition.

A message may include:

| Property | Meaning |
|---|---|
| `msgType` | Protocol-specific message type |
| `msgCategory` | Message category |
| `direction` | `in`, `out`, or `both` |
| `content` | Child element references |
| `contentComposition` | `allOf` or `oneOf` |
| `contentOrdering` | `ordered` or `unordered` |

## Child element references

A child element reference appears inside the `content` of a message, component, or group.

It requires:

| Property | Meaning |
|---|---|
| `refType` | `field`, `component`, or `group` |
| `refKey` | Reference to the target element |

It may also define:

| Property | Meaning |
|---|---|
| `refName` | Name to use for this reference |
| `presence` | `optional`, `required`, `conditionallyRequired`, `ignored`, `forbidden`, or `constant` |
| `offset` | Byte offset for binary protocols |
| `paddedLength` | Fixed padded length |

## Presence

Child element references support the following presence values:

| Value | Meaning |
|---|---|
| `optional` | The element may be present |
| `required` | The element must be present |
| `conditionallyRequired` | The element is required under defined conditions |
| `ignored` | The element is ignored |
| `forbidden` | The element must not be present |
| `constant` | The element has a constant value |

Composite data type members have a narrower presence model:

```text
optional, required, constant
```

Bitset members use:

```text
required, ignored, constant
```

## Variants

A variant represents a different form of the same element used for a particular use case.

Elements have a `variant` property that defaults to `base`.

The `classifiers.variants` collection can be used to define variants used in the API dictionary.

## Categories and sections

The `classifiers` object may define:

| Collection | Meaning |
|---|---|
| `variants` | Defined variants |
| `categories` | Groups of elements |
| `sections` | Groups of categories |

Categories may include:

- `section`;
- `componentType`, with values `message` or `field`;
- `includeFile`, with values `components` or `fields`.

## Documentation

Many elements support a `documentation` array.

Each documentation entry may include:

| Property | Meaning |
|---|---|
| `role` | Role of the documentation entry |
| `text` | Documentation text |
| `contentType` | MIME type, defaulting to `text/plain` |
| `language` | Language tag |

## Additional data

Many elements support an `additionalData` array.

Each entry contains:

| Property | Meaning |
|---|---|
| `role` | Role of the additional data entry |
| `data` | Additional data as a string |

Use `additionalData` for implementation-specific mappings or data that should remain within the schema-defined extension mechanism.

## Change log

Many elements support a `changeLog` array.

A change log entry may include:

- `changeType`;
- `version`;
- `changeScope`;
- `replacedBy`;
- `timestamp`;
- `trackingReference`;
- `author`;
- `description`.

Supported `changeType` values are:

```text
added, updated, replaced, deprecated
```

Supported `changeScope` values are:

```text
definitional, editorial
```
