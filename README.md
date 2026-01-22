<p align="center">
  <img
    src="assets/Logo%20-%20MatchAPI.svg"
    alt="MatchAPI logo"
    style="max-width: 360px; width: 100%; height: auto;"
  >
</p>

<p align="center">
  <a href="schema/LICENSE">
    <img src="https://img.shields.io/badge/license-Apache%202.0-blue.svg" alt="License">
  </a>
  <img src="https://img.shields.io/badge/type-schema-lightgrey.svg" alt="Schema">
</p>

<strong>MatchAPI is a machine-readable schema for describing financial messaging interfaces across binary, proprietary, and FIX protocols.</strong>

The current core schema version is [`matchapi-core-1.0.0.json`](schema/matchapi-core-1.0.0.json)

## Contents

- [Introduction](#introduction-to-matchapi-schema)
- [Motivation and Background](#motivation-and-background)
- [Positioning MatchAPI](#positioning-matchapi-vs-existing-standards)
- [Core Concepts](#core-concepts)
- [Key Use Cases](#key-use-cases)
- [Licensing](#licensing)
- [Compliance and Branding](#matchapi-compliance-and-branding)

# Introduction to MatchAPI schema

MatchAPI is a unified, machine-readable standard for describing financial messaging interfaces across binary, proprietary, and FIX-based protocols.

It provides a structured representation of message models, data types, business semantics, and protocol-level configuration, including structural constraints and descriptive metadata that may be used for validation.

Modern financial systems operate across a wide range of technologies, including proprietary binary protocols, venue-specific formats, REST, WebSocket, FIX, SBE, and FIXML. Traditionally, each protocol family required its own documentation format, tooling, and integration approach.

MatchAPI introduces a technology-neutral schema that allows these APIs to be described using a common model, independent of encoding, transport, or implementation language.

Its schema is defined using an open, JSON-compatible format and can be authored in JSON, JSON5, or YAML. This makes MatchAPI suitable for modern development pipelines, CI/CD workflows, API documentation systems, and schema-driven tooling.

MatchAPI v1.0 is intended as a foundational release. It establishes a stable core model on which additional capabilities may be layered over time, informed by practical usage and feedback from protocol owners, implementers, and integrators.

---

## Motivation and Background

Financial institutions typically operate a mix of legacy and modern interfaces, including:

- Proprietary and venue-specific binary protocols
    
- FIX with different session layers and encodings
    
- Proprietary, FIX, or SBE market-data protocols
    
- REST/JSON and WebSocket interfaces for ancillary or post-trade services
    

This diversity leads to recurring challenges:

- Fragmented documentation formats (PDFs, spreadsheets, proprietary schemas)
    
- Non-standardized semantics, particularly for binary protocols
    
- Inconsistent interpretation of message structures and constraints
    
- Limited reuse of tooling across venues and APIs
    
- High onboarding and long-term maintenance costs
    

MatchAPI addresses these challenges by providing a shared, protocol-agnostic structure that captures both business-level intent and protocol-level details in a single source of truth.

---

## Core Concepts

MatchAPI describes a protocol using a structured set of interconnected components.

### Data Types and Enumerations

A normalized catalog of primitive and composite types, including:

- Scalar types (integer, decimal, boolean, string)
    
- Encoded and binary representations
    
- Enumerations with explicit semantic meaning

### Fields, Groups, and Components

Reusable definitions that specify:

- Identifiers (names, numeric IDs, tags)
    
- Structural constraints and descriptive conditions
    
- Optional metadata and extensions

### Message Definitions

Each message definition captures:

- Business purpose and intent
    
- Required, optional, and conditional fields
    
- Structural layout and composition

---

## Key Use Cases

MatchAPI is a general-purpose schema, particularly suited for:

- **API communication with counterparties**  
    Sharing portable, machine-readable dictionaries that can be automatically ingested.
    
- **Normalization and interoperability**  
    Mapping proprietary APIs, binary feeds, and FIX variants into a unified internal model.
    
- **Conformance and certification support**  
    Serving as input for automated validation and test tooling built around published schemas.
    
- **Internal self-consistency checks**  
    Verifying that implementations remain aligned with published specifications.
    
- **Documentation generation**  
    Producing up-to-date, human-readable documentation from a single authoritative source.
    
- **DevOps and CI/CD integration**  
    Embedding schema checks into build pipelines to detect incompatible changes early.
    
---

## Community Feedback

MatchAPI is published as an open specification, and feedback from implementers and integrators is welcome.

Comments, issues, and suggestions may be submitted via GitHub Issues. Feedback from users of financial protocols is particularly valuable in guiding how the standard evolves beyond its foundational scope.

---
> [!IMPORTANT]
> MatchAPI JSON Schema and provided documentation are the intellectual property of [Esprow Pte. Ltd](https://www.esprow.com/).
> 
> MatchAPI™ is a trademark of Esprow Pte. Ltd. All rights reserved.

---

## Licensing

- The JSON Schema files are licensed under the **Apache License 2.0**, with an additional clause prohibiting misrepresentation and unauthorized rebranding.
- The documentation is licensed under the **Creative Commons Attribution-NoDerivatives 4.0 International (CC BY-ND 4.0)** license. You may share it, but you may not modify or adapt it.

For complete terms, please refer to [LICENSE](https://matchapi.org/license)

## Summary of Allowed Uses

You may:
- Use the schema internally or commercially.
- Modify the schema for internal use.
- Redistribute modified schemas (with attribution and without using the MatchAPI name).
- Share the documentation in its original form.
- Create and distribute your own protocol dictionaries that conform to the schema.

You may not:
- Use the MatchAPI name or logo for derivative works without permission.
- Redistribute modified documentation.
- Claim authorship or rebrand the schema as your own.

## MatchAPI Compliance and Branding

If your protocol dictionary validates against the official MatchAPI JSON Schema without modification, you may state that it is:

    “MatchAPI-compliant”

You may not:
- Claim that your dictionary is an official MatchAPI dictionary.
- Use the term “MatchAPI” in your product name, title, or brand without prior permission.
- Use the MatchAPI logo, trademark, or other brand assets unless licensed separately.

## Vendor/Project-Specific Extensions

To avoid naming conflicts with current or future versions of the MatchAPI schema, you are encouraged to use the **`x-` prefix** for any custom fields or metadata.

### Example:
```json
{
  "name": "OrderQty",
  "typeRef": { "id": "..." },
  "x-internalCode": "OQ123",
  "x-notes": "Used only for test orders"
}
```

These fields will be ignored by MatchAPI tooling unless explicitly supported.

## Licensing and Contact

For questions about licensing, branding, or partnership opportunities, please contact Esprow at info@esprow.com.
