# Datapass Control

> **Global constellation moved to `julian-passebecq/dataprojects`.**
>
> Read that repository first for the current six-product family, toolbox/IDE categories, ownership and portfolio status. This repository is now a **detailed sub-registry/history** for the Datapass-derived architecture and its migration decisions. If anything here conflicts with `dataprojects`, the global registry wins for product boundaries; implementation repos still win for code truth.

Central architecture/control repository for the four related data-engineering products.

This repository is intentionally **not** an application. It is a small machine-readable control plane so ChatGPT, Codex and other agents can understand product boundaries, current assets, target ownership and cross-project dependencies before changing code.

## Read order for agents

1. `control/index.json`
2. The relevant file under `control/projects/`
3. `control/relationships.json`
4. `control/shared-assets.json`
5. Relevant architecture decision under `control/decisions/`
6. `control/workstreams.json`
7. The actual product repository before making implementation claims

## Source-of-truth rule

- **Global product boundaries/categories now live in `julian-passebecq/dataprojects`.**
- This repo keeps detailed Datapass-family architecture/migration history.
- **Each product repository is authoritative for what is actually implemented and tested.**
- A target listed here must never be reported as already implemented unless the corresponding code repository proves it.
- Existing donor code may be reused or extracted, but must not be silently treated as part of another product until integrated there.

## Important historical note

The files below were created while the family had fewer explicit products. Airflow Lab and PBI / Semantic Lab have since been split into standalone products in the global `dataprojects` registry. Do not use the older product count here as the current portfolio definition.

## Important FactoryLab decision

Duckle (`slothflowlabs/duckle`) is the primary candidate for FactoryLab's lower execution layer. FactoryLab should spike Duckle integration before writing a new generic executor. See `control/decisions/duckle-factorylab.json`.

## Update protocol

When an agent changes detailed Datapass-family architecture:

1. confirm the global boundary in `julian-passebecq/dataprojects`;
2. update the relevant detailed file here only when useful;
3. keep `current_state` and `target_state` separate;
4. record implementation truth in the actual application repository.

Do not store secrets, local tokens, private URLs or generated runtime credentials in this repository.
