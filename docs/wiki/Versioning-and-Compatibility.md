# Versioning and Compatibility

MatchAPI users need to distinguish between the version of the MatchAPI schema and the version of a dictionary described by that schema.

## Schema version

The schema version identifies the MatchAPI Core schema used to validate a dictionary.

For MatchAPI Core 1.0.0, the schema identifier is:

```text
https://matchapi.org/schema/matchapi-core-1.0.0.json
```

The repository stores schema files under:

```text
schema/
```

## Dictionary version

The top-level `version` property identifies the version of the API dictionary being published.

This version is controlled by the dictionary publisher. It may change when the described API changes, even if the MatchAPI schema version does not change.

## Protocol version

The optional `protocolVersion` property identifies the version of the underlying protocol or API being described.

For example, a dictionary might use MatchAPI Core 1.0.0, describe version 2.3.0 of a venue API, and use a publisher-specific dictionary version.

## Compatibility guidance

Consumers should record:

- the MatchAPI schema identifier;
- the dictionary `name`;
- the dictionary `version`;
- the optional `protocolVersion`;
- the publisher or source, where available.

Publishers should document whether a dictionary release contains:

- definitional changes;
- editorial-only changes;
- deprecated elements;
- replaced elements;
- changes that may break downstream tooling.

## Wiki and release alignment

The GitHub Wiki shows the latest documentation synced from the main branch. Historical documentation is stored in the main repository under `docs/wiki/` and is versioned through repository tags.

For an older schema release, browse the corresponding repository tag and read:

```text
docs/wiki/
```

## Related pages

- [[Validation]]
- [[Publisher Guide|Publisher-Guide]]
- [[Licensing and Attribution|Licensing-and-Attribution]]

