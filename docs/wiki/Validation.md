# Validation

MatchAPI Core 1.0.0 is defined as a JSON Schema using JSON Schema Draft 2020-12.

The schema file is:

```text
schema/matchapi-core-1.0.0.json
```

The schema identifier is:

```text
https://matchapi.org/schema/matchapi-core-1.0.0.json
```

## What validation checks

Schema validation checks that a MatchAPI dictionary has the correct JSON structure.

It checks, for example, that:

- required top-level properties are present;
- property names are valid;
- values use the expected JSON types;
- enum values use allowed values;
- required properties inside definitions are present;
- objects that disallow additional properties do not contain unsupported properties;
- arrays marked as unique do not contain duplicate JSON values;
- strings with `format` constraints, such as `uuid`, `date-time`, and `regex`, are structurally valid, depending on validator support.

## What validation does not check

Schema validation does not prove that:

- the described API is implemented by the publisher;
- messages are semantically correct;
- references point to existing definitions;
- primary keys are globally unique;
- alternate keys are globally unique;
- business rules are complete;
- generated documentation is correct;
- an implementation conforms to the described API.

Some of these checks require application-level validation beyond JSON Schema.

## Required top-level properties

A MatchAPI dictionary must contain:

```text
name
version
content
```

## Additional properties

The root object uses:

```json
"additionalProperties": false
```

Many nested objects also use `unevaluatedProperties: false`.

This means a validator should reject unsupported properties in those objects. Implementation-specific information should be represented through schema-defined mechanisms such as `additionalData`, where available.

## Minimal valid example

See:

```text
examples/minimal-api.matchapi.json
```

## Tooling-neutral validation

MatchAPI does not require a specific validator or programming language.

Use any validator that supports JSON Schema Draft 2020-12.

At a high level, the validation process is:

1. Load `schema/matchapi-core-1.0.0.json`.
2. Load the MatchAPI dictionary to validate.
3. Validate the dictionary against the schema.
4. Report validation errors with their JSON paths.

## Validation pipeline recommendation

For published dictionaries, use at least two checks:

1. **JSON Schema validation** – checks schema conformance.
2. **Dictionary consistency validation** – checks reference resolution, key uniqueness, and publisher-specific rules.

The second check is outside the scope of the core JSON Schema, but it is important for production use.

See [[References and Keys|References-and-Keys]] for guidance on reference resolution and key uniqueness.

## Common validation errors

### Unsupported property

Cause:

- A property appears in a location where the schema does not permit it.

Typical fix:

- Remove the property, or move implementation-specific information into `additionalData` where supported.

### Missing `typeRef` in a field

Field definitions require `typeRef`.

Typical fix:

```json
{
  "name": "ClOrdID",
  "typeRef": {
    "name": "String"
  }
}
```

### Missing `content` in a message, component, or group

Complex elements require `content`.

Typical fix:

```json
{
  "name": "Heartbeat",
  "msgType": "0",
  "direction": "both",
  "content": []
}
```

### Invalid direction

The only permitted message direction values are:

```text
in, out, both
```

### Invalid data type

The only permitted data type values are:

```text
primitive, derived, enum, array, composite, bitset
```

## Related pages

- [[Getting Started|Getting-Started]]
- [[References and Keys|References-and-Keys]]
- [[Consumer Guide|Consumer-Guide]]
- [[Publisher Guide|Publisher-Guide]]
