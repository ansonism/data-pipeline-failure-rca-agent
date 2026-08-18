# Evaluation plan

    Start with deterministic evals against the mock/fake adapters, then add provider-backed eval runs.

    Domain acceptance targets from `SKILL.md`:

    - The agent distinguishes facts, hypotheses and assumptions.
- At least one disconfirming evidence check is performed for every high-ranked hypothesis.
- Suggested production changes default to dry-run and require approval.
- Output contains a reproducible validation plan.
- Sample incidents for schema drift, authentication failure and resource exhaustion pass evals.

    Do not use an LLM judge as the sole source of truth for safety-critical or mechanically verifiable assertions.

Phase 1 eval cases are validated against the strict `EvalCase` contract. They declare required stages and findings, forbidden findings/actions, an expected risk range, and minimum evidence coverage. The suite runs deterministically with `MockProvider` and requires no network access or model judge.
