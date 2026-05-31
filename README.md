<p align="center">
  <img
    src="assets/Logo%20-%20MatchAPI.svg"
    alt="MatchAPI logo"
    width="360"
  >
</p>

# MatchAPI

MatchAPI is a JSON Schema-based format for describing financial messaging APIs.

It is intended for developers, integrators, exchanges, brokers, banks, and software vendors who need a machine-readable description of message structures, fields, data types, repeating groups, components, variants, and protocol-specific constraints.

The core schema is published as:

```text
https://matchapi.org/schema/matchapi-core-1.0.0.json
```

## What problem does MatchAPI solve?

Financial messaging APIs are often described in PDFs, spreadsheets, proprietary dictionaries, or protocol-specific formats. This makes it difficult to:

- ingest specifications automatically;
- compare message models across protocols;
- generate documentation consistently;
- validate dictionaries before publication;
- use the same downstream tooling across FIX, proprietary binary protocols, JSON-based APIs, and other financial interfaces.

MatchAPI provides a neutral, machine-readable model for describing these APIs in JSON-compatible form.

## Who is this repository for?

This repository is primarily for developers who have received a MatchAPI JSON file and need to understand:

- what the file represents;
- how to validate it;
- how to inspect the messages, fields, data types, components, and groups it defines;
- how to consume the file in their own tooling.

## Repository contents

```text
schema/
  matchapi-core-1.0.0.json     Core MatchAPI JSON Schema

docs/
  README.md                    Documentation source notes
  wiki/                        Versioned source files for the GitHub Wiki

examples/
  minimal-api.matchapi.json    Minimal valid MatchAPI dictionary
  README.md                    Notes on examples

LICENSE
NOTICE.md
ATTRIBUTION.md
CHANGELOG.md
CONTRIBUTING.md
```

## Quick start

A MatchAPI file is a JSON document with three required top-level properties:

- `name` – the API name;
- `version` – the API version;
- `content` – the API model, including messages, fields, groups, components, and data types.

A minimal valid dictionary can be found in:

```text
examples/minimal-api.matchapi.json
```

To validate a MatchAPI file, use any JSON Schema validator that supports JSON Schema Draft 2020-12.

The schema file is:

```text
schema/matchapi-core-1.0.0.json
```

See [Validation](docs/wiki/Validation.md) for details.

## Documentation

The latest documentation is available in the repository Wiki.

The source for the Wiki lives in `docs/wiki/` so documentation is versioned with schema releases. For older schema versions, browse the matching repository tag and read `docs/wiki/`.

Start here in the source documentation:

- [Getting Started](docs/wiki/Getting-Started.md)
- [User Guide](docs/wiki/User-Guide.md)
- [Core Concepts](docs/wiki/Core-Concepts.md)
- [References and Keys](docs/wiki/References-and-Keys.md)
- [Consumer Guide](docs/wiki/Consumer-Guide.md)
- [Publisher Guide](docs/wiki/Publisher-Guide.md)
- [Validation](docs/wiki/Validation.md)
- [Examples](docs/wiki/Examples.md)
- [Versioning and Compatibility](docs/wiki/Versioning-and-Compatibility.md)
- [Licensing and Attribution](docs/wiki/Licensing-and-Attribution.md)
- [FAQ](docs/wiki/FAQ.md)

## Scope of the core schema

MatchAPI Core 1.0.0 defines a dictionary structure for financial messaging APIs. It includes:

- API metadata;
- data types;
- fields;
- components;
- repeating groups;
- messages;
- references between definitions;
- variants;
- categories and sections;
- documentation entries;
- additional data entries;
- change log entries;
- element key definitions.

It does not prescribe a particular programming language, runtime, validation tool, documentation generator, or transport implementation.

## Extension model

The core schema does not allow arbitrary additional properties at the top level or in most defined objects. Implementation-specific data should be carried through the schema-defined `additionalData` mechanism, where supported.

## Feedback

Please use GitHub Issues for schema feedback, documentation issues, or clarification requests.

Do not post confidential, proprietary, or client-specific API dictionaries in public issues.
