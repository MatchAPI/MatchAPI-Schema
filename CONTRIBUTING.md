# Contributing

Feedback is welcome through GitHub Issues and pull requests.

## Do not submit confidential API dictionaries

Do not include confidential, proprietary, venue-specific, client-specific, or commercially sensitive API dictionaries in public issues or pull requests.

## Useful issue types

Good issues include:

- unclear schema documentation;
- inconsistent terminology;
- validation ambiguity;
- schema examples that do not validate;
- requests for clarification;
- proposed non-breaking documentation improvements.

## Pull request guidance

When opening a pull request:

1. Keep changes focused.
2. Explain the problem being addressed.
3. Do not modify the core schema unless the change is intentional and clearly justified.
4. Update documentation when terminology changes.
5. Ensure examples validate against the current schema.

## Schema changes

Schema changes should be treated as versioned specification changes.

A schema change may affect downstream validators, documentation generators, and published dictionaries.

## Release checklist

Before publishing a schema release:

1. Confirm schema changes are intentional and versioned.
2. Update examples when schema behavior or recommended usage changes.
3. Update `docs/wiki/` for documentation affected by the release.
4. Confirm the Wiki sync workflow has run successfully on `main`.
5. Link release notes to the matching repository tag so users can find the corresponding `docs/wiki/` documentation.
