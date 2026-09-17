# ADR 0003: Separate public and restricted search

- Status: Accepted
- Date: 2026-09-16

## Context

A future knowledge estate may contain public, authenticated, and internal material. A static search
bundle is fully downloadable; client-side filters cannot enforce confidentiality.

## Decision

This repository indexes only public synthetic content. Any restricted extension must keep content
and indexes behind server-side authorization, enforce policy again during retrieval, and exclude
unauthorized documents before ranking or answer generation. Public and restricted indexes should be
separate by default.

## Consequences and revisit trigger

The demo needs no identity system and cannot accidentally imply UI hiding is access control. Revisit
only with a documented identity provider, policy model, cache boundary, direct-URL tests, index
isolation, and audit plan.
