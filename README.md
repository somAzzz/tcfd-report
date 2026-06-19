# TCFD Project Demo

**Live demo URL**: https://somAzzz.github.io/tcfd-report/

## What's in this report

A self-contained interactive HTML showcasing a production NLP system for
climate-related financial disclosure (TCFD) analysis of A-share annual reports.

Built on: 2026-06-19
Report size: 3841.7 KB
Test count: 366 passing

## How to view locally

Open `index.html` in any modern browser. Loads Plotly and Mermaid from CDN.

## Deploying to GitHub Pages

1. Create a new **public** repo: `tcfd-report`
2. Push: `index.html`, `README.md`, `.nojekyll`
3. Settings → Pages → Branch: `main`, Folder: `/ (root)` → Save

**Do NOT push the main `frequency_analyzer` repo.**

## Pre-push leakage check

```bash
python scripts/check_leakage.py index.html
```

Must exit 0 before pushing.
