# Copilot and Agent Automation Governance

## Purpose

Define mandatory governance for Copilot/agent automation so automation remains controlled, reviewable, and safe.

## Governance scope

- Instructions and prompts used by agents
- Agent role boundaries and ownership
- Human review gates before merge/release
- Escalation behavior when automation cannot safely proceed

## 1) Instructions governance

- All instruction files must be explicit, versioned, and attributable to an owner.
- Instructions must define allowed and disallowed actions.
- Instructions must include output expectations and validation checks.
- Any material behavior change requires review by maintainers before adoption.

## 2) Agent roles and boundaries

- Every agent must have a named mission, scope, and owner.
- Agents must not perform actions outside declared scope.
- If a request falls outside scope, agent must stop and hand off with context.
- High-impact actions (security, destructive operations, release actions) require explicit human approval.

## 3) Review gates

- Drafting gate: generated content/config must be visible in PR changes.
- Structural gate: required metadata and required sections must be present.
- Quality gate: outputs must be actionable, non-placeholder, and consistent with repository standards.
- Safety gate: sensitive changes require maintainer review and must pass security checks.
- Merge gate: no unresolved critical review findings.

## 4) Escalation rules

- Escalate immediately when requirements conflict, are ambiguous, or imply policy violations.
- Escalate when automation cannot verify safety or correctness with high confidence.
- Escalate when privileged actions are requested without required approvals.
- Escalation note must include:
  - Blocking condition
  - Attempted path
  - Recommended next action
  - Required reviewer role

## 5) Audit and traceability

- Keep changes in version control with clear commit messages.
- Preserve decision context in docs/ADRs when governance behavior changes.
- Avoid silent policy changes; update this document and related registries together.
