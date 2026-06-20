# TCFD Project Demo

**Live demo URL**: https://somAzzz.github.io/tcfd-report/

## What's in this report

A self-contained interactive HTML showcasing a production NLP system for
climate-related financial disclosure (TCFD) analysis of A-share annual reports.

Built on: 2026-06-20
Report size: 3865.0 KB
Test count: 375 passing

### Sections

1. **Sunburst** — 3 dimensions (Policy / Market / Technology) → 83 clusters →
   individual keywords. Click any segment to drill down; click a keyword to
   see the original annual-report sentence in the side panel.
2. **Streamgraph** — TCFD keyword mentions per year (2000–2024), split by
   dimension. Drag the bottom slider to zoom into a year range.
3. **Network** — Keyword co-occurrence graph for the most recent 3 years.
   Nodes are draggable; edge thickness encodes co-occurrence weight.
4. **Sankey** — Keyword flow across the 4-stage pipeline (sampling →
   extraction → evaluation → aggregation). Click any flow to see source
   sentences.
5. **AI Pipeline Resilience & Engineering Health** — 4-bar comparison of
   the pre/post refactor metrics (memory footprint, concurrency, schema
   compliance, test coverage). Click any bar to expand the live module
   dependency graph of the evaluation subpackage.

All data is anonymized (company names are replaced with generic labels)
and embedded in the HTML; runtime libraries are loaded from ECharts, Alpine,
Google Fonts, and Mermaid CDNs.

## How to view locally

Open `index.html` in any modern browser.

## Development

To rebuild the report from the source repo:

```bash
# 1. From the main frequency_analyzer repo:
PYTHONPATH=src python scripts/build_report.py --output output/report/

# 2. Run the pre-push leakage check (script auto-runs it too, must exit 0):
python scripts/check_leakage.py output/report/index.html

# 3. Stage and push to tcfd-report (NOT the main repo):
cd output/report
git add index.html README.md
git commit -m "vNN: <description>"
git push origin main
```

The build script:
- Runs `pytest --collect-only` to fill the "Test count" stat
- Discovers the evaluation subpackage module graph via AST
- Assembles 4 ECharts options (sunburst / streamgraph / network / sankey)
  + 1 AI Pipeline dashboard + 1 module graph
- Renders the Jinja2 template with all data inlined (single-file HTML)
- Auto-runs the leakage check and exits 1 if it fails

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
