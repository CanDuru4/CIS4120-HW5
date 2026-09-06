# CIS 4120 HW5 — Implementation Prototype (Port 5176)

![React](https://img.shields.io/badge/React-19-61dafb?logo=react&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-7-3178c6?logo=typescript&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-8-646cff?logo=vite&logoColor=white)
![Status](https://img.shields.io/badge/status-coursework%20prototype-lightgrey)

Interactive high-fidelity prototype for CIS 4120 (Introduction to Human–Computer Interaction) HW5.
It models a customs-declaration review workflow: an analyst creates a case, types the declarant
fields by hand, uploads the supporting PDFs, links each field to the region of a document that
proves it, and a reviewer validates the result in a field-by-document matrix before the case is
sent on. The audience is the course staff grading HW5 and the teammates iterating on the design —
it is a UI prototype, not a production system, and it has no backend.

This repository tracks only the latest **port 5176** prototype. Earlier per-port experiments
(5173/5174/5175) are deliberately untracked and listed in [`.gitignore`](.gitignore).

## Key features

All ten requirement surfaces live behind the `Req 1` … `Req 10` tabs of a single app shell:

| Tab | Surface |
| --- | --- |
| Req 1 | Hello-world boot screen that confirms the app runs on the target runtime |
| Req 2 | Style tokens — typography, colours, icons, badges, buttons |
| Req 3 | Role dashboard: cases grouped by status, role-specific actions (Analyst / Reviewer, plus Case Reviewer / Lead Reviewer / CEO dashboard views) |
| Req 4 | Case creation and manual entry of the fixed declarant fields |
| Req 5 | Multi-file PDF upload with tabbed document viewing (separate files or one combined file) |
| Req 6 | Manual evidence linking between a declarant field and a highlighted region of the active PDF |
| Req 7 | Send-file validation — missing values, missing links, and value mismatches block the send, with an explanation flow |
| Req 8 | Review matrix of declarant field × document with per-cell state |
| Req 9 | Field inspection modal showing the linked PDF region next to the typed value |
| Req 10 | Case routing between roles with comments and notifications |

Declarant fields covered by the prototype: company name, gross weight, invoice number,
item description, quantity.

## Tech stack

- **React 19** + **TypeScript 7** (strict mode)
- **Vite 8** dev server and build
- **react-router-dom 7** (`BrowserRouter` shell)
- **pdf-lib** — used by the sample-PDF generator script
- **pdfjs-dist 6** — declared for PDF rendering, not yet imported by any tracked source file
- No backend, no API keys: all case state lives in the browser

## Getting started

### Prerequisites

- Node.js `^20.19.0 || >=22.12.0` (required by Vite 8)
- npm 10+

### Install and run

```bash
git clone https://github.com/CanDuru4/CIS4120-HW5.git
cd CIS4120-HW5
npm ci
npm run dev
```

Then open <http://localhost:5176>. The dev script uses `--strictPort`, so it fails fast rather
than silently moving to another port if 5176 is taken.

### Environment variables

None. The prototype reads no environment variables and needs no `.env` file.

### Scripts

| Script | What it does |
| --- | --- |
| `npm run dev` | Vite dev server on port 5176 (`dev:5176` is an alias) |
| `npm run build` | `tsc -b` type-check, then `vite build` into `dist/` |
| `npm run preview` | Serve the contents of `dist/` |
| `npm run generate-sample-pdfs` | Regenerate the fixtures in `sample_pdfs/` with pdf-lib |
| `npm run lint` | Wired to ESLint, but no `eslint.config.js` exists yet, so it currently errors out |

### Sample data

`sample_pdfs/` holds ready-made declaration and supporting documents (plus `_demo` variants and
combined single-file versions) so a grader can exercise the upload and evidence-linking flows
without hunting for real PDFs.

## Project structure

```
index.html                     app shell; dynamically imports the 5176 entry point
src/
  main.5176.tsx                React root: StrictMode + BrowserRouter + Port5176App
  port5176/
    Port5176App.tsx            the whole prototype (tabs, case state, upload, linking, matrix)
    port5176.css               prototype styles
  styles/global.css            base resets and shared tokens
scripts/generateSamplePdfs.js  pdf-lib fixture generator
sample_pdfs/                   generated PDF fixtures
vite.config.ts                 Vite + @vitejs/plugin-react config
```

## State and persistence

Case-level data — declarant values, uploaded documents (stored as data URLs), evidence links,
comments and notifications — is persisted to `localStorage` under the key
`hw5_port5176_state_v1`. Clearing site data resets the prototype to an empty case list. Nothing
is uploaded anywhere.

## Build

```bash
npm run build
npm run preview
```

Known limitation: `index.html` loads the app through a `@vite-ignore` dynamic import, so the
production bundle contains only that loader and `npm run preview` will not render the prototype.
Use `npm run dev` for demos and grading until the entry point is made static.

## CI and dependency maintenance

- No GitHub Actions workflows. CodeQL runs as GitHub's default setup, not from a workflow file
  in this repository.
- [`.github/dependabot.yml`](.github/dependabot.yml) checks npm dependencies weekly and batches
  them into two grouped PRs: `npm-minor-and-patch` for minor/patch bumps, and `npm-majors` for
  major bumps. Majors are grouped rather than ignored so that each one still gets a deliberate
  `npm ci && npm run build` check before it is merged.
- `package.json` carries an `overrides` block that pins transitive packages
  (`@humanfs/node`, `brace-expansion`, `nanoid`, `postcss`, `react-router`) to versions at or
  above their first patched release. Do not lower those floors without checking the
  corresponding advisories; `npm audit` should report zero vulnerabilities.

## AI usage attribution

- Portions of this repository were developed with AI coding assistance (including code
  generation, refactoring suggestions, bug-fix drafts, and documentation edits).
- Team members reviewed, tested, and adjusted AI-assisted output before accepting changes.
- Final responsibility for implementation decisions, correctness, and submission content
  remains with the team.

## License

No license file — coursework, all rights reserved by the authors.

## Author

Can Duru — <https://canduru.net>
