# House Hunt Scorecard

A weighted scorecard for comparing houses. Two people rate 21 criteria from 1 to 10, the ratings are averaged, weighted by priority, and turned into a score from 1 to 100.

Everything lives in `index.html`, with no build step.

## Scoring

- Each criterion has a priority from 1 (must-have) to 5 (nice-to-have). Priority 1 counts 5× and priority 5 counts 1×.
- Each criterion's score is the average of both people's ratings. If only one person has rated it, that rating is used.
- Weighted average (1–10) → score: `1 + (avg − 1) × 99 / 9`, so all 1s = 1 and all 10s = 100.
- Unrated criteria are skipped. Each card shows how many of the 42 ratings are filled in.

## Data

Houses are saved in the browser's `localStorage`. To move them to another device, use **Names & data → Copy share link**. Opening that link merges the houses into that device's list, keeping ratings from both copies. You can also download and import JSON backups.

## Hosting

Served by GitHub Pages from the `main` branch root.
