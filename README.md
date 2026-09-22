# Datapass Control

Central architecture/control repository for the four related data-engineering products.

This repository is intentionally **not** an application. It is a small machine-readable control plane so ChatGPT, Codex and other agents can understand product boundaries, current assets, target ownership and cross-project dependencies before changing code.

## Read order for agents

1. `control/index.json`
2. The relevant file under `control/projects/`
3. `control/relationships.json`
4. `control/shared-assets.json`
5. The actual product repository before making implementation claims

## Source-of-truth rule

- **This repo is authoritative for portfolio/product boundaries and intended ownership.**
- **Each product repository is authoritative for what is actually implemented and tested.**
- A target listed here must never be reported as already implemented unless the corresponding code repository proves it.
- Existing donor code may be reused or extracted, but must not be silently treated as part of another product until integrated there.

## Product family

| Product | Primary job | Unit of work |
|---|---|---|
| **Datapass** | Data-engineering coding/interview practice | Question / algorithm / notebook cell |
| **Zilla / CaseLab** | Realistic DE take-homes and multi-step cases | Assignment / case |
| **Fabric Factory Lab** | Visual pipeline and Data Factory learning | Pipeline / activity / data flow |
| **Contoso Data Studio** | Build and inspect a realistic local data platform | Dataset / lakehouse / warehouse model |

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

## Update protocol

When an agent materially changes product scope or transfers ownership of a capability:

1. update the relevant `control/projects/<id>.json`;
2. update `control/relationships.json` or `control/shared-assets.json` only if the cross-product contract changed;
3. keep `current_state` and `target_state` separate;
4. record implementation truth in the actual application repository, not only here.

Do not store secrets, local tokens, private URLs or generated runtime credentials in this repository.
