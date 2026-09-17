# ADR 0002: Deterministic lexical search before semantic retrieval

- Status: Accepted
- Date: 2026-09-16

## Context

Product documentation contains exact error codes, versions, register names, and part-like
identifiers. Search quality must be measurable and explainable before adding embeddings or generated
answers.

## Decision

Implement a bounded local inverted index with field weights, BM25-style normalization, exact
identifier/title boosts, reviewed synonyms, pre-score filters, stable tie-breaking, and a 50-query
judgment set. Provide a separate extractive answer preview that cites results and abstains below a
threshold.

## Alternatives

- **Pagefind:** excellent static indexing and filters, but a custom scorer makes exact boosts and
  the evaluation contract directly testable in this small demonstration.
- **Hosted BM25 service:** scales and adds analyzers but adds operations, latency, and a network
  dependency.
- **Embeddings/hybrid retrieval:** useful for larger paraphrase-rich corpora, but adds
  model/version/privacy concerns before the lexical baseline is understood.

## Consequences and revisit trigger

Retrieval is transparent and reproducible but lacks sophisticated stemming, typo tolerance, and
large-corpus compression. Revisit when corpus size breaks asset/latency budgets or judged queries
show systematic vocabulary gaps that reviewed synonyms cannot maintain safely.
