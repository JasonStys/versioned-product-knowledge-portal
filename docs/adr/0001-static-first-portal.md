# ADR 0001: Static-first Astro portal

- Status: Accepted
- Date: 2026-09-16

## Context

Public documentation needs fast delivery, stable URLs, previewable builds, low operational
complexity, and strict content validation. The current scope does not need per-request identity,
writes, or server rendering.

## Decision

Use Astro content collections with static output and strict TypeScript. Keep canonical topics as
JSON and emit version-qualified HTML at build time.

## Alternatives

- **Docusaurus:** strong documentation conventions and versioning, but the custom
  content/provenance/search model would work against its opinionated structure.
- **Next.js:** appropriate when authenticated dynamic retrieval or server components are required;
  unnecessary runtime and deployment surface for this public corpus.
- **Hand-written generator:** smallest dependency surface but would recreate routing, build, and
  component behavior.

## Consequences and revisit trigger

Build failures catch content errors before publication, output can use immutable hosting, and
runtime attack surface is small. Revisit when server-enforced authorization, per-request
personalization, or frequently updated live content becomes a concrete requirement.
