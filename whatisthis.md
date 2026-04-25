# What is this?

This repository contains a browser-based code architecture analysis app called CodeFlow.

It is a single-file web app in `index.html` that loads dependencies from CDNs, scans a repository or local folder, and shows:

- file dependency graphs
- blast radius analysis
- code ownership and author stats
- security and pattern findings
- code health score

## What are the main files?

1. `index.html`
   - The entire app is bundled here as a single HTML file.
   - It contains styles, UI markup, and the full JavaScript analyzer.
   - It uses React for the UI and D3 for visualizations.

2. `README.md`
   - Documentation for the project, quick start instructions, and feature overview.

3. `tests/`
   - Smoke tests and validation scripts for the analyzer logic.
   - Ensures the parser and markdown extraction logic stay in sync.

4. `tests/fixtures/`
   - Sample files used by tests to verify mixed-language analysis.

## How the app works step by step

1. Open `index.html` in a browser.
2. Enter a GitHub repository URL, open a local folder, or load a ZIP file.
3. The app scans files and identifies code files, markdown files, and supported extensions.
4. It uses the built-in `Parser` object to detect function definitions, dependencies, and file layers.
5. It builds a graph of connections, detects patterns, and computes security or architecture issues.
6. It renders the results in an interactive UI with legend, toolbar, and detailed panels.

## What the tests do

- `tests/html-inline-script-analysis.smoke.js`
  - Verifies the HTML parser can find inline JavaScript and script blocks.
  - Confirms the embedded `Parser` code in `index.html` still extracts functions correctly.

- `tests/codeflow-golden.test.mjs`
  - Loads a small fixture repo from `tests/fixtures/golden-world`.
  - Verifies the analysis output shape, file counts, function counts, and known dependency links.

- `tests/sync-with-html.test.mjs`
  - Compares markdown link extraction between the source-of-truth module and the copy embedded in `index.html`.
  - Ensures `extractMarkdownLinks` and `resolveMarkdownLink` behave identically.

- `tests/codeflow-repo-smoke.mjs`
  - Runs the analyzer against a real repo directory.
  - Summarizes file counts, connections, patterns, and security issues.

## How to run the tests

From the repository root:

```bash
node tests/html-inline-script-analysis.smoke.js
node --test tests/codeflow-golden.test.mjs
node --test tests/sync-with-html.test.mjs
node tests/codeflow-repo-smoke.mjs --json .
```

## Notes on the current update

- Author metadata has been changed to `Sanket Bharadwaj`.
- UI branding was updated in `index.html`.
- Tests were reviewed and all currently pass.

## Why this file exists

This document explains:

- what the project is
- how it is structured
- what each test covers
- how to run the app and tests

It is meant to help new developers understand the repository quickly.
