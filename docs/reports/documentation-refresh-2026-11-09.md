# Documentation refresh — 2026-11-09

By Jason Stys.

This documentation-only edition describes source `b3f1942c3b18c7283068192caec764c5bb386a32`. It does not change application behavior, accounts, private data, installers or published releases.

## Published editions and completed review

| File | Bytes | SHA-256 | Reviewed scope |
| --- | ---: | --- | --- |
| [project-guide.docx](project-guide.docx) | 44044 | `7d13cf219335b0436002eea6f1b19c1a419abcc935aff21fbff1d82265f8424e` | 5 pages, each viewed individually |
| [validation-review.docx](validation-review.docx) | 42452 | `a11f10fbb40bba93f2decb5dfde2e1aa0a892ffcfe16edb6ba454b08530381bd` | 3 pages, each viewed individually |
| [validation-evidence.xlsx](validation-evidence.xlsx) | 7316 | `1cd240266b7a15d48b36045c3c7c536a16d8c5345a6efe64755b62745280a286` | Both tab previews; two actual Excel Tables/autoFilters; four formulas; failure-change/restore recalculation and zero formula errors |

Word review checked plain black titles, readable pagination, whole table rows, source references, practical limits and absence of clipping or overflow. Render receipts were matched to the current DOCX digest before approval. Workbook review inspected both tab previews and actual exported Table/autoFilter elements; recalculated success/failure summaries were compared independently with workflow metadata. Static previews do not draw Excel dropdown arrows; the exported workbook contains the actual filters.

## Evidence and change boundary

- Functional baseline: `b3f1942c3b18c7283068192caec764c5bb386a32`.
- Workflow observation: `2026-11-10T06:15:22.133948+00:00`; exact run URLs and source identities remain in [publications.json](publications.json).
- Local document-package validation verifies exact copied bytes, Office ZIP integrity, approved page/tab identities and internal documentation links. Repository-specific documentation and source-policy commands are run separately and recorded in the integration handoff.
- Source/index metadata is regenerated using the repository’s existing tools. Existing privacy, security, coverage and workflow gates are retained.
- PR and later main workflows must pass independently. This record does not claim future or unrun integration CI success.

## Interpretation

The Word files document the cited source; dated source reports retain their original execution scope. A passing workflow is distinct from completed analysis with zero findings, and neither establishes production suitability. The Excel source inventory is not a per-test execution report. Checksums identify exact bytes, not a signature or publisher attestation.

Use the [handbook](../handbook.md) to choose usage, design, security and test documentation. Keep editable Markdown and reviewed editions together; do not replace historical measurements with undated claims.

## Integration-local checks

Observed at `2026-11-10T08:05:10.386746+00:00` on Windows with this repository’s existing development tools. Python commands use its isolated development environment. The documentation source baseline remains the immutable revision above; these checks validate this documentation integration locally.

| Command | Observed result |
| --- | --- |
| `pnpm validate` | Passed, exit 0. |

The independent publication audit also matched every copied Office file to its approved SHA-256, checked ZIP package integrity and current page/tab approvals, compared immutable workflow/source metadata, and resolved every local handbook/report link within the repository. Hosted PR/main, browser, platform and container jobs remain separate required checks; they are not inferred from these local results.



The unchanged full pnpm validate gate passed formatting, exact source indexes, typed lint, Astro checking, all coverage-gated unit/policy tests, production build, static link/budget validation and the independent 50-judgment search evaluation. Browser/accessibility and CodeQL analyses remain separate required hosted observations.
