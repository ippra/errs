# errs - Enhanced Reliability and Resilience Score Worksheet

An interactive worksheet for comparing energy mitigation options with the
Enhanced Reliability and Resilience Score (ERRS). A group names two to four
options, scores each from 1 to 5 on six components, and the page works the
formula and ranks the options:

```
ERRS = [(Reliability + Resilience) × Feasibility × Acceptability
        × Vulnerable Population Impact] ÷ Cost
```

- **Beta:** https://ippra.github.io/errs/
- **Release:** https://ippra.net/errs

## What it does

- **Click-to-score sheet.** Each component has a 1-5 scale with a description
  of every level and examples of options that tend to score high and low.
- **Live formulas.** Scores fill in each option's formula as they are entered,
  with the arithmetic shown step by step. Hovering a term highlights the score
  it came from.
- **Comparison.** Options are ranked once at least two are fully scored.
- **Weight by importance (optional).** The group rates each component's
  importance from 1 to 3 and sees an importance-weighted average, on the 1-5
  scale with cost reversed, alongside the standard ERRS. A note says whether
  the two methods rank the options the same way.
- **Worked example and exercise.** "Load example" fills in a scored pair of
  options; "Load exercise" loads the two options from the ESF-12 stakeholder
  meeting exercise with the scores left blank.
- **Nothing leaves the browser.** Entries are saved in the browser's local
  storage only. There is no server and no account.

## What is here

| path | what it is |
|---|---|
| `site/index.html` | the whole worksheet: markup, styles and script in one file |
| `reference/errs_worksheet.pptx` | the original one-page print worksheet the site is built from |
| `.github/workflows/pages.yml` | publishes `site/` to GitHub Pages on every push to `main` |

There is no build step and no external dependency. The page carries the look
the institute's dashboards share (`ippra/s3ok_dash`, `ippra/wxdash`): the IPPRA
bar, the masthead with its viridis strip, and light, dark and greyscale themes
under "Adjust colors". To preview,
open `site/index.html` in a browser, or serve it:

```sh
python3 -m http.server 8902 --directory site    # http://localhost:8902
```

## Releasing

A push to `main` publishes the beta. When the beta is ready, copy
`site/index.html` to `ippra.net/errs`. The page uses no absolute paths, so it
runs unchanged at either address.
