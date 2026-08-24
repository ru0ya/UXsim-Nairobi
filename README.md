# nairobi-network-interventions

Simulation-based ranking of road network interventions for Nairobi, Kenya.

---

## The Question

> Given Nairobi's existing road network under peak-hour demand, which planned or proposed interventions — missing links, BRT corridors, highway upgrades, or new alignments — produce the greatest reduction in average travel time?

No target improvement is assumed. The simulation measures what is actually achievable and ranks interventions by impact.

---

## Why This Matters

Nairobi's congestion is **structurally driven**. Drivers lose over 109 hours per year to traffic (NIUPLAN puts the national cost of congestion at ~US$434M/year in lost productivity and fuel). The road network carries 2-3x its design capacity on major corridors at peak hour.

The JICA NIUPLAN master plan (2014) and the NaMSIP Eastlands Urban Renewal Plan (2019) identified the interventions needed — yet Njeru (2024) finds only **1 of 38 NIUPLAN priority projects was ever completed**, with implementation tracking collapsing entirely after 2022. Where institutions cannot prioritise ex-post, computational ex-ante ranking fills the gap: this project tests those interventions under realistic demand conditions and ranks them by measurable impact.

---

## Key Findings

**Superseded.** Results from the first notebook version were affected by a metric flaw (aborted trips inflating average travel time) and unseeded stochastic disruptions, so the published iteration-1 table is withdrawn pending a full re-run on methodology v2. Early validation runs (Enterprise Rd widening, Outer Ring dual carriageway — both actually built) are included in the notebook as model sanity checks.

---

## Methodology (v2)

- **Simulator** — UXsim (mesoscopic, Python)
- **Network** — OpenStreetMap trunk/primary/secondary roads, 982 links / 347 nodes; cached to CSV between sessions
- **Demand** — 11 corridor-level OD pairs, 65k veh @ scale 1.0, loaded within the first half of the horizon so trips can complete
- **Calibration** — link capacity factor tuned until simulated network speed matches NIUPLAN's ~20 km/h do-nothing congested average (replaces the earlier circular ATT-threshold scan)
- **Disruptions** — matatu stops, accidents at blackspots, junction indiscipline (on node flow capacity), CBD speed penalty
- **Reproducibility** — common random numbers: every candidate faces identical disruption sequences via stable-seeded RNG; headline metrics averaged over 3 replications
- **Metrics** — mean/median/p90 travel time over *completed* trips only; aborted trips reported separately; completion rate; share > 60 min
- **Search algorithm** — parallelised greedy search with cumulative application + one-pass swap test for local refinement
- **Candidate sourcing** — NIUPLAN missing-link register & Ch.7 transport plan; NaMSIP Eastlands plan (Riverfront Rd, bridges, viaducts); non-plan candidates explicitly flagged `[Gap]`

---

## Limitations

- Mesoscopic simulation — individual vehicle behaviour approximated
- No true modal shift — BRT/LRT candidates use a corridor car-demand reduction proxy, not mode-choice modelling
- BRT modelled as infrastructure upgrade, not reserved lanes with separate vehicle types
- Synthetic OD matrix — corridor-level demand, not full household travel survey
- Disruption parameters estimated — not calibrated against Ma3Route crash frequency data
- New-link alignments (C-2 connector, viaducts, river bridges) snapped to nearest existing nodes; geometry approximate
- Results claimed for simulated conditions only

---

## Data Sources

| Data | Source |
|------|--------|
| Road network | OpenStreetMap |
| Master plan interventions | NIUPLAN Final Report (JICA, Dec 2014) |
| Eastlands projects | NaMSIP Eastlands Urban Renewal Plan Vol.2 (Real Plan Consultants, Sept 2019) |
| Implementation status / motivation | Njeru (2024), UoN MA thesis — NIUPLAN implementation gaps |
| Congestion baseline | NIUPLAN transport survey (speeds, volumes, mode share) |
| Disruption parameters | Ma3Route / World Bank blackspots, Digital Matatus |

---

## Status

Notebook refactored to methodology v2. Full ranked results to be added when the search re-runs end-to-end (`Run All`).

---

## License

MIT — free to use with attribution.
