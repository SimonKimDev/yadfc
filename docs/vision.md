# Vision

## In one sentence

YADFC is a **large-scale agent simulation of a small city**, where economy and society come
out of thousands of individual citizens making simple decisions. Eventually it will be a game.

## Why

- **Fun first.** It's a long-term hobby project for the members of Studio IndigoBlue.
- **Learning Rust.** The project is a good fit for Rust: lots of data, a need for
  performance, and long-lived state that has to be correct.
- **Deep CS territory.** Pathfinding, economics, scheduling, data-oriented design,
  determinism, parallelism, and profiling all come up naturally.

## Inspirations

- **Dwarf Fortress**: deep simulation, emergent stories, and a "free forever" ethos
- **Songs of Syx**: very large populations and the city-scale economy
- **RimWorld / Banished / Anno**: needs-driven colonists, production chains

## Principles

1. **Simulation before game.** If the sim isn't interesting without graphics, adding
   graphics won't fix it.
2. **Emergence over scripting.** Citizens follow simple local rules. We don't hard-code
   city-level outcomes like prices, crime rates, or famines.
3. **One system at a time.** Every new system (jobs, housing, crime, …) should be small,
   observable, and testable on its own before the next one is added.
4. **Scale matters.** Start with about 1,000 citizens and design data layouts that can grow
   to tens of thousands.
5. **Determinism.** The same seed and the same inputs should give the same city. This makes
   debugging, testing, and replays possible.
6. **Observable.** Every system should be easy to inspect through stats, logs, and dumps.
   We can't tune what we can't see.

## Non-goals

- Making money: YADFC is and will stay free
- Deadlines or a release schedule
- Graphics or UI polish before the simulation core is working
- Copying Dwarf Fortress or Songs of Syx feature for feature: they're inspirations, not specs

## Team

Studio IndigoBlue: a small group of friends building something for fun.
