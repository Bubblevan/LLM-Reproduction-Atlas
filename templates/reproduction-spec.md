# Reproduction specification template

Use one copy per future candidate. Keep scope at one mechanism and make the outcome checkable.

## Identity
- ID / topic:
- Repository:
- Status:
- Priority:
- Source path and pinned commit:
- Paper title / canonical URL:
- Upstream code / exact revision (or UNVERIFIED):

## Question
Write one question that the implementation can answer.

## Claim boundary
- What the experiment can establish:
- What it cannot establish:
- Full-paper results required? Default: no.

## Mechanism
- Formula:
- Tensor shapes and conventions:
- Assumptions:
- Known edge cases:

## Implementation plan
- Critical path to write by hand:
- Libraries/framework pieces reused:
- Optional reference implementation:
- Explicit exclusions:

## Minimal experiment
- Inputs/data:
- Baseline/control:
- Measurement:
- Expected qualitative result:
- Random seed and config:
- Compute tier and expected time label:

## Completion gate
Check the smallest relevant items:
- [ ] Formula agrees with derivation/reference.
- [ ] Shapes, masks and indexing are checked.
- [ ] Gradients are finite.
- [ ] A relevant invariant/equivalence is checked.
- [ ] Loss/metric/qualitative behavior moves as expected.
- [ ] Compute or memory tradeoff is measured when central.
- [ ] Results include config, environment and caveats.

## Risks and scope
- Likely confounders:
- Dataset/checkpoint policy:
- What would cause the result to be inconclusive:
- Do NOT do:

## Evidence
- Source paths pinned to commit:
- Paper/upstream links:
- Notes on unverified provenance:
