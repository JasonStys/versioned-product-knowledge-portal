# File reference

## Root and automation

| File                                   | Purpose                                                                                             |
| -------------------------------------- | --------------------------------------------------------------------------------------------------- |
| `README.md`                            | Outcome, quick start, architecture, feature summary, commands, boundaries, and documentation index. |
| `package.json` / `pnpm-lock.yaml`      | Exact scripts, runtime policy, direct dependencies, and reproducible dependency graph.              |
| `pnpm-workspace.yaml`                  | Explicit `esbuild` install-script allowlist and release-age exceptions recorded by pnpm.            |
| `astro.config.ts`                      | Static output, canonical origin placeholder, directory routes, and origin checking.                 |
| `tsconfig.json`                        | Astro strictest TypeScript plus additional indexing and optional-property checks.                   |
| `eslint.config.mjs`                    | Type-aware strict/stylistic lint configuration.                                                     |
| `vitest.config.ts`                     | Unit-test discovery, V8 reporting, and coverage gates.                                              |
| `playwright.config.ts`                 | Desktop/mobile Chromium projects, preview server, traces, and reports.                              |
| `.prettierrc.json` / `.prettierignore` | Stable TypeScript, Astro, JSON, YAML, CSS, and Markdown formatting.                                 |
| `.npmrc`                               | Exact saves, strict peers, engines, and seven-day dependency release-age policy.                    |
| `.gitignore` / `.gitattributes`        | Generated exclusions, secret-file exclusions, LF normalization, and binary handling.                |
| `.github/workflows/ci.yml`             | Node 22/24 validation, audit, browser checks, and evidence artifacts.                               |
| `.github/dependabot.yml`               | Grouped weekly package and action updates with bounded PR counts.                                   |
| `CONTRIBUTING.md`                      | Development, content, code, test, commit, and review requirements.                                  |
| `SECURITY.md`                          | Supported version, private reporting, and public-content boundary.                                  |
| `CHANGELOG.md`                         | User-visible release history.                                                                       |
| `LICENSE`                              | MIT license for code and synthetic content.                                                         |

## Application

| File or directory                                    | Purpose                                                                              |
| ---------------------------------------------------- | ------------------------------------------------------------------------------------ |
| `src/content.config.ts`                              | Zod contract for identifiers, versions, provenance, sections, and complete warnings. |
| `src/content/topics/*.json`                          | Eleven synthetic, version-qualified documentation topics.                            |
| `src/data/products.ts`                               | Product/version/lifecycle catalog and guarded lookup helpers.                        |
| `src/data/synonyms.ts`                               | Small reviewed, non-recursive query-expansion map.                                   |
| `src/data/search-judgments.json`                     | Fifty reviewed relevance queries, filters, and expected documents.                   |
| `src/lib/contracts.ts`                               | Shared readonly product, topic, index, result, citation, and answer types.           |
| `src/lib/content.ts`                                 | Canonical route, flattened search text, and content/search adapters.                 |
| `src/lib/search.ts`                                  | Tokenizer, weighted inverted index, BM25-style search, filters, and abstention.      |
| `src/lib/search-client.ts`                           | Accessible browser bindings and safe DOM result/citation rendering.                  |
| `src/lib/redirects.ts`                               | Reviewed local legacy mapping and open-redirect guard.                               |
| `src/layouts/BaseLayout.astro`                       | Metadata, canonical URL, skip link, landmarks, primary navigation, and footer.       |
| `src/components/LifecycleBadge.astro`                | Text-and-shape lifecycle label.                                                      |
| `src/components/VersionBanner.astro`                 | Maintained/retired applicability warning.                                            |
| `src/components/WarningNotice.astro`                 | Condition/consequence/avoidance safety structure.                                    |
| `src/components/TopicCard.astro`                     | Versioned topic summary card.                                                        |
| `src/components/SearchPanel.astro`                   | Search/filter controls, live result region, and experimental answer panel.           |
| `src/pages/index.astro`                              | Portal landing page and current-topic entry points.                                  |
| `src/pages/products/index.astro`                     | Product/version catalog.                                                             |
| `src/pages/products/[product]/[version]/index.astro` | Generated version landing pages.                                                     |
| `src/pages/docs/[product]/[version]/[slug].astro`    | Generated semantic topics with warnings and provenance.                              |
| `src/pages/search/index.astro`                       | Search-document assembly and interactive search page.                                |
| `src/pages/about.astro`                              | Scope, evidence, and limitations.                                                    |
| `src/pages/404.astro`                                | No-guessing missing-route guidance.                                                  |
| `src/styles/global.css`                              | Tokens, layout, focus, components, reflow, reduced motion, and print.                |
| `public/robots.txt`                                  | Public crawler policy.                                                               |
| `public/redirects.json`                              | Host-neutral machine-readable legacy redirect manifest.                              |

## Tests and tools

| File                                    | Purpose                                                                                   |
| --------------------------------------- | ----------------------------------------------------------------------------------------- |
| `tests/unit/search.test.ts`             | Tokenization, boosts, filters, synonyms, bounds, citations, abstention, and empty corpus. |
| `tests/unit/content.test.ts`            | Stable routes, flattened searchable content, and public search projection.                |
| `tests/unit/redirects.test.ts`          | Known/unknown redirect behavior and local targets.                                        |
| `tests/unit/repository-quality.test.ts` | Neutrality, headers, docs, action SHAs, warning/route integrity, and manifest sync.       |
| `tests/e2e/portal.spec.ts`              | axe, keyboard bypass, version trap, abstention, warning evidence, and mobile reflow.      |
| `tools/load-topics.ts`                  | Stable offline topic loading and defensive narrowing.                                     |
| `tools/evaluate-search.ts`              | Recall@5/MRR calculation and Markdown/JSON evidence.                                      |
| `tools/validate-links.ts`               | Generated-route crawl plus JavaScript/CSS size budgets.                                   |
| `tools/update-symbol-index.ts`          | Line-accurate top-level symbol indexes for TypeScript, JavaScript, and Astro.             |

## Documentation and generated evidence

`docs/architecture.md`, `content-model.md`, `accessibility.md`, `security-model.md`,
`operations.md`, `testing-and-validation.md`, `search-evaluation.md`, `references.md`, and
`docs/adr/*.md` document design and evidence. `reports/*.json`, `reports/coverage/`, and Playwright
output are generated; CI retains them as artifacts.
