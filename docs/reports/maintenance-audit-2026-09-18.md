# Maintenance audit — 2026-09-18

## Result

The validated source baseline was `ecfb780`. The hosted [CI run](https://github.com/JasonStys/versioned-product-knowledge-portal/actions/runs/35385671374) passed its Node 22/24, browser, accessibility, search-evaluation, build, link, and production-audit gates.

## Dependency decisions

- The pinned pnpm setup action update was reviewed, validated, and merged.
- Node 26 type declarations were deferred because the supported and tested runtime contract is Node 22–24.
- Dependabot now ignores incompatible Node-type and TypeScript major proposals until the runtime and lint matrices are deliberately upgraded.

No open pull request or non-default maintenance branch remained when this report was prepared. Historical failed runs remain visible but are superseded by the successful default-branch run above.
