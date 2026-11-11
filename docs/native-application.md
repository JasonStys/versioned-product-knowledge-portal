# Native catalog workspace

The native Windows application uses the original search, source projection, structured comparison
and synthetic corpus. Its new catalog editor is an actual authoring workflow: product definitions,
edition dates/lifecycle, topic sections, ordered steps, literal code, complete warnings and
provenance are validated as one catalog. The public static reader remains a separate build-time
publication.

## Working with a catalog

The first workspace contains the original 12 synthetic topics. These are editable inputs within the
full application. Clone Apex 2.0 into 2.1 to practice a release review, then change the copied
warning and compare both versions. For a new use case, add a product, add its first edition, then
select **New topic**. The structured editor provides every original field; add/remove sections,
paragraphs, steps, optional code and warnings using ordinary JSON arrays/objects. Keep stable IDs
while editing.

Title and summary controls take precedence over their corresponding JSON fields. Applying a form
validates all affected records. Changing a product name synchronizes its topics. Promoting a current
edition maintains the old current edition; retirement requires an end-of-support date and preserves
content. Removing a topic affects the draft only. Moving a topic to another stable identity requires
an explicit new topic rather than silently renaming an existing record.

Native imports use an owner-selected file dialog and the exact `schemaVersion: 1`, `products`,
`topics` JSON shape of a saved catalog export. Unknown or duplicate keys, invalid real dates,
inconsistent product/version/lifecycle, incomplete warnings, duplicate IDs/routes and excessive
input are refused. Imports replace the draft only. Saving requires the base revision still to be
current; an old queued save cannot overwrite a newer one. Before switching contexts, resolve or
explicitly discard unapplied editor fields. Exported JSON/HTML always uses the last saved catalog.

## Storage, limits and recovery

The owner-local folder contains `owner.json`, one live `owner.lock`, `current.json`, `revisions/`
and `browser-state/`. Existing fixed files and the bounded browser tree must be ordinary local,
single-link files/directories before Chromium opens them. Ancestor aliases, UNC/device/ADS paths,
program-directory profiles and unknown entries are refused. These are static accidental-alias
checks, not protection against a malicious concurrent operating-system owner.

Each completed revision has an exact SHA256 filename and bound catalog hash, workspace identity,
monotonic sequence, parent revision, timestamp and fixed reason. The complete immutable record is
written and flushed before a new temporary pointer is flushed and renamed over `current.json`. Only
the pointer replacement is atomic. This does not promise a filesystem transaction across all files,
power-loss durability, authentication or an atomic relationship with exported documents. Normal
stopped-app restart and restore are exercised by the real native consumer.

- Catalog JSON is at most 2 MiB; at most 16 products, 12 editions per product and 256 topics.
- The original complete comparison chooser retains its 1,000-route budget. A catalog that cannot be
  used within that budget is refused before import/save, not accepted and then broken on render.
- Topic fields, identifiers, synonyms, sections, paragraphs, code and warning text have separate
  bounds. JSON nesting is at most 16 and duplicate escaped-equivalent keys are refused.
- At most 50 revisions and 110 MiB of revision bytes are retained. Nothing is silently pruned.
  Export the saved catalog, preserve a complete stopped-workspace backup and start a separate
  workspace when the history is full. Exported catalogs do not contain the old revision history.
- JSON imports are at most 2 MiB and HTML exports at most 8 MiB. Exports create a new file only;
  choose a new destination instead of replacing a prior report.
- Chromium state has fixed file/depth/byte admission budgets. The owner accepts at most four
  outstanding native operations and closes only after accepted work settles.

If initialization or a pointer replacement is interrupted, keep the complete folder. A completed
unreferenced revision is not silently activated. An unfamiliar temporary pointer, corrupt record,
stale lock or unsupported browser file causes refusal and is preserved for owner review. Do not
delete a sidecar, lock or revision to force startup. Restore a verified stopped-folder backup or
export from a still-open healthy workspace into a separate new workspace; seek help through the
repository with synthetic reproductions, never passwords or private catalog contents.

## Native boundary

One sandboxed, context-isolated renderer uses a fixed `portal://workbench` origin. Only exact hashed
bundled assets are served; profile files and arbitrary filesystem APIs are not routed. The sole main
frame can invoke a closed set of workspace operations. Main-process file dialogs choose paths;
renderer requests cannot supply one. Other origins, navigation, popup windows, downloads and
permissions are denied. Catalog text is rendered with `textContent`; saved HTML escapes all fields
and has a restrictive CSP. Native navigation stays on the current catalog rather than an unrelated
static starter page.

Quit retains the window/owner through actual accepted dialogs and file work. This does not prevent
forced OS termination, machine shutdown, filesystem failure, same-user malware or administrator
access. There is no developer account or remote collection service. The package is unsigned.

## Reproduce the native acceptance

Install the exact source and desktop locks, then run the source gates and build command in the
README. Verify the archive sidecar, extract the complete ZIP into a fresh separate directory, and
run the consumer against its actual executable:

```powershell
node desktop/tests/native-acceptance.mjs .runtime/acceptance-020 .runtime/extracted-020/KnowledgePortal.exe
```

Only a fresh own-project `.runtime` evidence folder is accepted. The consumer redirects home,
AppData and temporary directories into that synthetic folder and does not inherit provider keys. It
drives the same visible controls twice, actual catalog/store/export operations, original engines,
held dialog/Quit, narrow reflow and accessibility. Dialog selections are supplied by the harness;
catalog engines, filesystem operations and the real compiled app are not replaced by API mocks. The
mandatory native workflow extracts its built ZIP before using it and retains only small synthetic
receipts/screenshots, not the whole package, caches or profile.

The full Electron and Chromium/Node notices remain beside the executable. Project and actual bundled
Astro client terms are available in the application's runtime notice panel. Package hashes bind
measured bytes and source metadata, not publisher signatures or clean-machine certification.

Primary design references:
[Electron security](https://www.electronjs.org/docs/latest/tutorial/security),
[custom protocol](https://www.electronjs.org/docs/latest/api/protocol) and
[application lifecycle](https://www.electronjs.org/docs/latest/api/app).
