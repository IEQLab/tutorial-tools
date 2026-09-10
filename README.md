# Tutorial Tools

Small, self-contained web calculators for University of Sydney units in the School of Architecture, Design and Planning.

Each tool does the routine arithmetic that used to eat tutorial time, so students can spend class on interpretation. Every result should be validated against the student's own data and the relevant source standard.

## Layout

Tools are organised one directory per unit, with each tutorial's tool named by its week:

```
index.html                       Top-level directory: one card per unit
bpsd5030/
  index.html                     Unit page: BPSD5030 tools, arranged by week
  week04-iaq.html
  week06-acoustics.html
  week08-lighting.html
  week09-ratings.html
  week10-stats.html
```

To add a unit, create a `{unit}/` directory, drop its `weekNN-*.html` tools in, add a `{unit}/index.html` (copy an existing unit page and relist), and add a card to the top-level `index.html`.

## Tools

### BPSD5030 — Indoor Environments

| File | Tutorial | What it does |
|------|----------|--------------|
| `bpsd5030/week04-iaq.html` | Week 4 | Required outdoor airflow (ASHRAE 62.1 Ventilation Rate Procedure); actual ventilation from measured CO₂ (steady-state mass balance); ACH; occupancy scenario explorer with a CO₂-vs-occupancy chart. |
| `bpsd5030/week06-acoustics.html` | Week 6 | Energy-averaging and combining sound levels (dB); Sabine equation both directions (absorption ↔ reverberation time); a conform/doesn't-conform check of measured LAeq and mid-frequency RT60 against the AS/NZS 2107:2016 indicative ranges, taking both of the week's two spaces side by side and reporting the difference; quick speech-intelligibility (STI) estimate from speech-to-noise ratio, plus the full octave-band method. |
| `bpsd5030/week08-lighting.html` | Week 8 | Enter illuminance readings as a spatial grid; renders a heatmap of the working plane and computes the uniformity ratio (min ÷ avg), diversity (min ÷ max), and a box plot of the spread. Also benchmarks the average against the AS/NZS 1680.2 maintained-illuminance target for a chosen space type (the Week 8 brief's conform / doesn't-conform judgement). In-class exploratory aid; the submitted figure stays the student's own build. |
| `bpsd5030/week09-ratings.html` | Week 9 | Two-act challenge on building rating systems. Act 1: take a building to a target NABERS IE star rating on a fixed budget via real upgrades or measurement tactics, with a recertification that collapses gamed ratings. Act 2: certify the same building under WELL by buying credits (real per-feature points from the WELL v2 scorecard), exposing how cheap policy credits score the same as expensive performance credits. Six built-in building profiles. |
| `bpsd5030/week10-stats.html` | Week 10 / Assignment 2 | Full A2 analysis companion. Names the design (with a paired-vs-independent warning), computes descriptive statistics, paired-samples t-test, Wilcoxon signed-rank, and Cohen's dz effect size with the working shown on the student's own data, then models the Results sentence and Methods paragraph and carries a pre-submission checklist. Absorbs the former standalone A2 worked-example handout. |

Note on week order: from Semester 2, 2026 the BPSD5030 IAQ tutorial runs in Week 4 and lighting in Week 8, having previously been the other way around. Both files were renamed to follow their week, so the old `week04-lighting.html` and `week08-iaq.html` URLs no longer resolve; anything pointing at them (Canvas pages, saved links) needs updating. Filename week numbers are the contract here, so a future change in week order means another rename.

### BPSD6030 — Building Systems

| File | Tutorial | What it does |
|------|----------|--------------|
| `bpsd6030/week05-hvac-selector.html` | Week 5 / Assignment 2 | Stepped HVAC system selector for the Australian commercial sector. The student walks their building (program, NCC climate zone, size, floors) through fresh-air, heating/cooling, system, and plant choices across the all-air (VAV, CAV), air-plus-water (DOAS + chilled beam / fan-coil / radiant), refrigerant (VRF, split/packaged DX), and evaporative families. Draws the selection as a parametric colour-coded schematic, explains each part in plain language, and generates a ranked decarbonisation pathway (electrification, refrigerant GWP, heat recovery, clean supply) with a justification box to carry into Assignment 2. Deliberately does not size plant or estimate loads — DesignBuilder stays the load authority. Adapts the openly published MIT SDL HVAC System Selector (Irani, Reinhard & Reinhart, 2023, CC BY) to Australian systems, metric units, and a carbon focus. |

## Design constraints

- **Fully self-contained.** Each HTML file inlines its own CSS and vanilla JavaScript. No external scripts, fonts, stylesheets, or network requests. This keeps them fast, private, offline-capable, and embeddable under a strict Content-Security-Policy (e.g. inside Canvas).
- **No dependencies, no build step.** Open any file in a browser.
- **Light/dark aware and responsive.**

## Layout convention

To keep cognitive load manageable for students meeting these calculations for the first time, every tool follows one shared, tabbed layout. `bpsd5030/week04-iaq.html` is the reference implementation — copy its CSS/JS blocks and markup structure when building or updating a tool.

> **Direction (decided 2026-09-02): these tools serve their tutorial first.**
>
> They were built as general-purpose calculators that a tutorial happened to link to, and were deliberately written to stand alone. That was the wrong call. In practice they are used almost exclusively inside their own tutorial session, so supporting that session's learning exercises beats supporting hypothetical other uses. Where the two conflict, the tutorial wins.
>
> The immediate cause was Week 4, 2026 S2: students could not tell which tutorial activity needed which tab, and defaulted to whichever tab drew a picture. The first fix (a single collapsed "Where this fits" strip per tool) treated tutorial alignment as a small concession to be quarantined in one element. The decision goes further: alignment is the point, not a concession, so the strip is open by default and the tools speak to their tutorial directly.
>
> **The tutorial is the source of truth for the mapping.** Each tutorial `.md` in `teachr` carries an activity-to-tab table, and the tool's own strip mirrors it. A renumber is edited in the `.md` first, then in the tool. The two files that move together are listed under "Tool and tutorial pairs" below.

- **One thing at a time, in tabs.** Each distinct piece of functionality lives on its own tab (`role="tablist"`/`tab`/`tabpanel`, numbered pills, keyboard-navigable with arrow/Home/End keys and a Back/Next row). Tools whose steps build on each other use the tabs as an **ordered stepper** (IAQ, stats, ratings); the HVAC selector keeps its existing wizard logic, restyled to the same numbered-pill look. Tools with independent calculators use **free-navigation tabs** (acoustics, lighting).
- **A primer per tab.** Each tab opens with a short `.primer` — a one-line statement of purpose plus 2–3 sentences on "the idea behind the number." Primers may speak to the tutorial directly ("the plateau you measured in Activity 1"). A tool still carries no Canvas URL: linking out of a page students open mid-session is a different question from naming the exercise they are doing.
- **The orientation strip.** A `details.mapsto` ("Where this fits in today's tutorial"), **open by default**, sits between the tablist and the first panel and maps each tutorial segment to the tab that serves it. Tutorial vocabulary is not confined to it; it is the summary, not the quarantine. Two rules:
  - **Account for the whole session, not just the tabbed part.** The closing `.none` line names every segment that uses **no** tab. Where the counts nearly line up (four activities, four tabs) students read a 1:1 map that is not there, and the near-miss misleads more than no numbering would. It is equally wrong to list two tabless steps and stay silent about the two whole Parts that also use nothing.
  - **Use the tutorial's own numbering, unambiguously.** Say "Part 2, step 4" where the tutorial has more than one sequence numbered from 1 (BPSD5030 Week 6 has bare 1–4 in Part 1 and bare 1–6 in Part 2). Carry the segment title in italics as well as the number, so a wrong number is still recoverable.
  - Keep it muted, never the teal `details.maths` treatment, which means "optional maths aside".
- **Say whose numbers are on screen.** Where one set of inputs feeds several tabs, a `.datasource` line under the orientation strip reports whether the student is looking at the worked example or their own data, and gains `.mine` (accent border) once it is theirs. It carries `aria-live="polite"`, so only write to it on an actual change, and it is **hidden entirely while there is nothing on screen to label** ("Numbers on screen: no readings yet" is a caption for numbers that are not there, and it lands before the student has done anything that would give it meaning). It appears at the moment it starts saying something. This is what stops a student landing on a chart tab, seeing a finished curve, and never registering that it is not their room. Keep it a **status, not an instruction** ("Numbers on screen: the worked example"), because the line shows on every tab and an instruction repeated where it cannot be acted on reads as noise; how to replace the example goes in the header, stated once. Tools whose tabs are genuinely independent calculators (acoustics) omit the line entirely: there is no single global answer to "whose numbers", and a static header note is the honest version. That holds even now the acoustics tool takes two spaces in its AS/NZS 2107 check, because the pair is scoped to that one section rather than carried across the five tabs.

  The line must track **every** way the numbers become the student's, not just the obvious one. The IAQ tool has two independent routes (typing over the room profile, and dropping a CSV of measured CO₂ on tab 3) and reported only the first, so a student looking at a chart of their own readings was told they were looking at the worked example. Where a tool has an explicit "load example" button, hang the state on an origin flag rather than diffing against the defaults; diff against a snapshot only where the example is pre-filled with no button to hook (IAQ).
- **No cross-week references.** A tool never mentions another week's tool or tutorial ("unlike the Week 4 tool…"). Curriculum sequencing is authoring scaffold: invisible to the student in front of this tool, and confusing when it surfaces. Describe how *this* tool behaves and stop there. Referring to the tool's own week, or to an assessment the student is actually working on, is fine.
- **Progressive disclosure.** The always-visible surface is kept calm — primer, inputs, live results/verdict, chart. Formulas, derivations, and standards notes move into collapsible `details.maths` ("the maths behind it") panels. Short glosses use an accessible info-popover (a real `<button>` with `aria-expanded`, working on click, keyboard, and touch) rather than native `title=` tooltips.
- **Every control declares its states.** Default, hover, `:focus-visible`, `:active` and disabled, on every button and not only the tabs. Text inputs keep plain `:focus`. There is no loading state: the arithmetic is synchronous.
- **A System / Light / Dark control** sits top-right on every page. JS resolves the choice and writes `data-theme` on `<html>` before first paint, so the dark palette lives in one `:root[data-theme="dark"]` block rather than being duplicated across a media query. The choice is shared across all tools via `localStorage` under `tt-theme`, and is silently forgotten where a Canvas iframe blocks storage. Tools that draw to canvas or build an SVG from computed tokens expose a `window.__ttRedraw` hook so a theme change repaints them.
- **Footers carry provenance.** In order: what the numbers are (method, standard, edition), who stands behind them (the lab, the school, the unit, and any individual whose work is being used), when the tool was last revised, and where the source is. Update the revision month whenever a tool's behaviour changes.

### Tool and tutorial pairs

The mapping lives in both files and is maintained by hand, so they move together. Edit the
tutorial `.md` first, then mirror it in the tool.

| Tool | Tutorial (in the `teachr` repo) |
|---|---|
| `bpsd5030/week04-iaq.html` | `bpsd5030/tutorials/week04.md` |
| `bpsd5030/week06-acoustics.html` | `bpsd5030/tutorials/week06.md` |
| `bpsd5030/week08-lighting.html` | `bpsd5030/tutorials/week08.md` |
| `bpsd5030/week09-ratings.html` | `bpsd5030/tutorials/week09.md` |
| `bpsd5030/week10-stats.html` | `bpsd5030/tutorials/week10.md` |
| `bpsd6030/week05-hvac-selector.html` | none — see below |

To check a pair, extract the tab pill labels from the tool and the tab names from the
tutorial's table and diff the two lists, then read the strip's "uses no tab" line against the
tutorial's actual segment count. Both drifted before the first commit: a Week 6 table listing
four tool-using steps under a sentence that said three, and a strip that named two tabless
steps while ignoring two whole Parts. This is a verification step, not a build step; the
repo's no-dependencies, no-build-step constraint stands.

**BPSD6030 is the exception.** `week05-hvac-selector.html` has no tutorial to map to: the unit
has no `tutorials/` directory, and the tool is set as pre-class priming and then reused for
Assignment 2. It is also a JS-rendered stepper rather than an ARIA tablist, so the strip's
markup does not port unchanged. If it gets an orientation strip it needs different content
("before class, and again for A2") and its own markup.

### Open work: aligning the tools to their tutorials

Scoped 2026-09-02. The strip, the vocabulary and the tab-to-segment mapping are done across
all five BPSD5030 tools; what follows is what is left.

1. **Order tabs to the tutorial, not to the tool's internal logic.** Now that the mapping is
   written down per tool, the places where the two run on different axes are visible.
   BPSD5030 Week 6 is the live case: its tutorial runs Part 2 steps 1-6 while its five tabs
   run on a different axis entirely, which the strip currently papers over by listing them
   out of order. Week 10 is the milder case (four Steps against six tabs, two of which sit
   outside the session).
2. **Build the Week 4 share-back collector.** Deferred on 2026-09-02 ("no collector this
   round") under the old assumption. Activity 4 asks each group for three numbers living on
   three different tabs, with nothing gathering them. That is a tutorial-shaped feature, and
   the decision above is exactly the argument for building it. Week 4 has already run for
   2026 S2, so this is for the next offering.
3. **Carry Week 6's two spaces beyond the benchmark.** The AS/NZS 2107 check now takes Space 1
   and Space 2 side by side and reports the difference, which serves Part 2 step 6 and the
   take-home comparison. The other four tabs still hold one set of inputs, so a group still
   runs tab 1 twice and copies the results across by hand. A `.datasource` line for the
   acoustics tool (previously deferred for having no single answer to "whose numbers") only
   becomes meaningful if this happens.

   Partly addressed on 2026-09-10: tab 1 now has a second entry mode that takes the Part 2
   step 1 measurement sheet as it stands (one row per position, eight unweighted bands plus
   that position's LAeq) and returns its Average row, and hands the result on with buttons that
   write the band spectrum into the STI noise row on tab 4 and the LAeq into either space of
   the benchmark. That removes the nine-runs-of-one-text-box problem and two rounds of
   transcription, but it is still one space at a time: a group works Space 1, sends what it
   needs, then retypes for Space 2.
4. **Fix the Week 9 profile control's placement.** `#profile` drives both acts but sits inside
   `panel-1`, so switching to Act 2 hides the control that set the scenario. Activity 2 is its
   own 15-minute segment.

**Not up for revision.** The no-cross-week-references rule stands: it is about what confuses a
student sitting in front of one tool, not about how closely a tool tracks its tutorial.
Aligning harder to *this* week's tutorial is the decision; mentioning *other* weeks remains
wrong.

## Hosting (GitHub Pages)

This repo is published as a static site from the IEQLab GitHub organisation:

- Repo: [github.com/IEQLab/tutorial-tools](https://github.com/IEQLab/tutorial-tools) (public)
- Live site: [ieqlab.github.io/tutorial-tools](https://ieqlab.github.io/tutorial-tools/)

Pages is configured under **Settings → Pages → Build and deployment → Deploy from a branch**, branch `main`, folder `/ (root)`. The unit index and tools are live at:

- `https://ieqlab.github.io/tutorial-tools/` (all units)
- `https://ieqlab.github.io/tutorial-tools/bpsd5030/` (BPSD5030 tools)
- `https://ieqlab.github.io/tutorial-tools/bpsd5030/week04-iaq.html`
- `https://ieqlab.github.io/tutorial-tools/bpsd5030/week06-acoustics.html`
- `https://ieqlab.github.io/tutorial-tools/bpsd5030/week08-lighting.html`
- `https://ieqlab.github.io/tutorial-tools/bpsd5030/week09-ratings.html`
- `https://ieqlab.github.io/tutorial-tools/bpsd5030/week10-stats.html`
- `https://ieqlab.github.io/tutorial-tools/bpsd6030/` (BPSD6030 tools)
- `https://ieqlab.github.io/tutorial-tools/bpsd6030/week05-hvac-selector.html`

(GitHub Pages on the free org plan requires the repo to be **public**.)

## Embedding in Canvas

Link out to a tool, or embed with an iframe in the Rich Content Editor's HTML view:

```html
<iframe src="https://ieqlab.github.io/tutorial-tools/bpsd5030/week04-iaq.html" width="100%" height="900" style="border:1px solid #ccc;border-radius:8px"></iframe>
```

Note: some Canvas instances restrict iframe embeds to an allow-listed set of domains. If the embed does not render, use a plain link (opens in a new tab) instead.

## Accuracy notes

- ASHRAE 62.1 and Sabine calculations are exact implementations of the standard formulas.
- The paired t-test p-value uses the regularised incomplete beta function (Student's t distribution). The Wilcoxon p-value uses the normal approximation with continuity and tie corrections; for very small samples, confirm against exact tables or statistical software.
- The quick STI figure is a speech-to-noise approximation for a quick read only; use the full IEC 60268-16 method for anything reported. That full octave-band STI method reproduces the BPSD5030 STI workbook developed by Densil Cabrera (School of Architecture, Design and Planning, University of Sydney), verified cell-for-cell against the original spreadsheet.

## Licence

MIT. See `LICENSE`.
