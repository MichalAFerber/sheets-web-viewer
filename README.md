# Sheets Viewer

A fast, mobile-first, **single-file** spreadsheet viewer. Drag & drop an Excel or
OpenDocument workbook and browse every sheet as a clean table — one tap flips to a
CSV **source** view. It's a **viewer, not an editor** — no toolbars, no accounts,
no uploads. Everything runs locally in your browser.

🔗 **Live:** <https://sheets-viewer.us/>

![Single file](https://img.shields.io/badge/build-single%20HTML%20file-success) ![No build step](https://img.shields.io/badge/build%20step-none-success) ![License](https://img.shields.io/badge/license-MIT-blue)

> Part of the **[File Viewer](https://file-viewer.us/) family** — HTML, Markdown,
> ePUB, PDF, Data, DOCX, and Sheets each have their own dedicated viewer. Use the
> **☰ menu** in the header to jump between them.

## Features

- 📑 **Every sheet, as a table** — sheet **tabs** switch between worksheets;
  numbers, dates, and text render as formatted values with a sticky header row.
- `</>` **Source view** — one tap shows the active sheet as syntax-highlighted
  **CSV** (quoted-field aware).
- 🔀 **Drop to replace** — drop a new workbook while one is open and it replaces
  the current view.
- ☰ **Family menu** — a hamburger flyout links to every viewer.
- 🫥 **Distraction-free header** — auto-hides while you read, collapsing to a thin
  handle; hover, tap, or scroll up to bring it back.
- ✅ **File-type checking** — only spreadsheet types are accepted; other files are
  politely declined so you land in the right viewer.
- 🎨 **Pick any background color** — text and borders adapt for contrast (light
  **and** dark), remembered across visits.
- 🪶 **One file, no build** — `index.html` is self-contained and works offline,
  even from `file://`.
- 📊 **Privacy-friendly analytics** — self-hosted, cookieless
  [Plausible](https://plausible.io/); your files never leave your device.

## Supported file types

`.xlsx` `.xlsm` `.xlsb` `.xls` `.xlt` `.xltx` `.xltm` `.xlam` `.ods` `.fods`
`.dif` `.prn` `.dbf` `.numbers` `.xlml` `.wk1` `.wk3` `.et`

> CSV and TSV are handled by the sibling **[Data Viewer](https://data-viewer.us/)**
> (which also does JSON, YAML, and XML), so they're intentionally not duplicated here.

## Quick start

**Just open it.** Download [`index.html`](index.html), double-click it — no
server, no build, no internet needed.

```sh
python3 -m http.server 8080   # then open http://localhost:8080
```

## Deploy to Cloudflare Pages

Connect the repo (**Workers & Pages → Create → Pages → Connect to Git**),
framework preset **None**, build command blank, output directory `/`. The
[`_headers`](_headers) file applies a strict CSP automatically. Add the custom
domain **sheets-viewer.us** under the project's Custom domains tab.

## How it works

Everything is in [`index.html`](index.html) — app logic plus two inline libraries,
so parsing and highlighting work offline:

- [**SheetJS**](https://sheetjs.com/) (Community Edition) `v0.18.5` (Apache-2.0) —
  reads `.xlsx`, `.xls`, `.ods`, and many more spreadsheet formats.
- [**highlight.js**](https://github.com/highlightjs/highlight.js) `v11.9.0`
  (BSD-3-Clause) — highlights the CSV source view.

Tables are built as **escaped DOM** (never `innerHTML` of untrusted cell text),
so the viewer's CSP stays strict (`default-src 'none'`, no external assets).

**Note:** this is a viewer — it shows **values + structure**. Rich cell styling,
colors, merged-cell formatting, and charts aren't rendered; formulas show their
last-saved computed values.

## Credits

| Component | Version | License |
| --- | --- | --- |
| [SheetJS (xlsx)](https://sheetjs.com/) | 0.18.5 | Apache-2.0 |
| [highlight.js](https://github.com/highlightjs/highlight.js) | 11.9.0 | BSD-3-Clause |
| [JetBrains Mono](https://github.com/JetBrains/JetBrainsMono) | subset | OFL-1.1 |

The file-type icon (favicon and header icon) is from
[vscode-icons](https://github.com/vscode-icons/vscode-icons) (MIT). Analytics by
[Plausible](https://plausible.io/).

## License

[MIT](LICENSE) © 2026 Michal Ferber, aka **TechGuyWithABeard**. Bundled
components retain their own licenses — see [`LICENSE`](LICENSE) and
[Credits](#credits).
