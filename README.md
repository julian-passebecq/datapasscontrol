# Datapass Control

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

- **This repo is authoritative for portfolio/product boundaries and intended ownership.**
- **Each product repository is authoritative for what is actually implemented and tested.**
- A target listed here must never be reported as already implemented unless the corresponding code repository proves it.
- Existing donor code may be reused or extracted, but must not be silently treated as part of another product until integrated there.

## Product family

| Product | Primary job | Unit of work | Important runtime boundary |
|---|---|---|---|
| **Datapass** | Data-engineering coding/interview practice | Question / algorithm / notebook cell | Thin PySpark and Airflow coding surfaces only |
| **Zilla / CaseLab** | Realistic DE take-homes and multi-step cases | Assignment / case | Deep Spark and Airflow teaching/simulation |
| **Fabric Factory Lab** | Visual pipeline and Data Factory learning | Pipeline / activity / data flow | Fabric semantics over Duckle/DuckDB/DuckLake where proven |
| **Contoso Data Studio** | Build and inspect a realistic local data platform | Dataset / lakehouse / warehouse model | DuckLake + real dbt + dimensional analytics |

The intended progression is:

```text
Datapass
  coding drills
      ↓
Zilla / CaseLab
  multi-step technical assignments
      ↓
Fabric Factory Lab
  visual orchestration and data movement
      ↓
Contoso Data Studio
  complete local data platform
```

The products share ideas and selected engines, but should not collapse into one giant application.

## Important FactoryLab decision

Duckle (`slothflowlabs/duckle`) is now the primary candidate for FactoryLab's lower execution layer. It already provides a React Flow visual pipeline, DuckDB execution, DuckLake support, generated SQL, previews, per-node evidence, lineage, scheduling, run history, control-flow nodes and headless execution.

FactoryLab should therefore **spike Duckle integration before writing a new generic executor**. The preferred direction is:

```text
Fabric/ADF learning UI
        ↓
fastapi-fabric
Fabric semantics / validation / translation
        ↓
Duckle pipeline JSON / runner / server
        ↓
DuckDB / DuckLake
```

See `control/decisions/duckle-factorylab.json`.

Airflow remains a separate semantic domain: Datapass may offer a thin code→DAG scratchpad, while CaseLab owns deep Airflow scheduler/retry/trigger-rule teaching. FactoryLab may later demonstrate Airflow interoperability, but does not become the Airflow product.

## Update protocol

When an agent materially changes product scope or transfers ownership of a capability:

1. update the relevant `control/projects/<id>.json`;
2. update `control/relationships.json` or `control/shared-assets.json` only if the cross-product contract changed;
3. update a decision file when a foundational technology choice changes;
4. keep `current_state` and `target_state` separate;
5. record implementation truth in the actual application repository, not only here.

Do not store secrets, local tokens, private URLs or generated runtime credentials in this repository.
