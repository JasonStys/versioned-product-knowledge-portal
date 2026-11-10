# Relay Knowledge Portal

[![CI](https://github.com/JasonStys/versioned-product-knowledge-portal/actions/workflows/ci.yml/badge.svg)](https://github.com/JasonStys/versioned-product-knowledge-portal/actions/workflows/ci.yml)
[![CodeQL](https://github.com/JasonStys/versioned-product-knowledge-portal/actions/workflows/codeql.yml/badge.svg)](https://github.com/JasonStys/versioned-product-knowledge-portal/actions/workflows/codeql.yml)

A static-first, version-aware product documentation portal built with Astro and strict TypeScript.
It demonstrates how a knowledge experience can keep product applicability, lifecycle status, source
evidence, accessible presentation, and measured search quality attached to every answer.

All products, identifiers, procedures, and source records are synthetic. This repository is an
independent portfolio project and is not operating guidance for real equipment.

## 60-second quick start

Prerequisites: Node.js 22.19–24 and pnpm 11.

```bash
pnpm install --frozen-lockfile
pnpm dev
```

Open `http://localhost:4321`, select **Search**, choose version `2.0`, and search for `E-104`.
Change the filter to `1.5` to see why version context is part of the retrieval contract.

Select **Compare** to choose two versions of one product and a stable topic. For example, compare
Apex `1.5` to `2.0`, `error-e-104`: the same diagnostic identity changes from an address conflict to
a certificate-validity problem. Both exact editions, warnings, applicability and provenance stay
visible; the application never combines their procedures. Every topic links to comparisons against
its other known versions. Comparison URLs are shareable static pages and work without JavaScript.

Run the complete non-browser quality gate:

```bash
pnpm validate
```

Install Chromium once and run the browser/accessibility suite:

```bash
pnpm exec playwright install chromium
pnpm test:e2e
```

## What this proves

- **Version correctness:** every canonical URL includes product, version, and topic slug; reused
  diagnostic codes are disambiguated by explicit filters.
- **Edition review:** compare exact section text, ordered steps, code and every warning field by
  stable topic/section identity. Added, absent, changed and unchanged content is labeled, including
  warnings omitted by an older edition and topics absent from a retired version. Absence is never
  treated as proof a feature or risk disappeared.
- **Measured lexical retrieval:** a bounded inverted index uses BM25-style scoring, field weights,
  exact-identifier boosts, reviewed synonyms, deterministic tie-breaking, and a 50-query judgment
  set.
- **Grounded behavior:** the experimental answer panel repeats only a retrieved source summary,
  cites versioned pages, and abstains below a relevance threshold.
- **Accessible delivery:** semantic landmarks, skip navigation, visible focus, non-color-only
  status, 320-pixel reflow, keyboard tests, and Playwright/axe checks cover the automated portion of
  the accessibility plan.
- **Reviewable provenance:** every topic exposes its synthetic source ID, page references, and
  SHA-256 checksum.
- **Safe static operation:** public pages need no application server, database, credentials, or
  client-side access-control assumptions.

## Architecture at a glance

```mermaid
flowchart LR
    A[Validated JSON topics] --> B[Astro content collection]
    B --> C[Version-qualified static routes]
    B --> D[Search-document adapter]
    D --> E[Bounded inverted index]
    E --> F[Ranked results]
    F --> G[Cited extract or abstention]
    C --> H[Link, budget, keyboard, reflow, and axe checks]
    E --> I[50-query relevance evaluation]
```

The public site is generated at build time. Browser JavaScript initializes the search panel and
comparison chooser, applies product/version filters, ranks local documents, and creates results with
`textContent`. Comparison contents are rendered at build time with separate source columns and
complete notices. See [architecture](docs/architecture.md) and
[ADR 0001](docs/adr/0001-static-first-portal.md).

## Major features

### Product and version model

`src/data/products.ts` defines two invented product families and their current, maintained, and
retired versions. `src/content.config.ts` blocks the build when a topic violates identifiers, dates,
lifecycle, provenance, section, or complete-warning requirements.

### Search and answers

`src/lib/search.ts` builds an in-memory inverted index in O(T) time, where T is the number of
indexed tokens. Query work is O(P + R log R), where P is the total postings visited and R is the
number of matching documents. The corpus is intentionally small; the ADR describes when to replace
the local index with a dedicated service.

Exact identifiers such as `E-104` and `REG-40001` receive a separate boost. Query expansion is
limited to a reviewed synonym map, and product/version filtering happens before scoring. The answer
mode never invokes a model or tool—it returns a source summary and citations or an explicit
abstention.

### Version comparison

The comparison workflow matches a topic only within one product and two catalog versions. It keeps
missing counterparts explicit, shows retired/maintained applicability, compares source-ordered
sections and warnings, and preserves canonical links, source IDs, pages and checksums in both
columns. A reused identifier does not imply equivalent meaning. Reverse links and stable URLs let a
support engineer or documentation reviewer share the same review context. The chooser navigates only
to an allowlisted generated route. Keyboard, mobile, no-JavaScript, missing-topic and warning review
flows are exercised against the actual built site.

See [the edition comparison guide](docs/edition-comparison.md) for realistic walkthroughs and
bounds, and [latest validation](docs/reports/comparison-2026-11-09.md) for measured results.

### Validation evidence

`pnpm validate` checks formatting, lint, strict types, branch coverage, production build, internal
links, static-asset budgets, and search relevance. GitHub Actions repeats the gate on Node 22 and
24; a separate Chromium job tests keyboard behavior, mobile reflow, version filtering, and
detectable WCAG A/AA violations. Reports are retained as workflow artifacts.

The separate [CodeQL workflow](.github/workflows/codeql.yml) analyzes authored JavaScript/TypeScript
and GitHub Actions with `security-extended` queries on main pushes, pull requests, a weekly
schedule, and manual requests. It uploads processed findings to GitHub's **Security → Code
scanning** view. No-build source analysis does not execute the site or certify Astro template
escaping, content correctness, accessibility, or absence of vulnerabilities; the existing build and
browser gates remain required. See [scan coverage and review](docs/security-model.md#code-scanning).

## Repository map

| Path                    | Purpose                                                                           |
| ----------------------- | --------------------------------------------------------------------------------- |
| `src/content/topics/`   | Schema-validated synthetic product knowledge.                                     |
| `src/lib/`              | Content adapters, contracts, redirects, search engine, and browser binding.       |
| `src/pages/`            | Static landing, catalog, search, version, topic, about, and 404 routes.           |
| `src/components/`       | Accessible lifecycle, warning, topic, version, and search components.             |
| `src/styles/global.css` | Responsive tokens and component styles, including print/reduced motion.           |
| `tests/unit/`           | Search, data integrity, redirect, repository-policy, and adapter tests.           |
| `tests/e2e/`            | Keyboard, reflow, search, topic, and axe browser tests.                           |
| `tools/`                | Search evaluation, link/budget validation, topic loading, and symbol indexes.     |
| `docs/`                 | Architecture, contracts, ADRs, security, accessibility, operations, and evidence. |
| `.github/`              | Least-privilege CI and grouped dependency updates.                                |

The [file reference](docs/file-reference.md) explains every authored or generated file.

## Commands

| Command                | Result                                                  |
| ---------------------- | ------------------------------------------------------- |
| `pnpm dev`             | Local Astro development server.                         |
| `pnpm build`           | Reproducible static build in `dist/`.                   |
| `pnpm test:coverage`   | Unit and policy tests with enforced branch coverage.    |
| `pnpm test:e2e`        | Chromium desktop/mobile and accessibility checks.       |
| `pnpm evaluate:search` | JSON and Markdown relevance evidence from 50 judgments. |
| `pnpm validate:links`  | Internal-link crawl and JavaScript/CSS budget report.   |
| `pnpm update:headers`  | Regenerate line-accurate file symbol indexes.           |
| `pnpm validate`        | Complete non-browser validation gate.                   |

## Documentation

- [Architecture and complexity](docs/architecture.md)
- [Edition comparison](docs/edition-comparison.md)
- [Content and URL contracts](docs/content-model.md)
- [Search evaluation](docs/search-evaluation.md)
- [Testing and validation](docs/testing-and-validation.md)
- [Accessibility](docs/accessibility.md)
- [Security model](docs/security-model.md)
- [Operations and rollback](docs/operations.md)
- [File reference](docs/file-reference.md)
- [Research references](docs/references.md)
- [Contributing](CONTRIBUTING.md) and [security reporting](SECURITY.md)

## Limitations

- The corpus and judgment set are synthetic and small; reported relevance does not generalize to a
  commercial documentation estate.
- Automated accessibility checks find only a subset of barriers and do not establish conformance.
- The answer preview is extractive—not semantic or generative—and has no authorization layer because
  the repository contains only public sample content.
- The redirect manifest must be applied by a hosting adapter; static object storage alone cannot
  emit HTTP redirect status codes.
- No procedure in this demonstration should be used to control or service real equipment.

## Maintenance evidence

See the [latest maintenance audit](docs/reports/maintenance-audit-2026-09-18.md) for the validated
default-branch run and dependency compatibility decisions.

## License

Code and synthetic content are available under the [MIT License](LICENSE).
