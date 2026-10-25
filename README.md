# Match possession viewer and build up analysis

The original per-match Eventing application with a team-selectable build-up analysis and standalone report export. The site opens with the supplied PSG–Barcelona example from 20 October 2026.

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

## Hosting

`index.html` contains the complete application and bundled comparison sample. No tracking files, tracking viewer or separate prototype pages are deployed. GitHub Pages serves the root of the main branch. The original per-match source's possession logic, display layers and Playbook pages are retained.
