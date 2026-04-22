# Redline Name Cleaner Maintenance

This note explains how `docx-redline-name-cleaner` is maintained as a standalone repository and how it is integrated into `lawreview-tools` as the fourth tool in the suite.

## Repositories involved

- `docx-redline-name-cleaner` — source of truth for the tool itself
- `lawreview-tools` — source of truth for the shared shell, homepage, OG assets, and final integrated site build

## What lives where

### In `docx-redline-name-cleaner`

- `index.html` is the application source of truth
- `assets/vendor/jszip.min.js` is vendored locally and must remain available
- `README.md` documents the standalone tool and links back to the suite

### In `lawreview-tools`

- `src/data/tools.js` is the shared metadata source for all tools
- `scripts/fetch-tools.mjs` pulls browser tools into the shared `lawreview.tools` shell
- `scripts/og-source.mjs` is the source of truth for OG SVG layout and text
- `scripts/generate-og.mjs` renders OG SVG and PNG assets from that source
- `src/pages/index.astro` is the suite homepage

## Current integration model

`Redline Name Cleaner` is integrated the same way as the other browser-based tools, but with one additional fallback:

1. `lawreview-tools/scripts/fetch-tools.mjs` tries to fetch `index.html` from the GitHub repository.
2. If GitHub raw is unavailable for this tool, the script falls back to the local sibling workspace at `../docx-redline-name-cleaner/`.
3. The script writes the integrated page to `lawreview-tools/public/docx-redline-name-cleaner/index.html`.
4. It also copies `assets/vendor/jszip.min.js` into the integrated public output.
5. The shared lawreview.tools shell provides navigation, dark mode toggle, author section, footer, and visual reskinning.

GitHub Pages is not part of the live deployment path for this repository. The standalone repo should trigger `lawreview.tools` rebuilds via `.github/workflows/sync-to-lawreview.yml`, and the obsolete GitHub Pages workflow should remain removed.

## Single sources of truth

- Tool metadata: `lawreview-tools/src/data/tools.js`
- OG layout and text rendering: `lawreview-tools/scripts/og-source.mjs`
- Standalone app logic and UI: `docx-redline-name-cleaner/index.html`

Do not duplicate shared tool metadata in multiple places unless there is a clear reason.

## Safe update workflow

### If you change the app itself

1. Edit `docx-redline-name-cleaner/index.html`
2. Verify the standalone page still works
3. Run the integrated site build in `lawreview-tools`

### If you change tool metadata

1. Edit `lawreview-tools/src/data/tools.js`
2. If OG copy changed, regenerate OG assets
3. Rebuild `lawreview-tools`

### If you change OG design or text layout

1. Edit `lawreview-tools/scripts/og-source.mjs`
2. Run `node scripts/generate-og.mjs` in `lawreview-tools`

## Commands

### Rebuild OG assets

```bash
cd lawreview-tools
node scripts/generate-og.mjs
```

### Rebuild the integrated site

```bash
cd lawreview-tools
npm run build
```

## What to check after changes

- `lawreview-tools/public/docx-redline-name-cleaner/index.html` is regenerated
- `lawreview-tools/public/docx-redline-name-cleaner/assets/vendor/jszip.min.js` exists
- homepage card, nav, footer, and sitemap still include Redline Name Cleaner
- OG assets regenerate successfully
- dark mode still works in both standalone and integrated contexts

## Push and publish

This workspace can help with commit and push steps, but pushing to GitHub is still an explicit action and should be done intentionally after review.

If you want to publish changes:

1. Review the diff
2. Commit in the relevant repository or repositories
3. Push the branch to GitHub

If requested explicitly, those steps can be run from this workspace.