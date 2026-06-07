# nairobi-network-interventions

Simulation-based ranking of road network interventions for Nairobi, Kenya.

---

## The Question

> Given Nairobi's existing road network under peak-hour demand, which planned or proposed interventions — missing links, BRT corridors, highway upgrades, or new alignments — produce the greatest reduction in average travel time?

No target improvement is assumed. The simulation measures what is actually achievable and ranks interventions by impact.

---

## Why This Matters

Nairobi's congestion is **structurally driven**. Drivers lose over 109 hours per year to traffic. The road network carries 2-3x its design capacity on major corridors at peak hour. A JICA master plan in 2006 (NUTRANS) identified the interventions needed — most remain unbuilt nearly 20 years later.

This project tests those interventions computationally, under realistic 2025 demand conditions, and ranks them by measurable impact. The output is a ranked list that transport planners and development finance institutions can use to prioritise capital allocation.

---

## Key Findings So Far

Results are preliminary — greedy search in progress. Early findings from Iteration 1:

| Rank | Intervention | ATT reduction | Notes |
|------|-------------|--------------|-------|
| 1 | LRT — Waiyaki Way | 3.6% | Strongest single intervention |
| 2 | BRT Line 2 — Thika Road | 2.1% | Infrastructure upgrades already underway |
| 3 | Ring Road Parklands (ML 15B) | 1.4% | Stalled EU-funded missing link |
| 3= | Thika Road additional lanes | 1.4% | Ties with the stalled missing link |
| 5 | BRT Line 4 — Jogoo Road | 1.3% | AfDB funded |
| 6 | LRT — Jogoo Road | 0.9% | |
| 7 | Nairobi Riverfront Road | 0.7% | Entirely new alignment |

**Notable finding:** Completing Ring Road Parklands produces the same travel time improvement as a full new highway lane addition. The return on completing what is already partially built is comparable to new capital investment.

**Notable finding:** Several interventions make things worse in isolation — BRT on Outer Ring Road and Mombasa Road both increase average travel time when tested alone. This is because they route additional traffic into corridors that are already saturated. Interaction effects between interventions are significant and justify the greedy search methodology over simple independent ranking.

**Notable finding:** Turning off all disruptions (matatu stops, accidents, lane indiscipline) produces almost no improvement in average travel time. Nairobi's congestion is structurally driven by network undersupply relative to demand — not primarily by operational behaviour. This supports the NUTRANS conclusion that missing links and network expansion matter more than traffic management interventions.



## Methodology

- **Simulator** — UXsim (mesoscopic, Python)
- **Network** — OpenStreetMap, trunk/primary/secondary roads, 982 links, 347 nodes
- **Demand** — calibrated against NUTRANS 2025 projections, 9% peak hour factor
- **Disruptions** — random matatu stops, lane indiscipline, accidents at blackspot junctions
- **Calibration** — demand scaled to produce 60-minute average travel time at baseline
- **Search algorithm** — greedy, captures interaction effects between interventions
- **Platform** — Kaggle notebooks (CPU)

---

## Limitations

- Mesoscopic simulation — individual vehicle behaviour approximated
- No modal shift — BRT/LRT interventions don't model passengers switching from cars
- Synthetic OD matrix — corridor-level demand, not full household travel survey
- Disruption parameters estimated — not yet calibrated against Ma3Route crash frequency data
- Results claimed for simulated conditions only

---

## Data Sources

| Data | Source |
|------|--------|
| Road network | OpenStreetMap |
| Traffic volumes | NUTRANS 2006 / JICA |
| Crash blackspots | World Bank / Ma3Route 2024 |
| BRT plans | NAMATA MRTS documentation |
| Missing link locations | KURA / EU project documentation |

---

## Status

Greedy search running. Iteration 1 complete. Full ranked results to be added when search concludes.

---

## License

MIT — free to use with attribution.
