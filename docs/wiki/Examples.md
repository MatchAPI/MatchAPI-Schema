# Examples

The repository includes example MatchAPI dictionaries under:

```text
examples/
```

## Minimal example

`examples/minimal-api.matchapi.json` is a small valid MatchAPI dictionary intended to show the basic document structure.

Use it to confirm that a parser or validator can load a MatchAPI document.

## How to read examples

When reading an example dictionary, use this order:

1. Inspect the top-level `name`, `version`, and `content` properties.
2. Read `keys`, if present, to understand identity and reference rules.
3. Read `content.dataTypes`.
4. Read `content.fields`.
5. Read `content.components` and `content.groups`.
6. Read `content.messages`.
7. Review classifiers, documentation, additional data, and change logs.

## Suggested future examples

The repository should eventually include:

| Example | Purpose |
|---|---|
| Minimal dictionary | Smallest useful schema-valid file |
| Keys-focused dictionary | Demonstrates `name`, `id`, `uuid`, and `variant` key strategies |
| Realistic dictionary | Demonstrates fields, enum values, groups, components, messages, and variants |
| Publisher example | Demonstrates metadata, documentation entries, classifiers, and change logs |

Real-world examples should only be published if the relevant API owner has approved publication.

## Related pages

- [[Getting Started|Getting-Started]]
- [[References and Keys|References-and-Keys]]
- [[Consumer Guide|Consumer-Guide]]
- [[Publisher Guide|Publisher-Guide]]

