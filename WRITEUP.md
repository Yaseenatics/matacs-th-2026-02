# AI Proposal Triage — Design Write-up

## 1. AI vs. Rules

The system uses AI to extract structured information from proposal documents, including experience, price, timelines, warranties, and team details. Each extracted field includes supporting evidence so reviewers can verify it.

Deterministic application code validates the extracted data, checks mandatory requirements, calculates weighted scores, and generates rankings. AI does not determine eligibility or award contracts. This separation improves reliability, consistency, and explainability.

## 2. Consistency and Explainability

The system uses documented scoring formulas, fixed criterion weights, validated inputs, and deterministic calculations. Scores are calculated to full precision and rounded only for display. Each evaluation records the criteria version, extracted evidence, component scores, total score, and ranking rationale.

Identical validated inputs and criteria produce identical scores. AI extraction may vary, so uncertain or conflicting results are flagged for review before scoring. Reviewers can inspect the evidence and see how each criterion contributed to the final score.

## 3. Human Oversight and Audit

Human review occurs when mandatory evidence is missing or ambiguous, extracted information conflicts, or a proposal contains suspicious instructions. Reviewers can confirm evidence, resolve flags, request clarification, and override results with a documented reason.

The final award decision always remains with a human. Audit records include proposal identifiers, source evidence, extraction results, criteria version, scores, timestamps, reviewer actions, overrides, and the final decision.

## 4. Changing Criteria

Criteria and weights are stored as administrator-managed configuration, not hard-coded values. The system validates that mandatory checks are defined and weighted criteria total 100%.

Every criteria change creates a new version. Existing evaluations retain their original criteria and results. If proposals must be reevaluated, the system runs them against the new version and clearly identifies the updated results. This preserves auditability and prevents comparisons between incompatible scoring versions.

## 5. Risks and Safeguards

- **Incorrect extraction:** Require structured output, schema validation, source evidence, and human review of uncertain fields.
- **Fabricated information:** Score only supported, validated facts. Missing evidence is never treated as confirmed.
- **Prompt injection:** Treat proposal contents as untrusted data. Ignore embedded instructions that attempt to change criteria, scores, rankings, or system behaviour.
- **Inconsistent scoring or bias:** Use documented formulas, fixed weights, transparent evidence-based criteria, and consistent treatment of missing information.
- **Eligibility errors:** Evaluate mandatory requirements separately from weighted scoring. Flag Proposal B because the bidder's own licence is unconfirmed. Flag Proposal D because its completion timeline is unspecified.
- **Excessive AI costs:** Process each proposal once where possible, use AI only for tasks requiring document interpretation, and use ordinary code for validation and scoring.
- **Unauthorised changes or disputes:** Record criteria versions, reviewer overrides, and final decisions in an audit trail. Restrict access to administrative changes.

The system ranks only proposals with confirmed eligibility. A flagged proposal receives no rank or score until the uncertainty is resolved. The final award decision remains with the human reviewer.
