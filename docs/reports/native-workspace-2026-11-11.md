# Native catalog workspace validation — 11 November 2026

Author: Jason Stys. Scope: the actual product-knowledge application, not a separate example viewer.
These are observed local source/candidate results. A later pull request, exact-main analysis,
published archive, installation and any illustrated guide require their own observed evidence.

## What changed and why

The original portal publishes validated synthetic product topics with version-aware retrieval and
complete source comparisons. It lacked a durable end-user authoring application. Version 0.2.0 adds
real product/topic/edition controls, structured editing, exact draft previews, original search and
extractive abstention, original warning/section comparison, explicit catalog import, immutable
revision history/restore and saved JSON/inert HTML export.

The portable application includes the complete interface and runtime. A first launch creates a
separate owner-local workspace; it does not require Node, a repository checkout or default login.
The browser preview explicitly lacks native durability. The original static reader, no-JavaScript
comparison pages, 12-topic corpus, judged search set and all original quality floors remain.

Catalog validation is closed and bounded. Edits preserve stable IDs and applicability, promotion
maintains the former current edition, retirement preserves content, and incomplete warnings or
duplicate identities are refused. A valid catalog must also fit the unchanged original complete
comparison chooser's 1,000-route budget. Import is draft-only until an explicit saved revision.

Immutable records bind workspace, parent, sequence, complete catalog and content hash. Compare-and-
swap saves prevent a stale queued edit from overwriting a newer revision. The completed record is
flushed before an atomic current-pointer replacement; this is not an all-files/power-loss transaction.
Restore creates a new revision. Unknown/corrupt/incomplete state is preserved, not silently reset.

## Observed local validation

| Gate | Observed result |
| --- | --- |
| Original and new unit cases | 183 passed, including real file transactions, native origin/resource controls and actual-workflow negative mutations. |
| Original library coverage scope | 348/350 lines (99.42%), 329/335 branches (98.20%), 90/91 functions (98.90%). No new exclusion or lower floor. Native CJS/UI are additionally exercised by dedicated real file/native journeys; these percentages do not describe the entire packaged binary. |
| Strict Astro/TypeScript and lint | No type errors/warnings/hints; existing type-aware source rules retained. The new Electron CommonJS files use their actual module format with syntax/recommended checks and generated indexes. |
| Original plus new browser journeys | All 36 desktop/mobile Chromium cases passed. Original keyboard, no-JavaScript comparison, applicability/warning, query, reflow and accessibility oracles remain. Four added executions cover real browser authoring/retrieval and explicit temporary scope/reflow. |
| Static build, links and original asset budgets | All 69 pages passed link validation. JavaScript was 30,392 bytes of the unchanged 102,400-byte budget; CSS was 10,234 of 40,960 bytes. |
| Original judged retrieval | All 50 judgments passed; Recall@5 was 100% (96% floor), MRR 0.985 (0.90 floor). These measure only the original synthetic corpus. |
| Actual ZIP-extracted Windows application | All 13 user-workflow checks passed in two visible launches of the actual relocated EXE, with normal process exits `[0, 0]`. All 165 portable payload files were byte-identical before/after. |
| Actual native accessibility | The same native document passed the pinned axe-core WCAG A/AA rule tags with zero violations/incomplete checks; 25 checks passed. Native navigation and long hashes remained within 320/390 viewports. Automated checks do not establish full conformance. |
| Dependency review | Full source and full isolated desktop npm graphs had zero reported advisories at observation. No ignore or security-gate removal. |

The native consumer uses a fresh named synthetic profile and redirects home/AppData/temp into it.
Provider keys are not inherited. It supplies explicit dialog choices but does not replace the core,
filesystem operations or application endpoints. Its actual scenarios include:

1. Original E-104 search scoped to the exact edition, plus genuine extractive abstention.
2. Clone/promote Apex 2.0 to 2.1, edit a complete warning, and compare both original sources.
3. Render markup literally, export exact saved JSON and escaped inactive HTML, refuse overwrite.
4. Refuse duplicate-key imports without changing saved state; import a custom product/topic into
   the draft and explicitly save it.
5. Restore an earlier catalog as a new revision, preserve later records, close and reopen exactly.
6. Author a new product/edition/topic through actual controls, refuse an unapplied form save and
   cancel dirty Exit without losing editor fields.
7. Hold an actual accepted export choice, request Exit repeatedly, observe the same visible window
   and live owner lock, then complete that choice and observe normal exit and exact saved export.

Additional file tests refuse actual NTFS hardlinks in fixed files/browser sidecars, directories in
fixed slots, malformed UTF-8, stale/unknown revisions and oversized directories before byte reads.
Ordinary existing browser recovery files remain intact. A failed pointer replacement preserves the
old pointer, new complete record and temporary evidence rather than adopting an uncertain state.
Fifty real flushed revisions exercise the retention boundary without deleting earlier history.

## Issues actually found during validation

- The first accessibility wrapper attempted an auxiliary `Target.createTarget` unsupported by
  Electron. Its failure was retained, not reclassified as an accessibility pass. The test transport
  now executes the exact pinned axe-core on the same actual native document; the product CSP, rule
  tags and zero-violation requirement are unchanged. Original browser axe checks remain unchanged.
- Moving final lock release after window closure exposed a genuine quit-lifecycle fault: the
  window closed and `will-quit` was prevented, but an immediate promise-microtask reentrant quit
  left the process alive. An independent same-binary lifecycle probe observed those actual events;
  a later normal quit exited zero. The final authorized quit is now deferred one event-loop turn,
  after the real release. The unchanged full consumer then proved two normal zero exits. No forced
  termination, close-deadline extension or cleanup-as-pass was used.
- A complete directory allocation was removed from selected workspace/history admission. Bounded
  directory iteration stops at the real limit; preservation/no-later-read negatives exercise it.
- The original development graph contained fast-uri 3.1.8 and minimatch 10.2.6 advisories. Exact
  patched leaf overrides use fast-uri 3.1.9 and minimatch 11.0.1 in pnpm's supported workspace
  settings. Full source gates and full-graph audit are retained. Runtime Astro is unchanged.

Early local candidate/tooling failures are preserved separately from successful receipts. Working-
tree candidate measurements are explicitly labeled; they do not establish a clean published build.

## Reproduction and limits

Run `pnpm validate`, the original `pnpm test:e2e`, both full dependency audits, the exact-source
portable builder and the ZIP-extracted consumer described in [native operation](../native-application.md).
The new mandatory Windows workflow runs those native controls on its actual built/extracted package,
with read-only contents permission and only small three-day synthetic evidence uploads. It does not
publish a release or install an application. Hosted jobs and processed/raw CodeQL must be checked
for the exact resulting source; this local report does not predeclare their outcome.

The observed candidate used Electron 44.11.1 and embedded Node 24.22.2, with its original runtime
terms plus project and actual Astro client terms retained. The package is unsigned and this is not
clean-machine, publisher-signing, multiuser-hosting or legal certification. Catalogs are plaintext
for one trusted OS owner. Supplied source references are assertions; record/package hashes provide
integrity rather than authentication. Static alias checks do not defeat concurrent same-owner
malware, administrator access, machine failure or forced OS shutdown. No provider, cloud account,
device, normal private profile, Docker setting or installed application was used or modified.

Primary sources: [Electron security](https://www.electronjs.org/docs/latest/tutorial/security),
[protocol](https://www.electronjs.org/docs/latest/api/protocol),
[application lifecycle](https://www.electronjs.org/docs/latest/api/app),
[axe-core API](https://github.com/dequelabs/axe-core/blob/develop/doc/API.md),
[fast-uri scheme advisory](https://github.com/advisories/GHSA-w74x-v6f9-j3xg),
[fast-uri host advisory](https://github.com/advisories/GHSA-wjr9-j795-jxcr),
[minimatch advisory](https://github.com/advisories/GHSA-g3hv-75wg-m249) and
[pnpm workspace settings](https://pnpm.io/settings).
