# 2026-10-20 — Privacy and Acknowledgements for optional sign-in

Noto's studentnotes branch `fable/account-sign-in` adds optional Sign in with
Apple and Sign in with Google (device-local profile: display name for the Home
greeting, photo in Settings > Account) and links Google's GoogleSignIn-iOS
10.0.0 SDK into every build. Branch `fable/privacy-sign-in`, from `origin/main`
at `d43574f`. Marc asked for this PR ("Draft the PR now"); Marc merges.

- `privacy.html`: the short version no longer says "no account system" or
  "exactly two places"; a new "Signing in with Apple or Google" section says
  what is kept on the iPad (provider identifier, shared email, display name,
  chosen photo), that none of it is synced, backed up, exported or sent, the
  foreground validity check, sign out vs. remove profile, and the keychain
  record that survives app deletion and is cleared on the next first launch.
  "No third-party code of any kind" is replaced with the one outside library.
- `acknowledgements.html`: "bundles no third-party code" is replaced; Google
  Sign-In and the seven packages it resolves (AppAuth, GTMAppAuth, GTM Session
  Fetcher, App Check Core, GoogleUtilities, Promises, Interop for Google SDKs)
  are listed under the Apache License 2.0, each read from its LICENSE file in
  the resolved SwiftPM checkout (none ships a NOTICE file). AuthenticationServices
  and PhotosUI were added to the Apple frameworks list.
- Every statement was checked against the app source on `fable/account-sign-in`
  (AccountStore, AccountAuthentication, AccountPersistence, AccountPhoto,
  StudentNotesApp scene-phase hook).
- Google sign-in is still unconfigured (the button shows as unavailable). The
  page covers both providers so it needs no second change when Google is on.
- Publish with the app build that ships sign-in, not before. After merge,
  verify privacy.html and acknowledgements.html twice with curl.

# 2026-10-18 — Hosted legal and credits pages for Noto About

Marc requested Privacy, Terms and Acknowledgements open on the existing GitHub
Pages site instead of filling the app's About screen.

## Source and scope

- Isolated checkout: `/Users/marcgallo/noto-support/.Codex/worktrees/legal-pages`.
- Branch `fable/legal-pages`, from fetched `origin/main` at `aefd20a`.
- Added `terms.html` and `acknowledgements.html`, linked from the home page
  and shared legal/support footer. Reused the site's current typography/colors.
- Terms points to the same official Apple Standard EULA already linked by Noto;
  this change creates no custom license. Acknowledgements describe frameworks
  verified in the app source and its own InkLab engine, without invented credits.
- The published privacy policy's wording is unchanged; only navigation was added.
- No dependencies, services, workflows or hosting settings were added.

## Validation

- Source whitespace and local relative-link-target checks passed.
- Inspected Terms/Acknowledgements and the four-card home page in Safari at the
  existing narrow window size and a wider window size. Confirmed footer links,
  wrapping and reading order; restored the window size and closed the preview tab.
- Design scan used its regex fallback because optional HTML parser modules were
  unavailable. It reported no findings; this is not a computed-contrast audit.
- No automated test suite was added or run.

## Publication and app dependency

- Before publication checks: existing privacy page returned HTTP 200; the new
  Terms and Acknowledgements paths returned HTTP 404. Local preview is not a deploy.
- GitHub Pages is configured for the root of `main` (legacy source build).
- Open the PR for Marc to merge per the standing working agreement; do not merge
  or push directly to main. After merge, verify all five public HTML pages twice
  with curl and record HTTP/cache/age headers plus page-specific body markers.
- App changes are on studentnotes `fable/recently-deleted-previews`; About has
  three links, and the subscription privacy link uses the hosted policy. The
  duplicate native privacy screen was removed. Do not release the app links to
  the two new pages until their public URLs are verified live.
