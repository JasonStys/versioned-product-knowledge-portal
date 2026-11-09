# Edition comparison validation — 2026-11-09

Environment: Windows, Node v24.18.1, pnpm 11.25.0 (repository pin remains 11.19.0), Astro 7.3.8,
TypeScript 6.0.3, Vitest 5.0.4 and Playwright 1.64.0 Chromium. All data is the existing fictional
12-topic corpus. No external equipment or private user data was used.

| Command | Observed result |
| --- | --- |
| `pnpm install --frozen-lockfile --store-dir .../i/.tooling/pnpm-store` | Passed, including after the minimal patched transitive lock update; integrity/policy checks passed. |
| `pnpm validate` | Final full chained gate passed after the security patch, exit 0. |
| `pnpm format:check` / `pnpm validate:headers` | Formatting and every generated source line index passed. |
| `pnpm lint` / `pnpm typecheck` | Type-aware lint passed; Astro checked 42 files with zero errors, warnings or hints. |
| `pnpm test:coverage` | 56 tests passed; statements 98.90%, branches 94.19%, functions 97.67%, lines 98.81%; original thresholds unchanged. |
| `pnpm build` / `pnpm validate:links` | 68 static HTML pages built, including 44 comparisons and chooser; no broken root-relative links. JS 5,340 B / 102,400 B budget, CSS 8,129 B / 40,960 B budget. |
| `pnpm evaluate:search` | Original 50 judgments passed: Recall@5 100%, MRR 0.985, zero failures. |
| `PORTAL_TEST_PORT=44361 pnpm test:e2e` | 32 actual desktop/mobile Chromium tests passed in 17.7 s against a newly built portal and owned loopback server; no route/API mocks. |
| `pnpm audit --prod --audit-level high` | After patched lock: no known vulnerabilities found. |

The browser checks use real navigation and forms to compare E-104's changed meaning, both source
citations and complete warning fields, product-bound versions, calibration warning absence and
reverse labels, retired/missing topic context, new-topic absence, rejection of an injected
non-allowlisted topic, keyboard submission, JavaScript-disabled links/content, reflow, unique IDs
and automated WCAG A/AA axe checks. They also retain every original search, abstention, skip-link,
warning/provenance and homepage accessibility scenario. They do not establish complete WCAG
conformance or exhaustive browser/device support.

Independent pure-model tests distinguish all warning fields and section content types, preserved
source order, identifier sets, optional content, both missing sides, unrelated products, invalid or
hostile path segments, unknown/same versions, duplicate topic/section identities, catalog metadata
mismatch, 1,000-topic/128-section limits, and the 1,000-comparison-page build cap. Real-corpus tests
verify every emitted comparison request is valid, unique and reversible. Browser UI bindings are
kept with components and exercised in the real browser; they are not claimed as Node unit coverage.

## Dependency issue actually found and fixed

The production audit initially failed on eight advisories (four HIGH, four moderate) in transitive
`undici@8.11.2`, via Astro → Unifont. The lock now uses compatible `8.12.2`, within Unifont's existing
`^8.0.0` range, with registry SHA-512 integrity
`sha512-XtuDWVdqTLr3NAxm2ly9/hU6kUsJOgGh1RASzMBbsw6aWCOaQzHdW+QQDfdERjfJ2V5vL5pRPa4RetO9UfivDg==`.
The patch is verified by the [official security release](https://github.com/nodejs/undici/releases/tag/v8.12.2),
[upstream advisory](https://github.com/nodejs/undici/security/advisories/GHSA-xjj6-f33q-929c) and
[official package metadata](https://registry.npmjs.org/undici/8.12.2). No audit ignore, dependency
major upgrade, coverage exclusion or gate relaxation was added. Runtime requirements now accurately
state Node 22.19+ (or 24), matching the transitive dependency's pre-existing minimum engine.

The final full non-browser suite and all 32 actual-browser tests were rerun after installing this
patch. Hosted Node 22/24, hosted Chromium and any publishing/deployment checks remain the parent's
responsibility; this agent did not push, merge or trigger Actions. The site remains public static
synthetic documentation. Comparison matches editorial identities, not semantic equivalence, and
absence does not establish that a capability or hazard disappeared. Extractive answers and
abstention remain unchanged.
