# Edition comparison

The comparison workflow is for support engineers checking a diagnostic, documentation owners
reviewing changes, and readers deciding which edition applies to their installed product. It
compares authored evidence rather than proposing a merged or automatically updated procedure.

## Use it

Open **Compare**. Select a product, two distinct versions and a stable topic identity, then choose
**Compare editions**. Product changes rebuild the allowed version/topic options, so an Apex version
cannot accidentally be applied to a Northstar topic. Each topic also offers **Compare with ...**
links. The generated URL includes product/from/to/topic, can be shared, and supports **Reverse
comparison**. Direct fallback links appear when JavaScript is unavailable; comparison content is
always complete static HTML.

The top of a comparison calls out changed title/summary, identifier set and section order. The
section summary records added, absent, changed or unchanged content. Sections compare exact title,
paragraph order, step order, code, and all warning fields. Each source column then renders its
original text, complete condition/consequence/avoidance notices, version/lifecycle, update date and
source ID/page/checksum with a canonical source link. Section anchors use distinct from/to prefixes.

## Practical demonstrations

1. **Support diagnostic review:** Apex 1.5 → 2.0, `error-e-104`. The old summary describes a
   duplicate Ethernet address; the new summary describes certificate validity. Both definitions and
   different notices remain visible. Do not carry the 1.5 procedure into 2.0 just because the code
   matches.
2. **Documentation warning review:** Northstar 3.2 → 3.0, `analog-input-calibration`. The 3.2
   warning about injected current is absent in 3.0. The review prominently says this is a
   documentation absence, not evidence the underlying risk was resolved. The complete newer warning
   is retained on the left; reversing the comparison labels that same notice as added on the right.
3. **Retired documentation lookup:** Apex 2.0 → 1.0, `error-e-104`. Version 1.0 is explicitly
   retired and has no matching topic. The right column has no invented source, warning or procedure.
   It does not substitute a 2.0 explanation into the retired edition. The available side stays
   cited.
4. **New-topic review:** Apex 1.5 → 2.0, `quickstart`. The source edition is explicitly missing
   while the target's complete content is available. Unrelated topic slugs or a matching identifier
   on another product cannot be selected as substitutes.

All sample documents are fictional, pre-existing corpus records. Nothing here operates equipment.

## Matching and bounds

Matching uses product ID + topic slug + exact version, and section IDs within that topic. This is an
editorial identity convention, not a semantic equivalence judgment or a line-based source-code diff.
A renamed section appears as absent/added. Whitespace changes in authored strings count as changes.
Identifier order alone does not change the identifier set; section and step order remain visible.
Differences may reflect edition-specific scope, not a required migration action.

The pure comparison model rejects unknown/same versions, neither-edition topics, ambiguous topic or
section identities, and topic metadata that contradicts the public product/lifecycle catalog. The
validated Astro collection remains the public-content boundary. The model accepts at most 1,000
corpus topics and 128 sections per edition; route generation fails above 1,000 comparison pages. The
chooser accepts only those generated routes and rejects injected/external destinations. This corpus
emits 44 comparison pages plus the chooser, within the original JS/CSS asset budgets.

A single comparison scans N corpus topics and maps up to S sections, O(N + S + B) time for B source
text bytes examined and O(S) comparison rows; sorting identifiers adds O(I log I). Static route
enumeration scans the corpus for each known version pair. Full source text is intentionally kept
separate, so generated HTML size scales with the two source editions. Large enterprise estates would
need paginated build/index design and reviewed stable identities, not an unbounded all-pairs UI. No
live corpus scraping, account authentication, private-document indexing, AI generation or search
relevance behavior is introduced.

See [validation evidence](reports/comparison-2026-11-09.md) and the generated symbol headers for
actual source locations.
