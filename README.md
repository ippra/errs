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

## Deploying

Two deployments of one file.

**Beta: GitHub Pages, automatic.** `.github/workflows/pages.yml` publishes
`site/` to https://ippra.github.io/errs/ on every push to `main`. It adds a
`noindex` tag to the published copy, so the beta is never found in place of
production. The page shows a Beta label beside the masthead title wherever it
is not served from ippra.net. The repository's Pages source must be set to
GitHub Actions (Settings, Pages).

**Production: ippra.net, by hand. Matt deploys it.** There is nothing to
build. From a fresh clone of `main`:

```
rsync -av --delete site/ <ippra.net host>:<docroot>/errs/
```

The page is one static file with no relative or absolute paths of its own, so
it runs under any path and needs no server-side code. One server setting:
serve `index.html` with `Cache-Control: no-cache` (as for the dashboards, on
the entry URLs `/errs`, `/errs/` and `/errs/index.html`), so a new deploy is
seen without a hard refresh.

To publish a newer version, pull `main` and rsync again.
