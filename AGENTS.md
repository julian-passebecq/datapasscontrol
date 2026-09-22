# AGENTS.md — Datapass Control

This repository coordinates four separate products. Before editing any of them, read:

1. `control/index.json`
2. `control/projects/<product>.json`
3. `control/relationships.json`
4. `control/shared-assets.json`
5. relevant files under `control/decisions/`
6. `control/workstreams.json`

## Rules for AI agents

- Product boundaries in this repository are intentional. Do not merge the four products into one application.
- The application repositories are authoritative for implementation truth. This control repo is authoritative for intended ownership and cross-product boundaries.
- Distinguish **current_state** from **target_state**. Never report a target as already implemented.
- Reuse donor assets before deleting them from their current repository.
- Do not move a capability between products merely because its code currently lives in the wrong repository.
- Do not create a generic shared framework unless two products have already proven the same stable boundary.
- React Flow graph mechanics may be shared, but Airflow DAGs, Data Factory pipelines and Mapping Data Flows keep separate domain models.
- Never claim that a simulated Spark, Airflow, Fabric or SQL Server capability is the real external engine.
- For FactoryLab, read `control/decisions/duckle-factorylab.json` before executor work. Do not write a new generic ETL executor before the Duckle adapter/fork spike is completed.
- Duckle is not Airflow and not Microsoft Fabric. Preserve those truth boundaries.
- Airflow deep teaching ownership stays in CaseLab; FactoryLab may only add explicit interoperability later.
- A Duckle fork is not the default. Prefer documented JSON/CLI/HTTP adapter boundaries first; fork only for a measured blocker.

## Coordination protocol

Before substantial work:

1. inspect the target product repository;
2. inspect `control/workstreams.json`;
3. if useful, fill the relevant workstream's `claim` object with branch/agent/context;
4. work in the product repository, not in this control repository;
5. update the workstream status when the milestone materially changes.

Do not store secrets, session tokens or private runtime credentials here.

## Four product keys

- `datapass` — coding/interview studio
- `caselab` — take-home/case simulator
- `factorylab` — visual Data Factory learning product
- `contoso` — realistic data-platform studio
