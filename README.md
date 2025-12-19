# Introduction to MatchAPI schema

MatchAPI is a unified, machine-readable standard for describing financial messaging interfaces across both FIX and non-FIX protocols.

It provides a single, structured representation of message models, data types, business semantics, validation rules, workflows, and protocol-level configuration — designed to be portable, analyzable, and automation-ready.

Modern financial systems operate across a wide range of technologies, including FIX, proprietary binary protocols, REST, WebSocket, FIXML, SBE, and venue-specific formats. Traditionally, each protocol family required its own documentation format, tooling, and integration approach.  
MatchAPI introduces a technology-neutral schema that unifies these APIs under a common model.

Its schema is defined using an open, JSON-compatible format and can be authored in JSON, JSON5, or YAML, with XML support planned. This makes MatchAPI well suited for modern development pipelines, CI/CD workflows, API documentation systems, and automated validation tooling.

**In essence, MatchAPI bridges the gap between traditional financial messaging systems and modern API ecosystems.**

MatchAPI was developed in collaboration with major financial institutions to provide a stable foundation for exchanging, validating, testing, and evolving financial APIs across heterogeneous environments.

---

## Motivation and Background

Financial institutions typically operate a mix of legacy and modern interfaces, including:

- FIX with multiple session layers and encodings  
- Venue-specific binary APIs  
- Proprietary order-entry and market-data protocols  
- REST/JSON and WebSocket interfaces for ancillary or post-trade services  

This diversity leads to recurring challenges:

- Fragmented documentation formats (PDFs, spreadsheets, proprietary schemas)  
- Non-standardized semantics, particularly for binary protocols  
- Inconsistent validation and complex certification processes  
- Limited reuse of tooling across venues and APIs  
- High onboarding and long-term maintenance costs  

MatchAPI was created to address these challenges by providing a shared, protocol-agnostic structure that captures both business-level intent and protocol-level details.  
This enables APIs to be documented, validated, tested, and automated using a single source of truth.

---

## Positioning MatchAPI vs Existing Standards

MatchAPI draws inspiration from existing industry standards such as **QuickFIX XML and others**, while expanding beyond their scope.

### Business Semantics First

While **QuickFIX XML focuses on describing FIX message structure**, MatchAPI standardizes:

- Business meaning  
- Validation rules and constraints  
- Workflow and behavioral semantics  
- Permitted encoding and transport options  

This allows documentation, validation logic, and test cases to be generated from the same definition.

### Multi-Protocol and Encoding-Neutral by Design

Existing standards based on **FIX tag-based encodings** are primarily optimized for FIX-style messages, making binary protocols harder to model and work with.

MatchAPI is designed to support:

- FIX (tag=value, FIXML, FAST, SBE)  
- Proprietary and venue-specific binary protocols  
- Hybrid and vendor-defined message formats  

The schema is encoding-neutral, capable of describing both fixed-layout binary messages and self-describing formats.

### Modern Authoring Formats

MatchAPI uses JSON, JSON5, and YAML for authoring, making it compatible with:

- Continuous Integration pipelines  
- Modern API documentation frameworks  
- Code generation tools  
- Cloud-native and DevOps-oriented workflows  

This contrasts with older XML-centric specifications and allows MatchAPI artifacts to be consumed using standard parsing, linting, and validation tooling.

---

## Core Concepts

MatchAPI describes a protocol using a structured set of interconnected components:

### Data Types and Enumerations

A normalized catalog of primitive and composite types, including:

- Scalar types (integer, decimal, boolean, string)  
- Encoded and binary representations  
- Enumerations with explicit semantic meaning  

### Fields and Components

Reusable definitions that specify:

- Identifiers (tags, names, numeric IDs)  
- Constraints and validation rules  
- Optional metadata and extensions  

### Message Definitions

Each message definition captures:

- Business purpose and intent  
- Required, optional, and conditional fields  
- Structural layout and composition  

---

## Key Use Cases

MatchAPI is a general-purpose schema, particularly suited for:

### API Communication with Counterparties

Sharing portable, machine-readable dictionaries that can be automatically ingested.

### Normalization and Interoperability

Mapping FIX variants, binary feeds, and proprietary APIs into a unified internal model.

### Conformance and Certification Testing

Generating automated validation and test suites based on schema definitions.

### Internal Self-Validation

Ensuring implementations remain aligned with published specifications.

### Documentation Generation

Producing up-to-date, human-readable documentation from a single authoritative source.

### DevOps and CI/CD Integration

Embedding schema validation into build pipelines to prevent incompatible changes.

This repository contains the official MatchAPI JSON Schema standard and documentation.

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
