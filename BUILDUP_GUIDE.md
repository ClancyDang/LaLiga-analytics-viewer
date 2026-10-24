# Barcelona defensive third build up analysis

Open `eventing-buildup.html` in a browser. The file contains the PSG–Barcelona match from 20 October 2026 and a compact historical sample calculated from the supplied La Liga ZIP. It does not need a server or tracking data.

Scroll below the possession pitch to **Barcelona build-up profile**. Choose all starts, goal kicks only, or other starts excluding restarts. Use the example buttons to inspect successful and unsuccessful possessions. These buttons clear event filters so the selected possession is visible.

**Download build-up PDF** exports the profile alone. **Playbook pdf** includes the profile immediately after the cover for any selected Barcelona match. Ordinary possession pages retain the existing event-filter behavior. The build-up profile always covers the whole selected match within the chosen start category; it is not filtered by the possession viewer's event checkboxes. Referenced example IDs might therefore not appear in a filtered Playbook.

The existing match ZIP picker can load other fixtures. **Import Barcelona history ZIP** replaces the historical comparison sample. It scans HTML/HTM/TXT pages, keeps Barcelona fixtures, deduplicates by date and home/away team IDs, and skips invalid or undated fixtures. Only match dates strictly earlier than the selected fixture contribute to the baseline; same-day fixtures are excluded. Reimport after changing analysis definitions if rebuilding the compact historical file.

## Definitions

- Possessions come from the original per-match application's confirmed-control reconstruction, including periods 1–4. No new consecutive-team-event possession shortcut is used.
- A build-up begins with the first own effective-control or successful possession-gain event in a reconstructed possession. Its coordinates must be valid and its x value must be below 100/3. A missing start location excludes that possession; a later event is not substituted as the start.
- A controlled exit requires a retained-control event location or a completed-pass endpoint with x at least 100/3. Unsuccessful pass endpoints never establish an exit. A successful direct pass into the final third can count as both an exit and a final-third arrival.
- Outcomes follow the same possession through its end, not a fixed time horizon. Final third means x at least 200/3. The box is approximated by x at least 83 and y from 21.1 to 78.9, matching the application's existing goal-link thresholds.
- Exit route uses the first controlled location outside the defensive third: left when provider y is above 200/3; right below 100/3; centre otherwise. These are attack-relative provider coordinates. The display route map uses this same orientation for both home and away Barcelona fixtures.
- An early loss is recorded only when the possession ends with confirmed opposition control before exit. Other no-exit sequences, such as stoppages and period endings, remain a separate outcome. The loss count does not describe every possible football turnover.
- Goal kicks use the GoalKick event type or qualifier. Other restarts are detected using the source application's restart function. All starts includes all three groups; other starts excludes all detected restarts.
- Each outcome is counted at most once per build-up. Outcomes overlap and are not mutually exclusive. Route counts are mutually exclusive and sum to the number of build-ups.
- Rates use all build-ups in the selected scope as denominator. Route rates use build-ups in that route. Average exit time and pass attempts use successful exits only. A pass attempted after the ball is already outside the defensive third is excluded from the pass-to-exit count.
- The route diagram connects each route's mean start to its mean first controlled location outside the defensive third. It is an aggregate diagram, not an actual pass path. Width represents route frequency. Crosses mark starts of no-exit sequences.

## Supplied example

The supplied PSG–Barcelona event page contains 195 reconstructed match possessions. Barcelona has 46 qualifying defensive-third build-ups: 36 exits, 12 final-third arrivals, 6 box arrivals, 3 shot-producing possessions, and 9 confirmed early losses. Exit routes: 12 left, 11 centre, 13 right, and 10 without an exit. Goal-kick starts: 3; other starts excluding restarts: 36; other restarts: 7.

The historical ZIP contains 9 unique Barcelona fixtures and 328 qualifying build-ups before the example match. Baseline totals: 234 exits, 137 final-third arrivals, 48 box arrivals, 40 shot-producing possessions, and 57 confirmed early losses.

These are descriptive observed rates. La Liga opponents differ from the PSG match, and the feature does not estimate pressure, VAEP, causal effects, or tracking-based movement. xG/xGOT are retained in the application's other report pages but are not used as the primary build-up outcome.

## Files and rebuilding

- `eventing-buildup.html`: standalone application and embedded example/history.
- `buildup-analysis.js`: new analysis, interface and PDF page module.
- `barcelona-buildup-history.json`: compact per-build-up historical records, calculated from the provided ZIP.
- `build-buildup.mjs`: integrates the module into the earlier enhanced full per-match source and embeds the supplied example payload. It uses the temporary readable example-source extraction path from this working session.
- `test-buildup.cjs` and `verify-buildup-export.cjs`: development checks for failed endpoints, controlled arrivals, missing coordinates, loss definitions, historical import, date cutoffs, selectors, possession navigation and PDF exports.

The original Word source files and existing site files are not replaced by this standalone build. For GitHub Pages, publish this application as `buildup.html` alongside `index.html`.
