# Introduction to MatchAPI schema

MatchAPI is an open, unified, machine-readable standard designed to describe financial APIs for both FIX and non-FIX protocols. It is published under the Apache 2.0 License and currently supports JSON, JSON5, and YAML formats, with XML support coming soon.
Its schema design consolidates message definitions, data types, and business semantics – making it ideal for integration with modern API documentation tools, development pipelines, and testing systems.

**_In essence, MatchAPI acts as a bridge between the traditional financial messaging world and the modern API ecosystems._**

MatchAPI was developed in collaboration with major financial institutions to provide a technology-neutral format for exchanging, validating, and testing APIs, enabling seamless interaction between legacy systems and modern architectures.

**MatchAPI Key Advantages:**

- **Open & Portable** – Easy to integrate with in-house systems and open-source tools.

- **Cross-Protocol** – Supports FIX, FIXML, SBE, REST, and more.

- **Future-Proof** – Designed for automation, AI-assisted analysis, and seamless DevOps integration.


This repository contains the official MatchAPI JSON Schema standard and documentation.


> [!IMPORTANT]
> MatchAPI JSON Schema and provided documentation are the intellectual property of [Esprow Pte. Ltd](https://www.esprow.com/).
> 
> MatchAPI™ is a trademark of Esprow Pte. Ltd. All rights reserved.


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
