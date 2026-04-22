# Redline Name Cleaner

**Standardize comment and tracked-change names in Word documents** before you circulate a draft outside your editorial or research team.

🔗 **[lawreview.tools/docx-redline-name-cleaner/](https://lawreview.tools/docx-redline-name-cleaner/)**

---

## Why this exists

Law review editors, professors, and research assistants routinely circulate Word drafts whose comments and tracked changes expose internal names that should not appear in the outward-facing version of the file.

Cleaning those names manually inside Word is slow, repetitive, and easy to do inconsistently. Redline Name Cleaner handles that cleanup in the browser, without uploading the document anywhere.

## What it does

Redline Name Cleaner scans one or more `.docx` files for comment and tracked-change names, lets you choose which identities to unify, and downloads cleaned copies with updated Word revision metadata.

If multiple original names are changed to the exact same replacement name in a document, Word will display them as the same visible review identity in the output file.

No installation. No account. No upload. Your documents never leave your browser.

## Features

- **Multiple files** — upload and process several `.docx` files at once
- **Per-file settings** — each document keeps its own selections and replacement names
- **Saved presets** — store common replacement names in your browser for reuse
- **Batch download** — export all edited files as a single `.zip`
- **Fully client-side** — documents are processed locally in your browser
- **Vendored dependency** — JSZip is bundled in the repository, so the app does not rely on a CDN at runtime

## How to use

1. Open **[lawreview.tools/docx-redline-name-cleaner/](https://lawreview.tools/docx-redline-name-cleaner/)**
2. Upload one or more `.docx` files
3. Open each file card and review the detected names
4. Select the people you want to unify
5. Apply a typed replacement name or a saved preset
6. Download the edited file, or download all edited files as one `.zip`

## Requirements

- A modern browser: Chrome, Firefox, Safari, or Edge
- A `.docx` Word document containing comments and/or tracked changes

## Privacy

Your documents are processed entirely in your browser's memory. No file content is uploaded to any server. No account is required. No usage data is collected.

## Project structure

- `index.html` — the complete application UI, styling, and client-side logic
- `assets/vendor/jszip.min.js` — vendored JSZip runtime used to read and rewrite `.docx` archives
- `THIRD_PARTY_LICENSES.md` — third-party attribution and license notes
- `.github/workflows/sync-to-lawreview.yml` — triggers the `lawreview.tools` rebuild after pushes to `main`
- `MAINTENANCE.md` — maintenance notes for the lawreview.tools integration

## Part of lawreview.tools

Redline Name Cleaner is one tool in the **[lawreview.tools](https://lawreview.tools)** suite — a free, open-source collection of Bluebook tools for law review editors and legal scholars:

| Tool | What it does | When to use it |
|------|-------------|----------------|
| **[Zotero Perma Archiver](https://lawreview.tools/zotero)** | Auto-archives URLs to perma.cc as you save items in Zotero | While writing |
| **[PermaDrop](https://lawreview.tools/permadrop/)** | Batch-archives all URLs in a `.docx` to perma.cc | Before submission |
| **[SupraDrop](https://lawreview.tools/supradrop/)** | Audits citation logic across all footnotes | Before submission |
| **Redline Name Cleaner** | Standardizes visible review identities in comments and tracked changes | Before circulation |

Typical workflow: Zotero Perma Archiver while researching → PermaDrop to archive remaining URLs → SupraDrop to catch citation errors → Redline Name Cleaner to clean visible review identities before circulation or submission.

## Maintenance

For integration details, update flow, and the relationship with `lawreview-tools`, see [MAINTENANCE.md](MAINTENANCE.md).

## License

Copyright (C) 2026 [Kirin Chang](https://kirinchang.com)  
Research Fellow, U.S.-Asia Law Institute, NYU School of Law

Licensed under the [GNU Affero General Public License v3.0](LICENSE).  
If you modify this tool and run it as a network service, you must release your modified source code under the same license.

## Third-party software

This repository vendors [JSZip](https://stuk.github.io/jszip/) version 3.10.1. See [THIRD_PARTY_LICENSES.md](THIRD_PARTY_LICENSES.md) and [`assets/vendor/JSZIP_LICENSE.markdown`](assets/vendor/JSZIP_LICENSE.markdown).

---

*Not affiliated with or endorsed by The Bluebook, Zotero, or perma.cc.*
