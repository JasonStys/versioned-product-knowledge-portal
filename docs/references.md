# Engineering references

Primary sources used for design decisions and validation:

- [Astro content collections](https://docs.astro.build/en/guides/content-collections/) — build-time
  loaders, schema validation, and generated content types.
- [TypeScript strict mode](https://www.typescriptlang.org/tsconfig/strict.html) — stronger
  type-checking guarantees.
- [Playwright accessibility testing](https://playwright.dev/docs/accessibility-testing) — axe
  integration and the limits of automated accessibility scans.
- [WCAG 2.2](https://www.w3.org/TR/WCAG22/) — keyboard access, focus, labels, contrast, reflow, and
  target guidance.
- [Vitest coverage](https://vitest.dev/guide/coverage) — V8 coverage and threshold configuration.
- [GitHub Actions security hardening](https://docs.github.com/en/actions/security-for-github-actions/security-guides/security-hardening-for-github-actions)
  — least privilege and immutable action references.
- [OWASP Cross Site Scripting Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)
  — output encoding and safe DOM sinks.
- [RFC 9110](https://www.rfc-editor.org/rfc/rfc9110) — HTTP semantics for redirects and caching.

Dependencies and standards should be rechecked before each release. The repository records the
selected versions in `package.json`, `pnpm-lock.yaml`, and workflow comments.
