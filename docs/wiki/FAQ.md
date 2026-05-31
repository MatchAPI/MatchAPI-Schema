# FAQ

## What is MatchAPI?

MatchAPI is a JSON Schema-based format for describing financial messaging APIs in a structured, machine-readable way.

## Is MatchAPI tied to one protocol?

No. MatchAPI is intended to be protocol-neutral. It can describe FIX-style protocols, proprietary binary protocols, JSON-based APIs, and other financial messaging interfaces.

## Is JSON Schema validation enough?

No. JSON Schema validation checks the document structure. Production use should also check semantic consistency, including reference resolution and key uniqueness.

## When should I define explicit keys?

Define explicit keys when the dictionary depends on protocol ids, message type codes, variants, duplicate names across contexts, or any identity rule that should be clear to consumers.

## Should I use `name`, `id`, or `uuid` as a key?

Use `name` when names are stable and unique. Use `id` when the protocol has stable identifiers such as field tags or message codes. Use `uuid` when names or protocol identifiers may change or collide.

## What does `variant` do?

`variant` distinguishes different forms of the same logical element. If omitted, it defaults to `base`.

## Can I add custom properties?

Not in most schema-defined objects. Use `additionalData`, where available, for implementation-specific information.

## Where are older docs?

The Wiki shows the latest synced documentation. Older documentation is available in repository tags under `docs/wiki/`.

