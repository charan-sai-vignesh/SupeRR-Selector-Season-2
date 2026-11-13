# SupeRR Selector Season 2 — Round 1 Methodology Report

## Executive summary

This analysis ranks players by how much their delivery-level contribution improves in defined high-pressure states relative to their own usual performance in comparable situations. It covers the supplied IPL and T20I data from 2022–2026. Pressure is identified using only the score state known before a delivery; match result and player reputation are not used.

The working data contains 837 in-scope matches with standard first- and second-innings ball-by-ball records (367 IPL and 470 T20I), 193,988 deliveries, and 74,722 deliveries flagged as pressure. Super-over innings are excluded. The rankings use a minimum of 50 pressure balls across at least 3 matches for batters, and 60 pressure legal balls across at least 3 matches for bowlers.

## 1. Data and scope

The analysis joins `ball_by_ball.csv` to `matches.csv` and `competitions.csv` by match and competition IDs. T20 competitions are restricted to competition names beginning with “IPL”; this excludes other competitions also labelled T20 in the data. All T20Is are retained. The data used spans January 2022 to November 2026. Sixteen in-scope match records did not have usable standard-innings ball records. Innings 3 and 4 (super overs) are excluded because they are too short and structurally different from normal innings.

A legal ball is any delivery other than a wide or no-ball (“Overstep”). Innings overs are taken from the revised-overs fields when present and positive, otherwise 20 overs are assumed. The first-innings total is reconstructed from batter runs and both extras fields; a revised target is used for the chase when supplied, otherwise the target is first-innings total plus one.

## 2. Pressure definition

Pressure is assigned before each delivery from the state of the innings. It combines late-innings wicket risk in the first innings with required-rate and wicket constraints in a chase:

- **First innings:** pressure if 30 or fewer scheduled legal balls remain and at least 4 wickets have fallen; or 12 or fewer balls remain and at least 2 wickets have fallen.
- **Second innings:** while runs remain to win, pressure if the required run rate (RRR) is at least 9.0; or RRR is at least 7.5 with at least 5 wickets down; or 12 or fewer balls remain with at least 18 runs required.

For a chase, $\mathrm{RRR}=6\times\frac{\mathrm{runs\ required}}{\mathrm{legal\ balls\ remaining}}$. On an ordinary 20-over schedule, innings phases are also derived from scheduled balls: powerplay = first 30%, middle = next 45%, and death = final 25% (approximately overs 1–6, 7–15, and 16–20).

These thresholds represent a demanding scoring equation, loss of batting resources, and late-innings leverage. They are intentionally transparent and state-based. They do not use the eventual winner, final margin, or award outcomes, avoiding hindsight leakage. The first-innings definition is necessarily an innings-squeeze proxy: without a target, it cannot identify closeness to a match result.

## 3. Performance and rating construction

### Batters

For each batter delivery, the run-equivalent contribution is:

$$\mathrm{BatImpact}=\mathrm{batter\ runs}-8\times\mathrm{striker\ dismissals}.$$

Wides are excluded from balls faced; a no-ball counts as faced. Dismissal value is set to 8 runs as a simple, fixed cost of losing a wicket. This captures both scoring and the risk of losing a wicket, rather than relying on strike rate alone.

### Bowlers

For each bowler delivery, the contribution is:

$$\mathrm{BowlImpact}=-\mathrm{bowler\ charged\ runs}+8\times\mathrm{bowler\ credited\ wickets}.$$

The runs charged to a bowler include batter runs and wides/no-ball extras, but exclude byes and leg-byes. Wickets credited to bowlers are caught, bowled, LBW, stumped, and hit wicket; run-outs and other non-credit dismissals are not counted. The denominator is legal balls, while wide/no-ball costs remain in the numerator.

### Player-specific usual baseline and pressure lift

Each player's non-pressure impact rate is calculated separately within the same format (IPL/T20I), season, innings number, innings phase, and wickets-lost band (0–2, 3–5, 6–10). Small player/context samples are shrunk toward that player's format-season non-pressure rate using 30 prior-ball equivalents; if that baseline is unavailable, the comparable cohort context rate is used. This adjusts for role and context while avoiding direct comparison of IPL run environments with T20I environments.

The raw pressure lift is the pressure impact less the estimated usual impact for the same pressure exposure, expressed per 100 batter-faced balls or per 100 legal balls bowled. Positive lift means the player performed better than their expected usual level under comparable non-pressure conditions. For bowlers, impact is already signed so a less-negative or positive difference is better.

To moderate small samples, the reported rating is:

$$\mathrm{Rating}=\mathrm{Lift}_{100}\times\frac{n}{n+80}\times(0.75+0.25p),$$

where $n$ is pressure exposure and $p$ is the share of the player's pressure-appearance matches with positive match-level lift. The 80-ball shrinkage constant reduces volatility from limited exposure; match consistency adjusts the rating modestly rather than allowing a few exceptional deliveries to dominate. Rankings are sorted from highest to lowest rating.

## 4. Eligibility and fairness

- Batter eligibility: at least 50 pressure balls faced and pressure appearances in at least 3 matches.
- Bowler eligibility: at least 60 pressure legal balls and pressure appearances in at least 3 matches.
- Format- and season-specific usual baselines prevent IPL/T20I and season run environments from being mixed in the comparison.
- Phase and wickets-lost matching helps account for different batting roles and bowling contexts.
- Pressure outcomes are compared with the same player's own historical non-pressure performance, with transparent cohort fallback and small-sample shrinkage.
- Player IDs, rather than names alone, are used for aggregation. The same player is not repeated in either list.

The resulting eligible populations were 301 batters and 237 bowlers. The eligibility cutoffs are modest to retain enough candidates; ranks near the cutoff should be treated as less certain.

## 5. Final rankings and evidence

“Pressure impact” and “usual” are run-equivalent units per 100 pressure balls (batters) or legal balls (bowlers). “Lift” is their difference. Positive-match share is the percentage of pressure-appearance matches in which match-level lift was positive. Rating is the shrunken, consistency-adjusted lift used to order the list.

### Top 10 batters

| Rank | Player (ID) | Pressure balls | Matches | Pressure runs / outs | Pressure impact | Usual | Lift | Positive matches | Rating |
|---:|---|---:|---:|---:|---:|---:|---:|---:|---:|
| 1 | Shashank Singh (2756) | 370 | 31 | 677 / 13 | 154.86 | 66.00 | 70.76 | 51.6% | 51.14 |
| 2 | Reeza Hendricks (768) | 372 | 15 | 624 / 11 | 144.09 | 85.08 | 59.01 | 60.0% | 43.71 |
| 3 | Muhammad Waseem (22565) | 193 | 9 | 319 / 7 | 136.27 | 76.11 | 60.16 | 66.7% | 38.99 |
| 4 | Vipraj Nigam (46066) | 72 | 9 | 139 / 5 | 137.50 | 24.36 | 90.92 | 44.4% | 37.09 |
| 5 | Karun Nair (930) | 84 | 5 | 143 / 3 | 141.67 | 57.12 | 84.55 | 40.0% | 36.81 |
| 6 | Ashutosh Sharma (8101) | 290 | 25 | 511 / 16 | 132.07 | 62.12 | 50.29 | 56.0% | 35.08 |
| 7 | Aaron Finch (250) | 82 | 6 | 131 / 5 | 110.98 | 36.53 | 74.44 | 66.7% | 34.54 |
| 8 | Fakhar Zaman (2921) | 243 | 17 | 412 / 11 | 133.33 | 84.44 | 48.48 | 58.8% | 32.72 |
| 9 | Sanju Samson (2258) | 547 | 44 | 956 / 27 | 135.28 | 89.34 | 41.74 | 59.1% | 32.69 |
| 10 | Mark Chapman (3374) | 325 | 25 | 534 / 16 | 124.92 | 81.07 | 45.39 | 56.0% | 32.42 |

### Top 10 bowlers

| Rank | Player (ID) | Pressure legal balls | Matches | Runs conceded / credited wickets | Pressure impact | Usual | Lift | Positive matches | Rating |
|---:|---|---:|---:|---:|---:|---:|---:|---:|---:|
| 1 | Matthew Humphreys (22471) | 124 | 8 | 137 / 13 | -26.61 | -125.78 | 99.16 | 75.0% | 56.51 |
| 2 | Mohammad Nawaz (2490) | 313 | 22 | 331 / 30 | -29.07 | -80.34 | 54.14 | 59.1% | 38.71 |
| 3 | Sakib Hussain (35318) | 149 | 10 | 203 / 11 | -77.18 | -122.93 | 53.13 | 70.0% | 31.97 |
| 4 | George Dockrell (1101) | 68 | 7 | 58 / 4 | -38.24 | -107.11 | 76.23 | 57.1% | 31.27 |
| 5 | Abrar Ahmed (5979) | 295 | 24 | 292 / 21 | -42.03 | -76.99 | 44.79 | 50.0% | 30.83 |
| 6 | George Linde (4229) | 84 | 6 | 98 / 9 | -30.95 | -96.38 | 60.67 | 83.3% | 29.78 |
| 7 | Tabraiz Shamsi (4237) | 108 | 6 | 135 / 12 | -36.11 | -88.83 | 52.72 | 66.7% | 27.76 |
| 8 | Sufiyan Muqeem (34485) | 170 | 10 | 165 / 11 | -45.29 | -78.14 | 42.26 | 80.0% | 27.30 |
| 9 | Benjamin Sears (4856) | 173 | 14 | 214 / 15 | -54.34 | -80.84 | 44.42 | 42.9% | 26.04 |
| 10 | Gudakesh Motie (3276) | 214 | 17 | 262 / 14 | -70.09 | -103.46 | 37.58 | 58.8% | 24.54 |

The largest batting lift in the top ten is Vipraj Nigam's, but it comes from 72 pressure balls across 9 matches, so its score is strongly sample-shrunk. Shashank Singh leads because his positive lift is supported by 370 pressure balls across 31 matches. In the bowling list, Matthew Humphreys' improvement is supported by 124 pressure balls across 8 matches; Mohammad Nawaz combines a slightly smaller lift with much greater exposure (313 pressure balls, 22 matches), which is why the latter ranks second after adjustment.

## 6. Reliability checks and limitations

Consistency is checked at match level: a pressure appearance is a match with positive pressure exposure, and its lift is compared with the player's usual context baseline. The report shows the positive-match share, while the rating applies only a modest consistency multiplier. Pressure exposure and appearances are shown so that a high score with a thin sample is visible rather than hidden.

The model is descriptive, not causal. The 8-run wicket value and pressure cutoffs are defensible choices, not uniquely correct constants; different thresholds or wicket values can alter the order. The first-innings pressure proxy is less complete than chase pressure because no target is available during that innings. The supplied data begins in 2022, and player roles, team strength, venue, pitch, opposition quality, match conditions, and tactical choices are not fully modeled. Revised targets are used when present, but incomplete metadata and missing ball records may still affect coverage. Finally, positive match share measures frequency, not the size or importance of each individual game state.

## 7. Reproduction

Run `analyze_pressure.py` from this folder with Python 3 and pandas installed. It reads the original CSVs and writes `batter_pressure_rankings.csv` and `bowler_pressure_rankings.csv`. These files contain the full eligible rankings, player IDs, sample sizes, pressure and usual rates, consistency shares, and ratings. The top-10 tables above are drawn directly from those generated results.
