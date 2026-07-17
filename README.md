# IEQ Tools

Small, self-contained web calculators for the **BPSD5030 Indoor Environmental Quality** tutorials (University of Sydney, School of Architecture, Design and Planning).

Each tool does the routine arithmetic that used to eat tutorial time, so students can spend class on interpretation. Every result should be validated against the student's own data and the relevant source standard.

## Tools

| File | Tutorial | What it does |
|------|----------|--------------|
| `iaq.html` | Week 8 | Required outdoor airflow (ASHRAE 62.1 Ventilation Rate Procedure); actual ventilation from measured CO₂ (steady-state mass balance); ACH; occupancy scenario explorer with a CO₂-vs-occupancy chart. |
| `acoustics.html` | Week 6 | Energy-averaging and combining sound levels (dB); Sabine equation both directions (absorption ↔ reverberation time); quick speech-intelligibility (STI) estimate from speech-to-noise ratio. |
| `stats.html` | Week 10 / Assignment 2 | Descriptive statistics, paired-samples t-test, Wilcoxon signed-rank, Cohen's dz effect size, and a model Results sentence for the IMRaD write-up. |
| `index.html` | — | Landing page linking the three tools. |

## Design constraints

- **Fully self-contained.** Each HTML file inlines its own CSS and vanilla JavaScript. No external scripts, fonts, stylesheets, or network requests. This keeps them fast, private, offline-capable, and embeddable under a strict Content-Security-Policy (e.g. inside Canvas).
- **No dependencies, no build step.** Open any file in a browser.
- **Light/dark aware and responsive.**

## Hosting (GitHub Pages)

This repo is published as a static site from the IEQLab GitHub organisation:

- Repo: [github.com/IEQLab/tutorial-tools](https://github.com/IEQLab/tutorial-tools) (public)
- Live site: [ieqlab.github.io/tutorial-tools](https://ieqlab.github.io/tutorial-tools/)

Pages is configured under **Settings → Pages → Build and deployment → Deploy from a branch**, branch `main`, folder `/ (root)`. The tools are live at:

- `https://ieqlab.github.io/tutorial-tools/iaq.html`
- `https://ieqlab.github.io/tutorial-tools/acoustics.html`
- `https://ieqlab.github.io/tutorial-tools/stats.html`

(GitHub Pages on the free org plan requires the repo to be **public**.)

## Embedding in Canvas

Link out to a tool, or embed with an iframe in the Rich Content Editor's HTML view:

```html
<iframe src="https://ieqlab.github.io/tutorial-tools/iaq.html" width="100%" height="900" style="border:1px solid #ccc;border-radius:8px"></iframe>
```

Note: some Canvas instances restrict iframe embeds to an allow-listed set of domains. If the embed does not render, use a plain link (opens in a new tab) instead.

## Accuracy notes

- ASHRAE 62.1 and Sabine calculations are exact implementations of the standard formulas.
- The paired t-test p-value uses the regularised incomplete beta function (Student's t distribution). The Wilcoxon p-value uses the normal approximation with continuity and tie corrections; for very small samples, confirm against exact tables or statistical software.
- The STI figure is a speech-to-noise approximation for a quick read only; use the full IEC 60268-16 method for anything reported.

## Licence

MIT. See `LICENSE`.
