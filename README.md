# Match possession viewer and build up analysis

The original per-match Eventing application with a team-selectable build-up analysis and standalone report export. The site opens with the supplied PSG–Barcelona example from 20 October 2026. A second bundled example, Barcelona–Real Madrid on 25 October 2026, includes two dynamic-event measures.

## Presenting the feature

1. Open the site and click **Build-up analysis only**.
2. Select a team and a start category.
3. Compare controlled exits, final-third arrivals, box entries, shots and confirmed early losses.
4. Click a current-match result or exit route to inspect its underlying possessions.
5. Click **Export build-up report only** to download one page. The original **Playbook pdf** remains available in the full viewer.

The bundled comparison sample covers 88 La Liga matches and 20 clubs. Only the selected team's fixtures dated strictly before the analysed match enter its baseline. PSG has no history in the supplied La Liga sample. Match selection and historical sample import remain separate controls.

**Load match ZIP** loads fixtures to analyse. **Import team history ZIP** replaces the historical sample with both teams from each valid dated fixture. Imported files remain in the current browser session; reloading restores the bundled example and history.

## Reading the report

Build-ups begin with controlled possession in the defensive third. Exit means retained control beyond that third. Subsequent outcomes follow the same possession, so they can overlap. No exit does not necessarily mean a turnover: stoppages and period endings are separated from confirmed opponent control.

The pitch arrows summarize mean start and exit locations, rather than individual passes. Clicking a possession opens the original pitch viewer for the actual sequence. Small-sample labels indicate fewer than 20 build-ups; this is a display rule, not a significance test. Full definitions are available under **Calculation notes**.

## Dynamic build-up measures

Choose **2026-10-25 · Barcelona vs Real Madrid** in the Match menu. Both teams are supported; the team and build-up start selectors apply to these measures. They also appear in the one-page build-up report and the build-up page of the full Playbook.

- **Controlled exits from high-pressure starts:** confirmed exits divided by complete defensive-third possessions whose first player-possession begins under the source's `high_pressure` or `very_high_pressure` rating. Pressure later in the sequence does not qualify a start. An exit needs a subsequent own-control start outside the defensive third or a successful pass with an outside reception. Unsuccessful pass endpoints never count.
- **Completed first-line-breaking passes:** successful passes carrying `first_line_break=True`, shown as a proportion of successful passes with an explicit True/False assessment. Counts follow the entire defensive-start possession, including actions after the first exit. Missing flags are unassessed, not failed line breaks. Passing-option records are not actual passes and are not used.

For Barcelona, all starts produce **10/12 high-pressure exits (83.3%)** and **16/104 assessed completed passes breaking the first line (15.4%)**. There are **37 complete native build-ups**, 13 with unknown starting pressure and 136 completed passes without a line-break assessment. These are source-specific denominators, not the event viewer's 33 reconstructed build-ups. Real Madrid has 11/29 high-pressure exits and 17/85 assessed completed passes breaking the first line.

Sequences are reconstructed from the dynamic file's first/last team-possession flags, sorted by period and frame, with duplicate event IDs removed. Incomplete sequences and sequences crossing periods or team boundaries are omitted. Fully extrapolated player-possession records cannot provide pressure, exit or pass evidence. Goal-kick and other-restart scope is identified from the first reception type; unknown starts are excluded from the non-restart category. Small-sample labels are display cues, not statistical tests.

Expand **Inspect dynamic build-ups and calculation rules** to see native sequence IDs, players, clocks, starting pressure, exits, pass assessment coverage and completed line-break actions. These are separate source records; they are not automatically matched to WhoScored possession IDs. The fixture is gated by its date and both team names, not cross-provider numeric IDs. No dynamic values or historical dynamic comparison are inferred for other fixtures. Reloading does not require re-importing the supplied example.

The bundled dynamic subset comes from `2087076_dynamic_events.csv`, using `2087076_match.json` for fixture identity. Only the player-possession fields needed by these two measures are included. No tracking viewer, positional tracking, EPV, xG or prediction model is added.

## Hosting

`index.html` contains the complete application and bundled comparison sample. No tracking files, tracking viewer or separate prototype pages are deployed. GitHub Pages serves the root of the main branch. The original per-match source's possession logic, display layers and Playbook pages are retained.
