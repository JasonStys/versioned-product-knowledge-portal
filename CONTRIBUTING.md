# Contributing

## Development environment

Use a supported Node.js release from `package.json` and pnpm 11. Install exactly the committed
lockfile:

```bash
pnpm install --frozen-lockfile
```

## Change workflow

1. Create a focused branch and describe the user or maintenance outcome.
2. Add or update a schema-valid topic, implementation, and the smallest useful tests.
3. Run `pnpm update:headers` after code symbols move.
4. Run `pnpm validate`; run `pnpm test:e2e` for markup, style, component, or browser changes.
5. Review generated relevance/link evidence and commit intentional documentation changes.
6. Request review with assumptions, risks, screenshots when visual behavior changed, and rollback
   notes.

## Content rules

- Use invented products and openly redistributable material only.
- Keep product and version explicit. Never silently copy a current-version instruction into an older
  route.
- Safety notices require condition, consequence, and avoidance fields.
- Identifiers must be stable uppercase values; slugs and topic IDs must remain stable after
  publication.
- Preserve provenance when importing an upstream canonical topic.

## Code rules

- Keep TypeScript in strictest mode and prefer immutable, explicit contracts.
- Give exported functions JSDoc that explains behavior, inputs, output, and failure where
  applicable.
- Use DOM `textContent` or framework escaping for corpus text; do not add `innerHTML` sinks.
- Bound input, result counts, retries, queues, and assets. Document complexity for retrieval
  changes.
- Do not weaken a test threshold to make an unexplained regression pass.

## Commit and release convention

Use imperative commits such as `Add version-scoped diagnostic search`. User-visible changes go in
`CHANGELOG.md`. Releases follow semantic versioning; generated static output is rebuilt from the
tag.
