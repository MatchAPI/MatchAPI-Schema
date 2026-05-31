# Consumer Guide

This guide is for developers building tools that read MatchAPI dictionaries.

## Recommended processing order

1. Parse the JSON document.
2. Validate it against the MatchAPI Core JSON Schema.
3. Load the `keys` section and establish default keys where omitted.
4. Build lookup indexes for each collection.
5. Check primary and alternate key uniqueness.
6. Resolve references.
7. Apply documentation, classifier, additional data, and change log information as needed.

## Build lookup indexes

For each collection in `content`, build indexes using the collection primary key and any alternate keys.

Common collections are:

| Collection | Typical use |
|---|---|
| `dataTypes` | Resolve `typeRef`, `baseTypeRef`, `valuesTypeRef`, and `elementsTypeRef` |
| `fields` | Resolve field references from messages, components, and groups |
| `components` | Resolve reusable component references |
| `groups` | Resolve repeating group references |
| `messages` | Inspect or generate message-level documentation and tooling |

## Resolve references after indexing

References should be resolved after indexes are built. This avoids ordering assumptions in the JSON file.

A dictionary producer may list fields before data types, messages before components, or use another ordering. Consumers should not depend on array order except where the schema defines ordered content within a message, component, group, or composite type.

## Treat JSON Schema validation as the first check

JSON Schema validation confirms that the document has the expected shape. It does not prove that references resolve, keys are unique, or business rules are complete.

Production consumers should add semantic checks for:

- unresolved references;
- duplicate primary keys;
- duplicate alternate keys;
- invalid or unsupported variants;
- enum value consistency;
- publisher-specific rules.

## Handle unknown data carefully

The core schema does not allow arbitrary properties in most locations. Publisher-specific data should appear through schema-defined mechanisms such as `additionalData`, where available.

Consumers should preserve additional data they do not understand when round-tripping a dictionary, but should avoid interpreting it unless the producer's convention is known.

## Generate useful diagnostics

When reporting errors, include:

- the JSON path of the source reference or element;
- the target collection;
- the key values used;
- whether the error is structural, semantic, or publisher-specific.

Good diagnostics make dictionaries easier to publish and adopt.

## Related pages

- [[Getting Started|Getting-Started]]
- [[References and Keys|References-and-Keys]]
- [[Validation]]
- [[Examples]]

