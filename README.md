# Tutorial Tools

Small, self-contained web calculators for University of Sydney units in the School of Architecture, Design and Planning.

Each tool does the routine arithmetic that used to eat tutorial time, so students can spend class on interpretation. Every result should be validated against the student's own data and the relevant source standard.

## Layout

Tools are organised one directory per unit, with each tutorial's tool named by its week:

```
index.html                       Top-level directory: one card per unit
bpsd5030/
  index.html                     Unit page: BPSD5030 tools, arranged by week
  week04-lighting.html
  week06-acoustics.html
  week08-iaq.html
  week09-ratings.html
  week10-stats.html
```

To add a unit, create a `{unit}/` directory, drop its `weekNN-*.html` tools in, add a `{unit}/index.html` (copy an existing unit page and relist), and add a card to the top-level `index.html`.

## Tools

### BPSD5030 — Indoor Environments

| File | Tutorial | What it does |
|------|----------|--------------|
| `bpsd5030/week04-lighting.html` | Week 4 | Enter illuminance readings as a spatial grid; renders a heatmap of the working plane and computes the uniformity ratio (min ÷ avg), diversity (min ÷ max), and a box plot of the spread. Also benchmarks the average against the AS/NZS 1680.2 maintained-illuminance target for a chosen space type (the Week 4 brief's conform / doesn't-conform judgement). In-class exploratory aid; the submitted figure stays the student's own build. |
| `bpsd5030/week06-acoustics.html` | Week 6 | Energy-averaging and combining sound levels (dB); Sabine equation both directions (absorption ↔ reverberation time); quick speech-intelligibility (STI) estimate from speech-to-noise ratio. |
| `bpsd5030/week08-iaq.html` | Week 8 | Required outdoor airflow (ASHRAE 62.1 Ventilation Rate Procedure); actual ventilation from measured CO₂ (steady-state mass balance); ACH; occupancy scenario explorer with a CO₂-vs-occupancy chart. |
| `bpsd5030/week09-ratings.html` | Week 9 | Two-act challenge on building rating systems. Act 1: take a building to a target NABERS IE star rating on a fixed budget via real upgrades or measurement tactics, with a recertification that collapses gamed ratings. Act 2: certify the same building under WELL by buying credits (real per-feature points from the WELL v2 scorecard), exposing how cheap policy credits score the same as expensive performance credits. Six built-in building profiles. |
| `bpsd5030/week10-stats.html` | Week 10 / Assignment 2 | Full A2 analysis companion. Names the design (with a paired-vs-independent warning), computes descriptive statistics, paired-samples t-test, Wilcoxon signed-rank, and Cohen's dz effect size with the working shown on the student's own data, then models the Results sentence and Methods paragraph and carries a pre-submission checklist. Absorbs the former standalone A2 worked-example handout. |

### BPSD6030 — Building Systems

| File | Tutorial | What it does |
|------|----------|--------------|
| `bpsd6030/week05-hvac-selector.html` | Week 5 / Assignment 2 | Stepped HVAC system selector for the Australian commercial sector. The student walks their building (program, NCC climate zone, size, floors) through fresh-air, heating/cooling, system, and plant choices across the all-air (VAV, CAV), air-plus-water (DOAS + chilled beam / fan-coil / radiant), refrigerant (VRF, split/packaged DX), and evaporative families. Draws the selection as a parametric colour-coded schematic, explains each part in plain language, and generates a ranked decarbonisation pathway (electrification, refrigerant GWP, heat recovery, clean supply) with a justification box to carry into Assignment 2. Deliberately does not size plant or estimate loads — DesignBuilder stays the load authority. Adapts the openly published MIT SDL HVAC System Selector (Irani, Reinhard & Reinhart, 2023, CC BY) to Australian systems, metric units, and a carbon focus. |

## Design constraints

- **Fully self-contained.** Each HTML file inlines its own CSS and vanilla JavaScript. No external scripts, fonts, stylesheets, or network requests. This keeps them fast, private, offline-capable, and embeddable under a strict Content-Security-Policy (e.g. inside Canvas).
- **No dependencies, no build step.** Open any file in a browser.
- **Light/dark aware and responsive.**

## Layout convention

To keep cognitive load manageable for students meeting these calculations for the first time, every tool follows one shared, tabbed layout. `bpsd5030/week08-iaq.html` is the reference implementation — copy its CSS/JS blocks and markup structure when building or updating a tool.

- **One thing at a time, in tabs.** Each distinct piece of functionality lives on its own tab (`role="tablist"`/`tab`/`tabpanel`, numbered pills, keyboard-navigable with arrow/Home/End keys and a Back/Next row). Tools whose steps build on each other use the tabs as an **ordered stepper** (IAQ, stats, ratings); the HVAC selector keeps its existing wizard logic, restyled to the same numbered-pill look. Tools with independent calculators use **free-navigation tabs** (acoustics, lighting).
- **A primer per tab.** Each tab opens with a short `.primer` — a one-line statement of purpose plus 2–3 sentences on "the idea behind the number." Written to stand alone (companion to, not dependent on, the tutorial), with no hard links back to Canvas.
- **Progressive disclosure.** The always-visible surface is kept calm — primer, inputs, live results/verdict, chart. Formulas, derivations, and standards notes move into collapsible `details.maths` ("the maths behind it") panels. Short glosses use an accessible info-popover (a real `<button>` with `aria-expanded`, working on click, keyboard, and touch) rather than native `title=` tooltips.

## Hosting (GitHub Pages)

This repo is published as a static site from the IEQLab GitHub organisation:

- Repo: [github.com/IEQLab/tutorial-tools](https://github.com/IEQLab/tutorial-tools) (public)
- Live site: [ieqlab.github.io/tutorial-tools](https://ieqlab.github.io/tutorial-tools/)

Pages is configured under **Settings → Pages → Build and deployment → Deploy from a branch**, branch `main`, folder `/ (root)`. The unit index and tools are live at:

- `https://ieqlab.github.io/tutorial-tools/` (all units)
- `https://ieqlab.github.io/tutorial-tools/bpsd5030/` (BPSD5030 tools)
- `https://ieqlab.github.io/tutorial-tools/bpsd5030/week04-lighting.html`
- `https://ieqlab.github.io/tutorial-tools/bpsd5030/week06-acoustics.html`
- `https://ieqlab.github.io/tutorial-tools/bpsd5030/week08-iaq.html`
- `https://ieqlab.github.io/tutorial-tools/bpsd5030/week09-ratings.html`
- `https://ieqlab.github.io/tutorial-tools/bpsd5030/week10-stats.html`
- `https://ieqlab.github.io/tutorial-tools/bpsd6030/` (BPSD6030 tools)
- `https://ieqlab.github.io/tutorial-tools/bpsd6030/week05-hvac-selector.html`

(GitHub Pages on the free org plan requires the repo to be **public**.)

## Embedding in Canvas

Link out to a tool, or embed with an iframe in the Rich Content Editor's HTML view:

```html
<iframe src="https://ieqlab.github.io/tutorial-tools/bpsd5030/week08-iaq.html" width="100%" height="900" style="border:1px solid #ccc;border-radius:8px"></iframe>
```

Note: some Canvas instances restrict iframe embeds to an allow-listed set of domains. If the embed does not render, use a plain link (opens in a new tab) instead.

## Accuracy notes

- ASHRAE 62.1 and Sabine calculations are exact implementations of the standard formulas.
- The paired t-test p-value uses the regularised incomplete beta function (Student's t distribution). The Wilcoxon p-value uses the normal approximation with continuity and tie corrections; for very small samples, confirm against exact tables or statistical software.
- The quick STI figure is a speech-to-noise approximation for a quick read only; use the full IEC 60268-16 method for anything reported. That full octave-band STI method reproduces the BPSD5030 STI workbook developed by Densil Cabrera (School of Architecture, Design and Planning, University of Sydney), verified cell-for-cell against the original spreadsheet.

## Licence

MIT. See `LICENSE`.
