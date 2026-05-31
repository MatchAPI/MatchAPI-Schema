# References and Keys

References and keys are the mechanism that lets a MatchAPI dictionary connect one definition to another without duplicating the target definition.

For example, a field references a data type, and a message references fields, components, and groups.

## What a key is

A key is a set of properties that uniquely identifies an element within a collection.

For example, a field might be identified by:

```text
name + variant
```

or by:

```text
id
```

The `keys` section tells consumers which properties should be used to identify and reference elements.

## Why keys exist

Keys exist so that tools can:

- resolve references consistently;
- detect duplicate definitions;
- support protocol-specific identifiers;
- support variants of the same logical element;
- compare dictionaries across versions.

Without keys, a consumer would have to guess whether a reference such as `{"name": "Symbol"}` should match by name, id, uuid, variant, or some combination of those properties.

## Primary and alternate keys

Each key definition has:

| Property | Meaning |
|---|---|
| `primaryKey` | The key used when resolving references |
| `alternateKeys` | Additional uniqueness rules that consumers or validators may check |

The primary key is the reference key. Alternate keys are useful for detecting duplicates and preserving other forms of identity, but they are not the normal reference mechanism.

Example:

```json
{
  "keys": {
    "fields": {
      "primaryKey": ["id"],
      "alternateKeys": [["name", "variant"]]
    }
  }
}
```

With this key definition, field references should use `id`:

```json
{
  "refType": "field",
  "refKey": {
    "id": "55"
  }
}
```

The dictionary may still require each field `name + variant` combination to be unique because it is listed as an alternate key.

## Default keys

If a primary key is omitted, most element collections default to:

```text
name + variant
```

If `variant` is omitted, it defaults to:

```text
base
```

This means the following reference normally resolves to the `base` variant of the `Symbol` field:

```json
{
  "refType": "field",
  "refKey": {
    "name": "Symbol"
  }
}
```

Enumerated values are different. Their default primary key is `name`, with `value` as an alternate key.

## Choosing a key

| Situation | Suggested primary key |
|---|---|
| The protocol has stable numeric or coded identifiers | `id` |
| Names are stable and unique for each variant | `name`, `variant` |
| The same element name has multiple forms | include `variant` |
| Names or protocol identifiers may change | `uuid` |
| Enum symbols are stable but encoded values also need uniqueness | primary `name`, alternate `value` |

Use explicit keys when publishing a public dictionary if the dictionary depends on protocol ids, message type codes, variants, or any identity rule that should not be left implicit.

## Reference resolution

A consumer can resolve a reference with this process:

1. Determine the target collection from the reference location or `refType`.
2. Find the primary key for that collection.
3. Read the same properties from the reference object.
4. Apply default values, such as `variant: "base"`, where appropriate.
5. Find exactly one target element with matching key values.
6. Report an error if no element or more than one element matches.

## Example: field type reference

A field references its data type through `typeRef`:

```json
{
  "name": "ClOrdID",
  "typeRef": {
    "name": "String"
  }
}
```

If data types use the default primary key, this resolves to the `String` data type with variant `base`.

## Example: message child reference

A message references child elements through `content`:

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

The `refType` tells the consumer to look in `content.fields`. The `refKey` identifies the referenced field using the field collection primary key.

## Related pages

- [[Core Concepts|Core-Concepts]]
- [[Consumer Guide|Consumer-Guide]]
- [[Publisher Guide|Publisher-Guide]]
- [[Validation]]

