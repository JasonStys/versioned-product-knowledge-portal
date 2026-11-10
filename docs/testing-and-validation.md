# Testing and validation

## Strategy

The suite follows a pyramid: pure unit tests cover ranking and contracts; build/integration checks
cover content, routes, links, budgets, and repository policy; a smaller browser suite covers real
interaction, keyboard behavior, responsive reflow, and automated accessibility rules.

| Area                                           | Test type              | Evidence and target                                                        |
| ---------------------------------------------- | ---------------------- | -------------------------------------------------------------------------- |
| Tokenization, ranking, boosts, filters, limits | Unit                   | Exact outputs and edge cases; enforced branch coverage.                    |
| Citation and abstention                        | Unit + browser         | Version-correct citations; unrelated questions abstain.                    |
| Content schema and warnings                    | Astro build + policy   | Invalid fields or incomplete warnings block publication.                   |
| URLs and redirects                             | Unit + generated crawl | Unique routes, local redirects, no broken internal targets.                |
| Search relevance                               | Offline evaluation     | 50 judgments; Recall@5 ≥ 96%; MRR ≥ 0.90.                                  |
| Accessibility                                  | Browser + manual plan  | Keyboard skip, reflow, labels, warning structure, axe A/AA scan.           |
| Performance                                    | Static budget          | Total browser JS ≤ 100 KiB; CSS ≤ 40 KiB.                                  |
| Supply chain                                   | CI policy + audit      | Locked packages, release-age policy, SHA-pinned actions, production audit. |

## Commands

```bash
pnpm format:check
pnpm types:sync
pnpm lint
pnpm typecheck
pnpm test:coverage
pnpm build
pnpm validate:links
pnpm evaluate:search
pnpm test:e2e
pnpm audit --prod --audit-level high
```

## Recorded baseline

Reference run on September 16, 2026 with Node.js 24 and pnpm 11.19.0:

- 21 unit/repository-policy tests passed.
- 12 Playwright cases passed across desktop and mobile Chromium (six scenarios per project).
- V8 coverage: 98.18% statements, 86.95% branches, 95.23% functions, and 98.16% lines.
- Astro diagnostics: 34 files, zero errors, warnings, or hints.
- Production build: 23 static pages; the reference run completed in 1.30 seconds.
- Generated-site validation: 23 HTML files, zero broken internal targets, 5,340 bytes of JavaScript,
  and 7,104 bytes of CSS.
- Search evaluation: 50 judgments, 100% Recall@5, 0.985 mean reciprocal rank, and zero failed
  judgments.
- Production dependency audit: no known vulnerabilities.
- Visual inspection completed for the home page, populated search results, and a warning-bearing
  topic page. A manual screen-reader, forced-color, and 400% zoom audit remains a release task.

Machine-readable results are written to `reports/` and uploaded by CI. GitHub Actions repeats the
non-browser suite on Node.js 22 and 24 before running the browser job.

## Security analysis

The independent CodeQL workflow runs the `javascript-typescript` and `actions` extractors with
`build-mode: none` and `security-extended` on main pushes, main-targeting PRs, weekly schedules, and
manual requests. Unit repository-policy checks cover immutable action references and the restricted
upload authority. Normal Node 22/24, coverage, static build, search and Chromium gates remain
required. The [scan record](reports/codeql-2026-11-09.md) distinguishes local checks from hosted
extraction/query/upload evidence. CodeQL does not directly establish `.astro` template, PDF/content,
accessibility or runtime safety; an empty alert list is not a security certificate.

## Gaps

Manual screen-reader and forced-color checks are release tasks, not automated claims. The small
corpus does not exercise stemming in other languages, very large indexes, access-controlled
retrieval, or production analytics.

## Edition comparison regression coverage

The unchanged unit coverage gates now include the pure comparison module. Browser-only chooser
bindings live with UI components and are validated through actual built-page Playwright flows; no
API responses or generated HTML are mocked. Desktop and mobile tests cover E-104 meaning changes,
warning absence without risk inference, reversed comparisons, retired/missing topics, injected
non-allowlisted options, no-JavaScript static behavior, unique anchors, reflow and axe checks.
`PORTAL_TEST_PORT=44361 pnpm test:e2e` selects an owned test-only port; servers are never reused.
See [latest evidence](reports/comparison-2026-11-09.md).
