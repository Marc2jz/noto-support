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

# 2026-11-03 — Legal and support pages become redirects to notonotes.com

## What changed and why

- `privacy.html`, `terms.html`, `acknowledgements.html` and `support.html` are now
  small redirect pages (same `<title>`, `rel=canonical`, `meta refresh` with 0 delay,
  a visible notice with a plain link, styled by `style.css`). No scripts, no tracking.
  The old text is gone from these files (it remains in git history).
- `index.html` cards now link straight to `https://notonotes.com/support`, `/privacy`,
  `/terms` and `/acknowledgements`. Nothing else on it was changed.
- Why: the App Store listing and older app versions still link to these four URLs. The
  old text is outdated (privacy.html says "no account system, no servers of its own"
  while the app now links to a notonotes.com account). The maintained pages live on
  the website.

## Merge order (do not skip)

- Merge this only AFTER the website version that carries the moved app facts
  (the current privacy/terms/acknowledgements/support content) is live at
  notonotes.com. Merging earlier would redirect App Store users to pages that lack
  those facts. Verify the four notonotes.com URLs answer 200 with the expected text first.

## Open PRs that touch the same files

- PRs #6, #8, #9, #10 add privacy.html text for features not yet shipped; PR #11 adds
  support.html email reports. All five edit files that are now redirects and will
  conflict. Not closed or edited here.
- After this redirect, their text belongs in the website's `src/LegalPages.jsx` or the
  `/support` page, when those features ship.
