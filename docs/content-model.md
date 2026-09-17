# Content and URL contracts

## Product lifecycle

`src/data/products.ts` is the catalog authority. Each product version is `current`, `maintained`, or
`retired` and can include an end-of-support date. The state appears as text and a shape, and
non-current topic pages add a banner before procedures.

## Topic contract

Each JSON topic contains:

- stable `id`, `topicSlug`, `productId`, product name, and explicit version;
- lifecycle, content type, updated date, public visibility, identifiers, and reviewed synonyms;
- provenance source ID, source pages, and SHA-256 checksum;
- one or more sections with paragraphs and optional steps, code, or a complete warning;
- warnings with severity, condition, consequence, and avoidance.

Astro validates the contract with Zod at build time. Runtime tools perform a smaller defensive check
before using JSON outside Astro.

## URL policy

Canonical topics use `/docs/{product-id}/{version}/{topic-slug}/`. Product landing pages use
`/products/{product-id}/{version}/`. The trailing slash is intentional and enforced by the build.

Published canonical routes should not be reassigned. When a route must change, add a reviewed
mapping to both `src/lib/redirects.ts` and `public/redirects.json`; the synchronization test
prevents drift. Redirects must be root-relative and cannot point to an external host.

## Applicability and deprecation

A topic describes exactly one product/version pair. Shared source content may be duplicated into
canonical version topics only when its applicability is reviewed. Retired content remains findable
for installed-base users but is labeled, filtered, and linked to migration guidance.

## Import boundary

The current JSON fixtures model an export from an upstream documentation pipeline. A future importer
should validate the upstream schema, retain source checksums/page mappings, reject duplicate
canonical routes, and produce a deterministic diff before replacing this directory.
