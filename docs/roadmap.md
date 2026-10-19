# Roadmap

There are no dates and no deadlines. Phases happen roughly in order but can overlap, and
each phase should leave the simulation in a runnable, observable state.

## Phase 0: Bootstrap (in progress)

- [x] Repository, license, vision, and initial design docs
- [ ] Cargo workspace skeleton, CI (fmt, clippy, test)

## Phase 1: Headless tick simulation

- Fixed-step tick loop, seeded RNG, deterministic runs
- About 1,000 citizens with hunger, wealth, and current task
- Food sources and eating; starvation
- Stats output (population, average hunger, deaths per tick) and a tick-time benchmark

## Phase 2: Space and movement

- Tile grid world
- Pathfinding (A* first; flow fields or hierarchical search later as scale needs it)
- Citizens physically travel to food, work, and home

## Phase 3: Jobs and the job market

- Workplaces, employment, wages
- Citizens look for jobs when they run short of money

## Phase 4: Supply and demand

- Production chains (raw → processed goods)
- Markets with prices driven by supply and demand
- The "can afford?" check becomes meaningful

## Phase 5: Housing

- Dwellings, rent or ownership, homelessness
- Families sharing a home

## Phase 6: Transportation

- Roads, traffic, and travel cost affecting decisions

## Phase 7: Crime

- Stealing as an alternative to buying, guards or police, consequences

## Phase 8: Disease

- Health, contagion, sanitation, healthcare

## Phase 9: Social class

- Wealth stratification, mobility, class-based behavior

## Phase 10: Politics

- Factions, opinions, governance, unrest

## Later / someday

- Rendering and UI (watch the city, then interact with it)
- Player agency: turning the simulation into a game
- Lore: the world, its history, and its people
- Modding and save files
- Scaling to tens of thousands of citizens (parallelism, profiling)
