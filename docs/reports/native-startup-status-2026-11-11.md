# Fatal startup status correction — 2026-11-11

## Problem and retained purpose

The full versioned knowledge authoring/search/comparison application remains unchanged. This
correction addresses how its native owner reports a fatal startup. Actual Electron 44.11.1
measurements of main `e4b3cd025246881bc8cc7ea3f0dc5a96e75c20a9` showed that setting
`process.exitCode = 1` followed by `app.quit()` still returned process status 0. A supervising tool
could therefore mistake resource refusal or failed readiness for successful completion.

The native 0.2.0 source was not yet publicly released when this was found. No published package,
source revision, user workspace or earlier evidence is overwritten by this correction.

## Minimal runtime change

Only the two fatal-startup paths use the new finalizer. Its actual closing promise stops new
admission in the same turn, waits for every already accepted operation, waits for workspace-close
settlement, preserves any changed ownership token, and finally calls `app.exit(1)`. It does not
force a live operation to look complete. The normal `closeOwned`, `will-quit`, pending-dialog
retention and `app.quit()` path are unchanged.

Electron's [explicit exit API](https://www.electronjs.org/docs/latest/api/app#appexitexitcode)
bypasses normal quit events, which is why accepted work and workspace closing must finish before it
is used here. Normal user Quit continues through those existing events. The
[error dialog API](https://www.electronjs.org/docs/latest/api/dialog#dialogshowerrorboxtitle-content)
is replaced only in the regression, avoiding a modal human acknowledgement during automated tests.

## Actual failure and control measurements

The regression executes the real source main in separate actual Electron processes. It builds a
small self-consistent, inert UI fixture around hash-verified original catalogue/search/comparison
code and the production resource readers, protocol, preload and workspace. The UI invokes the real
IPC. It is a startup-status fixture, not a substitute demonstration app or published payload.

| Case                                                    | Actual original main                  | Actual corrected main, first local run                   |
| ------------------------------------------------------- | ------------------------------------- | -------------------------------------------------------- |
| Invalid resources, before workspace acquisition         | Exit 0, real admission error observed | Exit 1; saved baseline untouched                         |
| Existing foreign owner token                            | Exit 0, real admission error observed | Exit 1; token and saved baseline untouched               |
| Real accepted save followed by rejected readiness       | Exit 0; accepted revision persisted   | Exit 1; original revision and new accepted save retained |
| No readiness signal, actual unchanged 30-second timeout | Exit 0 after 30.407 s                 | Exit 1 after 30.540 s; original revision retained        |
| Real save, accepted readiness and normal Quit control   | Exit 0 with new saved revision        | Exit 0 with new saved revision                           |

All five first corrected cases passed without replacing `app.exit`, `app.quit`, filesystem calls,
workspace methods, IPC or renderer readiness. The error-dialog display is the only stubbed method.
The test entry uses the real Electron `app.setPath` API to isolate initial Chromium storage before
workspace admission. Valid main then selects the real workspace browser directory normally.

Earlier harness-only failures are retained separately: a Git safe-directory path-format error
stopped before execution; early cases without explicit initial Chromium storage isolation produced a
breakpoint exit without the required error callback. Those crashes were rejected, not accepted as
expected failures. Shorter environment paths alone did not resolve them; no unverified crash cause
is asserted. Properly isolated measurements produced the complete original `0/0/0/0/0` vector.

## Required validation and limits

The full original source, coverage, type, static-build, search, browser, dependency-audit and
compiled fourteen-case native gates remain required. The Windows native workflow adds these five
actual source-main processes after building the package, with the unchanged 30-second readiness
timer and a 45-second per-process observation bound. It retains only the small synthetic receipt,
not the workspace or binary. The workflow-policy tests reject omitting this regression or widening
artifact scope.

Use the package's original engines and same-owner plaintext workspace assumptions. This status
correction does not add authentication, encryption, a multiuser service, source signatures, a
clean-machine installation claim, or protection from forced OS termination. Full compiled-user
acceptance is distinct from these synthetic startup failures. Later exact-source hosted/main checks
and independent download/install acceptance remain separate requirements; local results are not
relabelled as those unrun stages.
