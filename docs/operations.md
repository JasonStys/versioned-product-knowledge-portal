# Operations and rollback

## Build

```bash
pnpm install --frozen-lockfile
pnpm validate
pnpm exec playwright install chromium
pnpm test:e2e
```

The deployable artifact is `dist/`. Validation evidence appears under `reports/` and the reviewed
summary under `docs/search-evaluation.md`.

## Configuration

The public build has no runtime environment variables. `astro.config.ts` contains the canonical
placeholder site URL; a real deployment must replace it with the production origin before release.
The host should add a strict Content-Security-Policy, HSTS after HTTPS verification,
`X-Content-Type-Options: nosniff`, and an appropriate referrer policy.

## Health checks

After deployment:

1. Request `/`, `/products/`, `/search/`, and one topic for each lifecycle state.
2. Verify the canonical link uses the production origin.
3. Search an exact identifier and a natural-language task with version filters.
4. Request each legacy path and confirm the configured HTTP redirect target.
5. Check error monitoring for unexpected 404s and asset failures.

## Observability

Static hosting should record aggregate route status, latency, cache outcome, and release identifier
without full query strings or user identifiers. Search analytics are intentionally absent from this
demo; a future design must define consent, minimization, retention, and access before capturing
queries.

## Rollback

Retain the previous immutable `dist/` artifact and its redirect manifest. On a failed smoke test,
atomically switch the release pointer to the prior artifact, reapply its redirects, purge only
affected cache keys, and repeat health checks. Do not mix pages from one release with search assets
from another.

## Troubleshooting

- **Astro schema error:** open the named JSON path and compare it with `docs/content-model.md`.
- **Relevance gate failure:** inspect failed rows in `reports/search-evaluation.json`; adjust
  content or reviewed synonyms, then explain the change—do not simply reduce the threshold.
- **Broken-link gate:** run `pnpm build && pnpm validate:links` and inspect the report source/URL
  pair.
- **Stale symbol indexes:** run `pnpm update:headers`, review the line changes, then rerun
  validation.
- **Browser failure:** open `reports/playwright-html/index.html` and retain the trace from the
  failed test.
