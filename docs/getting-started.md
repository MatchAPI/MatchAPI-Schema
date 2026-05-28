# Getting Started with MatchAPI

This guide is for developers who have received a MatchAPI JSON file and need to understand what to do with it.

## 1. Identify the file

A MatchAPI file is a JSON document that conforms to the MatchAPI Core JSON Schema.

The schema identifier for MatchAPI Core 1.0.0 is:

```text
https://matchapi.org/schema/matchapi-core-1.0.0.json
```

A MatchAPI file should contain at least:

```json
{
  "name": "Example API",
  "version": "1.0.0",
  "content": {}
}
```

The required top-level properties are:

| Property | Meaning |
|---|---|
| `name` | Name of the API being described |
| `version` | Version of the API dictionary |
| `content` | The actual API model |

## 2. Validate the file

Validate the file against:

```text
schema/matchapi-core-1.0.0.json
```

Use a JSON Schema validator that supports Draft 2020-12.

Validation answers a structural question:

> Is this JSON document shaped like a valid MatchAPI dictionary?

It does not prove that the described API is semantically correct, implemented correctly, or commercially supported by the API publisher.

See [Validation](validation.md).

## 3. Inspect the top-level structure

A MatchAPI dictionary may contain the following top-level sections:

| Section | Purpose |
|---|---|
| `$schema` | Optional schema URI |
| `$comment` | Optional comment about the API |
| `name` | API name |
| `id` | API identifier |
| `url` | External URL for the API or related documentation |
| `version` | API dictionary version |
| `protocolVersion` | Protocol-specific version, such as a FIX version |
| `endianness` | Big-endian or little-endian byte order for binary APIs |
| `keys` | Unique key definitions for referencing elements |
| `metadata` | Publisher and descriptive metadata |
| `content` | Messages, fields, groups, components, and data types |
| `classifiers` | Variants, categories, and sections |

## 4. Start with `content`

The `content` object is the main part of a MatchAPI dictionary. It may contain:

| Collection | Description |
|---|---|
| `messages` | Message definitions |
| `components` | Reusable complex elements |
| `groups` | Repeating group definitions |
| `fields` | Field definitions |
| `dataTypes` | Primitive, derived, enum, array, composite, and bitset data types |

For most users, the practical reading order is:

1. `dataTypes`
2. `fields`
3. `components`
4. `groups`
5. `messages`

## 5. Resolve references

MatchAPI definitions refer to other definitions using reference objects.

For example, a field definition uses `typeRef` to reference a data type:

```json
{
  "name": "ClOrdID",
  "typeRef": {
    "name": "String"
  }
}
```

A message contains child element references inside `content`:

```json
{
  "name": "NewOrderSingle",
  "msgType": "D",
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

The way references are resolved depends on the relevant primary key. If no custom key is defined, most element types default to `name` and `variant` as the primary key.

## 6. Read message definitions

A message definition may include:

| Property | Meaning |
|---|---|
| `name` | Message name |
| `msgType` | Protocol-specific message type |
| `msgCategory` | Message category, such as session or application |
| `direction` | `in`, `out`, or `both`, from the API's point of view |
| `content` | Child field, component, and group references |
| `contentComposition` | `allOf` or `oneOf` |
| `contentOrdering` | `ordered` or `unordered` |

The direction is from the API's point of view. For example, `in` means the message is sent from the client to the API.

## 7. Use the dictionary in your tooling

A MatchAPI dictionary can be used to drive:

- documentation generation;
- conformance checks;
- internal API catalogues;
- message validation logic;
- integration tooling;
- protocol mapping;
- change impact analysis.

MatchAPI does not require a specific implementation language. The schema is JSON-compatible and can be consumed from any environment that can parse JSON.
