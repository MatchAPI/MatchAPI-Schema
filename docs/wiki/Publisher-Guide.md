# Publisher Guide

This guide is for organisations publishing MatchAPI dictionaries.

## Publish a valid dictionary

Before publishing a MatchAPI dictionary:

1. Validate the JSON document against `schema/matchapi-core-1.0.0.json`.
2. Check reference resolution.
3. Check key uniqueness.
4. Check that the dictionary version is clear.
5. Check that documentation entries do not disclose confidential implementation details.
6. Check that licensing and attribution notices are included where required.

## Use stable identifiers

Where possible, use stable identifiers for elements.

The schema supports:

- `uuid`;
- `id`;
- `name`;
- `variant`.

For protocol-specific elements, `id` can be used for identifiers such as FIX tags or other protocol-defined codes.

## Define keys deliberately

The `keys` section controls how elements are uniquely identified and referenced.

If you omit keys, the default primary key for most element types is `name` and `variant`.

For public dictionaries, define keys explicitly if your API uses:

- numeric field identifiers;
- message type codes;
- variants;
- duplicate names across contexts;
- protocol-specific identifiers.

See [[References and Keys|References-and-Keys]].

## Use variants consistently

Use `variant` when the same logical element has different forms for different use cases.

Avoid creating variants where a separate named element would be clearer.

## Use categories and sections for navigation

The `classifiers.categories` and `classifiers.sections` collections are useful for documentation and human navigation.

For example, a publisher may group messages by business area or group fields by functional section.

## Keep additional data controlled

Use `additionalData` for implementation-specific data and mappings.

Avoid placing sensitive internal details into public dictionaries unless they are intended for publication.

## Maintain change logs

Use `changeLog` entries for definitional changes, deprecations, replacements, and significant editorial updates.

For public dictionaries, change logs help consumers understand the impact of a new version.

## Publish examples carefully

If publishing example dictionaries:

- ensure they validate against the schema;
- ensure they do not contain client-confidential API details;
- make clear whether they are illustrative or authoritative;
- keep them aligned with the current schema version.

## Avoid tool lock-in

MatchAPI is intended to be consumable by any toolchain that can parse JSON.

Publishers should avoid presenting MatchAPI as dependent on a particular programming language or implementation toolkit.

## Related pages

- [[References and Keys|References-and-Keys]]
- [[Validation]]
- [[Versioning and Compatibility|Versioning-and-Compatibility]]
- [[Licensing and Attribution|Licensing-and-Attribution]]
