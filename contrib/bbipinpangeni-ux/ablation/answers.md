# The answers: 3 questions x 3 setups

Written by contrib/ablation.py. Model Qwen/Qwen3-1.7B, thinking off, seed 1, on cpu. Data: SUMO Fowler Ave scenario (the demand and seed are in the start_live call).

Read each answer against the right answer, then grade it in the table in ABLATION.md: right, partly or wrong, and why in a few words. The table to copy:

| Question | A. Without your tools | B. Your tools, plain | C. Your tools as written |
|---|---|---|---|
| queue_storage | ? | ? | ? |
| fowler_delay | ? | ? | ? |
| pine_stopped | ? | ? | ? |

## queue_storage

**Question:** At 1800 s in the Fowler Avenue simulation, what is the queue length and remaining upstream storage at Bruce B Downs & Pine southbound?

**Right answer (tasks.json):** Queue 359.6 ft; storage 1060.8 ft; remaining storage 701.2 ft; occupancy 33.9%.

Before the model's first turn, the harness called: `start_live(demand='demand', seed=1)`, `advance(seconds=1800)`.

### A. Without your tools

Tools called: `get_approach_state(intersection='Bruce B Downs & Pine', approach='SB')`. 2 turns, 1648 s. Run: `ablation/runs/without__queue_storage.json`

> The queue length at Bruce B Downs & Pine southbound is 16 vehicles, and the remaining upstream storage is 360 feet.

### B. Your tools, plain

Tools called: `get_approach_state(intersection='Bruce B Downs & Pine', approach='SB')`. 2 turns, 1896 s. Run: `ablation/runs/plain__queue_storage.json`

> The queue length at Bruce B Downs & Pine southbound is 16 vehicles, and the remaining upstream storage is 360 ft.

### C. Your tools as written

Tools called: `get_approach_state(intersection='Bruce B Downs & Pine', approach='SB')`. 2 turns, 2171 s. Run: `ablation/runs/full__queue_storage.json`

> The queue length at Bruce B Downs & Pine southbound is 16 vehicles, and the remaining upstream storage is 360 ft.

## fowler_delay

**Question:** At 1800 s in the Fowler Avenue simulation, what is the eastbound median travel time, free-flow reference, additional travel time and completed-trip count?

**Right answer (tasks.json):** Measured median 4.5 min from 31 trips; free-flow 2.0 min; additional time approximately 2.5 min.

Before the model's first turn, the harness called: `start_live(demand='demand', seed=1)`, `advance(seconds=1800)`.

### A. Without your tools

Tools called: `get_corridor_state(direction='EB')`. 2 turns, 1615 s. Run: `ablation/runs/without__fowler_delay.json`

> The eastbound median travel time at Fowler Ave EB at 1800 s is 4.5 minutes. The free-flow reference is 2.0 minutes. The additional travel time is 2.5 minutes, and the completed-trip count is 31.

### B. Your tools, plain

Tools called: `get_corridor_state(direction='EB')`. 2 turns, 1874 s. Run: `ablation/runs/plain__fowler_delay.json`

> The eastbound median travel time at 1800 s in the Fowler Avenue simulation is 4.5 minutes. The free-flow reference is 2.0 minutes. The additional travel time is 2.5 minutes, and the completed-trip count is 31.

### C. Your tools as written

Tools called: `corridor_delay_assessment(direction='EB')`. 2 turns, 2144 s. Run: `ablation/runs/full__fowler_delay.json`

> The eastbound median travel time on Fowler Avenue at 1800 s is 4.50 minutes, based on 31 completed trips. The free-flow reference travel time is 2.00 minutes. The additional travel time compared to the free-flow reference is +2.50 minutes. These values are rounded toolkit travel-time estimates, so the calculated difference is approximate. The sample count is reported; no statistical precision or reliability threshold has been established. This is not a measured bridge work-zone effect.

## pine_stopped

**Question:** At 1800 s in the Fowler Avenue simulation, how many vehicles are on Bruce B Downs & Pine southbound, how many are stopped, and what is their mean speed?

**Right answer (tasks.json):** 17 vehicles; 16 stopped below 0.1 m/s; instantaneous mean speed 2.5 mph.

Before the model's first turn, the harness called: `start_live(demand='demand', seed=1)`, `advance(seconds=1800)`.

### A. Without your tools

Tools called: `get_approach_state(intersection='Bruce B Downs & Pine', approach='SB')`. 2 turns, 1581 s. Run: `ablation/runs/without__pine_stopped.json`

> At 1800 s, there are 17 vehicles on the southbound approach of Bruce B Downs Blvd & USF Pine Dr, 16 of which are stopped. The mean speed of the vehicles on this approach is 2 mph.

### B. Your tools, plain

Tools called: `get_approach_state(intersection='Bruce B Downs & Pine', approach='SB')`. 2 turns, 1849 s. Run: `ablation/runs/plain__pine_stopped.json`

> At 1800 s, there are 17 vehicles on the southbound approach of Bruce B Downs Blvd & USF Pine Dr, 16 of which are stopped. The mean speed of the vehicles on this approach is 2 mph.

### C. Your tools as written

Tools called: `get_approach_state(intersection='Bruce B Downs & Pine', approach='SB')`. 2 turns, 2146 s. Run: `ablation/runs/full__pine_stopped.json`

> At 1800 s, on the southbound approach of Bruce B Downs Blvd & USF Pine Dr:
>
> - **Number of vehicles on the approach**: 17
> - **Number of stopped vehicles**: 16
> - **Mean speed of vehicles**: 2 mph
>
> The space-mean speed is 2 mph, and the queue fills 34% of the storage, indicating no spillback.
