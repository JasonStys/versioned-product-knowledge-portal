# Relay Knowledge Portal handbook

By Jason Stys.

Read and compare version-qualified synthetic product documentation while retaining applicability,
complete warnings and source citations. The static portal searches its bounded local corpus and
never merges incompatible procedures.

Add shareable side-by-side edition comparisons with canonical sources, structured warnings,
lifecycle/missing counterparts and an allowlisted no-JavaScript-friendly chooser.

Helps readers compare applicable instructions without merging incompatible procedures or assuming an
absent warning means safety.

## Read the documentation

| Edition                                                      | Audience and contents                                                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------ |
| [project-guide.docx](reports/project-guide.docx)             | User and developer guide: purpose, current usage, design, boundaries and source references.                        |
| [validation-review.docx](reports/validation-review.docx)     | Reviewer edition: exact tested baseline, observed workflows, dated local results and remaining limits.             |
| [validation-evidence.xlsx](reports/validation-evidence.xlsx) | Two filterable Excel Tables for observed workflows and test-source inventory, with recalculating outcome formulas. |

The editable Markdown remains the maintenance source. The Word files are readable editions. The
workbook is an evidence index rather than a test runner. See
[publication identities and review](reports/publications.json) and the
[documentation refresh record](reports/documentation-refresh-2026-11-09.md).

## Current usage and help

[README quick start](../README.md) is the entry point. Use the project-specific guides below before
changing inputs, operating modes or deployment assumptions.

### Usage and operations

- [operations](operations.md)

### Design and contracts

- [adr/0001 static first portal](adr/0001-static-first-portal.md)
- [adr/0002 deterministic lexical search](adr/0002-deterministic-lexical-search.md)
- [adr/0003 public restricted boundary](adr/0003-public-restricted-boundary.md)
- [architecture](architecture.md)
- [content model](content-model.md)
- [security model](security-model.md)

### Security and validation

- [testing and validation](testing-and-validation.md)

## Historical results and reproduction

The reviewed source is
[`b3f1942c3b18c7283068192caec764c5bb386a32`](https://github.com/JasonStys/versioned-product-knowledge-portal/tree/b3f1942c3b18c7283068192caec764c5bb386a32).
The observed functional workflow baseline is `b3f1942c3b18c7283068192caec764c5bb386a32`; those
observations are recorded at `2026-11-10T06:15:22.133948+00:00`. They do not certify an unrun later
revision.

- [Detailed recorded validation](reports/comparison-2026-11-09.md)
- [Current Actions](https://github.com/JasonStys/versioned-product-knowledge-portal/actions) records
  later integration checks separately.
- Preserve dated measurements and follow the existing testing guide to reproduce them; a test-source
  inventory alone does not establish execution.

## Practical boundaries

- Public synthetic static corpus; no private accounts, content scraping or real-equipment guidance.
- Edition comparison matches editorial identities, not semantic equivalence; missing text or
  warnings do not prove feature/hazard removal.
- Extractive search/citation limits and abstention remain; automated checks do not establish
  exhaustive accessibility conformance.

## Maintaining these editions

Update the editable usage/design/test documents first. Rebuild and visually review every Word page
and workbook tab before replacing an edition; verify the exact binary digests and evidence source in
publications.json. Keep account data, logs with secrets, installed-app state and private test stores
out of documentation. Source and release assets retain their existing security and licensing
boundaries.
