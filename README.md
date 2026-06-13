# Astrel Config Schema

Public JSON Schema for Astrel remote config payloads. SDKs and CI validate published configs against these files.

Canonical host: **https://schema.astrel.io**

## Versions

| Version | Status  | Released   | Deprecated | Sunset | URL |
|---------|---------|------------|------------|--------|-----|
| v1      | current | 2026-06-13 | -          | -      | https://schema.astrel.io/v1/astrel-config.schema.json |

Machine-readable version of this table: [`index.json`](https://schema.astrel.io/index.json)

## Referencing the schema

Always pin to a major version URL. It is an immutable contract and will keep returning the same schema:

```
https://schema.astrel.io/v1/astrel-config.schema.json
```

A config payload declares which major it targets via `schema_version`. That integer always equals the directory major, so a payload with `"schema_version": 1` validates against `/v1/`.

## Versioning policy

**A new major version (new directory) is cut only for breaking changes:**

- Removing or renaming a field
- Changing a field's type
- Making an optional field required
- Tightening validation so configs that previously passed now fail
- Adding a value to an enum that SDKs match exhaustively (e.g. the lottery `algorithm`)

**Non-breaking changes are revised in place, no new directory:**

- Adding optional fields
- Loosening validation
- Clarifying descriptions

Every change, breaking or not, is tagged as a GitHub Release for an immutable, changelogged snapshot.

## Deprecation policy

Published version files are **never deleted**, even after sunset, so historic configs and old pinned SDKs always have something to validate against.

Lifecycle: `current` → `supported` → `deprecated` (sunset date set) → `sunset`.

Deprecated versions are supported for at least **6 months** before sunset. When a version is deprecated, its schema file gains a top-level annotation:

```json
"x-astrel-status": "deprecated",
"x-astrel-sunset": "2026-12-13"
```

Status definitions are documented in `index.json`.
