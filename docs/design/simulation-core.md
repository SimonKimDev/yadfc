# Simulation core

> Status: **draft**. This is the starting model, not a final design.

## Scope

This doc covers the headless simulation loop and the basic citizen model, the part that
everything else builds on. Rendering, input, and persistence are out of scope.

## World

- The world is a discrete 2D tile grid. Early phases can begin with an abstract
  "locations" graph and add the grid later.
- Simulation time moves forward in fixed **ticks**. One tick stands for a fixed span of
  in-game time (to be tuned).
- The world owns all state: citizens, buildings, items, and markets. Systems read and write
  that state on each tick.

## Citizen

Starting target: **about 1,000 citizens**.

```
Citizen
├── hunger        # rises over time; starvation when it hits the max
├── home          # optional reference to a dwelling
├── job           # optional reference to an employer/workplace
├── wealth        # money (integer units)
├── family        # links to other citizens
└── current task  # what the citizen is doing right now
```

More attributes come with later systems: health (disease), social class, reputation (crime),
opinions (politics), and so on.

## Tick loop

On each tick, roughly in this order:

1. **Update needs.** Needs decay or grow over time (for example, hunger goes up).
2. **Decide.** Citizens whose current task is finished, or who face an urgent need, choose
   a new task.
3. **Act.** Run current tasks: move, work, buy, eat, sleep, and so on.
4. **Resolve world systems.** Production, markets, and consequences such as starvation or
   death.
5. **Record stats.** Collect aggregate metrics to observe and debug the run.

## Decision flow (first need: food)

```
Need food
   ↓
Find food
   ↓
Can afford?
 ├─ yes → buy
 └─ no  → seek work / steal / starve
```

- **Find food:** the nearest or cheapest source that is known or reachable.
- **Afford:** compare wealth with the current price.
- **No money:** pick between working, stealing, and going hungry based on the
  citizen's traits and circumstances. This is where crime first appears.

If this works, an economy should **emerge** from many such decisions instead of being
scripted.

## Performance notes

- Prefer data-oriented layouts (struct-of-arrays / ECS-style) over object graphs full of
  `Rc<RefCell<…>>`.
- Keep the core single-threaded and deterministic first. Add parallelism later where it's
  safe (for example, per-citizen decisions that only read shared state).
- Benchmark tick time against citizen count from the start.

## Open questions

- Should the core use an ECS? Options include Bevy ECS on its own, `hecs`, a custom one, or
  plain `Vec`s.
- How long is a tick in game time, and how many ticks per second when running headless?
- Use a utility-AI style decision model, or simple priority rules at first?
- Should citizens only know about places they've seen (local knowledge), or should they
  know the whole city?
- How do we guarantee determinism? (Fixed-point vs. floats, RNG strategy, iteration order.)
- What format should save files use?
