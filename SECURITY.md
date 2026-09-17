# Security policy

## Supported versions

Until the first stable release, only the latest commit on `main` receives security fixes.

## Reporting a vulnerability

Do not open a public issue for a suspected vulnerability or exposed secret. Use GitHub's private
security-advisory workflow for this repository. Include affected paths, reproduction steps, impact,
and any suggested mitigation. Avoid including real credentials or customer data.

## Repository boundaries

This project publishes synthetic public content as static files. It does not implement
authentication, authorization, device control, or private search. A deployment that adds restricted
content must use server-side policy enforcement and a separately authorized index; hiding UI
elements is not access control.

See [docs/security-model.md](docs/security-model.md) for threats, controls, and residual risks.
