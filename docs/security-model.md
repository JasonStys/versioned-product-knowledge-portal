# Security model

## Assets and trust boundaries

Assets are documentation integrity, product/version applicability, stable routes, provenance, search
results, and build/release evidence. Authored JSON, query text, dependency packages, CI actions, and
hosting headers cross trust boundaries. The published site contains no credentials, private content,
or device endpoints.

## Threats and controls

| Threat                               | Control                                                                                                          | Residual risk                                                    |
| ------------------------------------ | ---------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| Active content in imported topics    | Schema accepts strings; templates escape; search client uses `textContent`; no raw corpus HTML.                  | Future rich-text imports need a reviewed allowlist sanitizer.    |
| Wrong-version instruction            | Version-qualified routes, persistent labels, pre-score filters, judgment traps for reused codes.                 | A reader can still manually select the wrong installed version.  |
| Open redirect                        | Only reviewed root-relative mappings; unknown paths return undefined; manifest synchronization test.             | Host configuration must faithfully apply the manifest.           |
| Dependency or action compromise      | Exact lockfile, release-age policy, production audit, grouped updates, full action SHAs, read-only token.        | Registry and transitive-package compromise cannot be eliminated. |
| Denial through large queries/results | 160 characters, 12 base tokens, 20-result maximum, bounded synonym expansion, static corpus.                     | A future remote index requires independent quotas and timeouts.  |
| Misleading generated answer          | Extractive summary only, citations, version filter, threshold, explicit abstention, no action tools.             | Relevant source material can still be incomplete or wrong.       |
| Private-content disclosure           | This build contains public synthetic content only. ADR requires a separate authorized index for restricted data. | Adding authentication only in the UI would be insecure.          |

## Code scanning

`.github/workflows/codeql.yml` explicitly scans `javascript-typescript` and `actions` in separate,
bounded Ubuntu jobs. Both use no-build extraction and GitHub's `security-extended` query suite. The
workflow covers main pushes, pull requests targeting main, weekly scheduled analysis, and manual
requests; there are no source-path filters, query suppressions, or ignored findings. JavaScript,
TypeScript and workflow YAML are supported; `.astro` templates and CSS are not claimed as direct
CodeQL coverage. Real rendered-page, injection, link and accessibility regressions remain part of
the existing validation suite.

The workflow default stays `contents: read`. Only each analysis job receives
`security-events: write` for its code-scanning result upload. Checkout does not persist credentials.
The full commit pins are reviewed, no repository build/install commands run with that upload
permission, and no deployment secrets or `pull_request_target` trigger are introduced. Dependency
and extractor caches and CodeQL database uploads are disabled; processed SARIF findings remain
available in GitHub's Security view without creating extra run artifacts.

A successful analysis means extraction, query execution and result processing completed; it does not
itself mean zero alerts. Review each language/category, exact event revision and any extraction
warnings. Inspect new and existing open alerts, trace the real input-to-sink path, fix a confirmed
issue with a regression test, and rerun both CodeQL and normal validation. Unsupported syntax,
framework modeling gaps and false negatives remain possible. The dependency audit covers a different
supply-chain boundary. See [the setup and validation record](reports/codeql-2026-11-09.md).

## Secrets

The build requires no secrets. `.env*` files are ignored except the example convention, commands use
placeholder credentials, and logs must redact authorization headers. If deployment credentials are
introduced, prefer short-lived workload identity and keep deployment permissions in a separate
workflow.

## Response

Follow [SECURITY.md](../SECURITY.md). Preserve evidence, remove public exposure only when necessary,
rotate any affected credential, patch the smallest boundary, add a regression test, and publish
impact and supported versions.
