# Data Pipeline Failure RCA Agent

    An evidence-first root-cause-analysis agent for Airflow, dbt, Spark, Databricks and cloud data-pipeline failures, with safe remediation planning and human approval gates.

    ## Why this exists

    Diagnose failed or degraded data pipelines by collecting evidence, forming competing hypotheses, ranking likely root causes, estimating blast radius, and generating safe remediation and verification plans.

    This repository is intentionally scaffolded as a **production-oriented agent project**, not a prompt-only demo. It starts with a deterministic mock provider so the complete orchestration path can be executed locally before adding any commercial LLM.

    ## Core workflow

    ingest_incident_context -> normalize_logs_and_events -> extract_error_signatures -> generate_competing_hypotheses -> collect_supporting_and_disconfirming_evidence -> rank_root_causes -> estimate_blast_radius -> propose_remediation -> generate_validation_and_rollback_plan

    ## Specialized agents

    - `incident_intake`
- `log_analyst`
- `change_correlator`
- `lineage_analyst`
- `rca_reasoner`
- `remediation_planner`
- `verification_agent`

    ## Planned tool adapters

    - `log_reader`
- `orchestrator_adapter`
- `git_diff_reader`
- `lineage_reader`
- `metric_reader`
- `sql_explainer`

    ## Quick start

    ```bash
    python3 -m venv .venv
    source .venv/bin/activate
    pip install -e ".[dev]"
    data-pipeline-failure-rca run examples/sample_input.json --output out/result.json
    pytest
    ```

    Or:

    ```bash
    make setup
    make demo
    make test
    ```

    ## Safety defaults

    - Mock/dry-run behavior is the default.
    - External systems are accessed only through explicit adapters.
    - No production mutation should be added without an approval gate.
    - Facts, assumptions, hypotheses and recommendations should remain distinguishable in outputs.
    - Credentials must come from environment/secret stores, never source control.

    ## Codex implementation guide

    Start with [`SKILL.md`](./SKILL.md). It defines the mission, architecture, implementation sequence, acceptance criteria and guardrails Codex should follow.

    ## Repository layout

    ```text
    .
    ├── AGENTS.md
    ├── SKILL.md
    ├── config/
    ├── docs/
    ├── evals/
    ├── examples/
    ├── kubernetes/
    ├── prompts/
    ├── scripts/
    ├── src/pipeline_rca/
    ├── terraform/
    └── tests/
    ```

    ## Current state

    **Phase 1 core.** The typed harness validates configuration and domain inputs, writes an atomic checkpoint after every stage, supports idempotent resume by run ID, and emits redacted structured logs. The default CLI stores state under `out/state/`. `make demo`, `make test`, and `make lint` verify the runnable mock-provider implementation.