AI Automation Creation Process

Purpose

When creating any new AI automation file, agent, skill, prompt, or instruction, you must also update the related registry files so the system can discover and route tasks correctly.

Core rule:

No AI file exists unless it is registered.
No automation runs unless it has tags, triggers, owners, permissions, and fallback rules.


---

1. Standard Creation Flow

Create file
→ Add metadata block
→ Add tags
→ Define triggers
→ Define required agent
→ Define required skills
→ Define required tools
→ Define permissions
→ Define outputs
→ Define failure behavior
→ Update registry
→ Update master index
→ Add test/eval entry


---

2. Required Updates by File Type

Created File Type	Must Update

- Agent	```AGENT_REGISTRY.md, AGENT_ROUTING_RULES.md, PERMISSION_MATRIX.md```
- Skill	```SKILL_REGISTRY.md, agent skills.md, SKILL_PERMISSION_MATRIX.md```
- Instruction ```INSTRUCTION_REGISTRY.md, related agent/workflow file```
Prompt	PROMPT_REGISTRY.md, related skill or agent
Automation	AUTOMATION_REGISTRY.md, AUTOMATION_TRIGGERS.md, WORKFLOW_REGISTRY.md
Hook	HOOK_REGISTRY.md, AUTOMATION_REGISTRY.md
Workflow	WORKFLOW_REGISTRY.md, WORKFLOW_STATE_MACHINE.md
Tool	TOOL_REGISTRY.md, TOOL_PERMISSION_MATRIX.md, related agent tools.md
MCP Server	MCP_SERVER_REGISTRY.md, MCP_TOOL_REGISTRY.md
Knowledge Source	KNOWLEDGE_REGISTRY.md, RAG_PIPELINE.md
Memory Rule	MEMORY_SYSTEM.md, MEMORY_RETENTION_POLICY.md



---

3. Required Metadata Block

Every AI-related file should start with this:

---
id: ai-file-id
type: agent | skill | instruction | prompt | automation | hook | workflow | tool | knowledge
name: human-readable-name
status: draft | active | deprecated | archived
version: 0.1.0
owner: owner-name
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags:
  - tag-one
  - tag-two
domains:
  - frontend
  - backend
  - docs
  - release
triggers:
  - manual
  - event
  - scheduled
requires:
  agents: []
  skills: []
  tools: []
  instructions: []
outputs:
  - markdown
  - json
  - task
permissions:
  read: []
  write: []
  execute: []
human_review_required: true
fallback: fallback-name
audit_required: true
---


---

4. Example: Markdown Formatting Agent

Step A — Create Agent Folder

/agents/markdown-formatting-agent
  AGENT.md
  instructions.md
  skills.md
  tools.md
  workflows.md
  examples.md


---

Step B — Create AGENT.md

---
id: agent.markdown-formatting
type: agent
name: Markdown Formatting Agent
status: active
version: 0.1.0
owner: ai-system
created: 2026-05-13
updated: 2026-05-13
tags:
  - markdown
  - formatting
  - documentation
  - cleanup
  - docs-quality
domains:
  - docs
  - content
  - publishing
triggers:
  - manual
  - doc.created
  - doc.updated
  - workflow.documentation.review
requires:
  agents: []
  skills:
    - skill.markdown-cleanup
    - skill.structure-validation
    - skill.link-validation
  tools:
    - tool.filesystem
    - tool.markdown-parser
  instructions:
    - instruction.docs-formatting
    - instruction.markdown-style
outputs:
  - formatted-markdown
  - validation-report
permissions:
  read:
    - docs
    - knowledge.reference
  write:
    - docs.draft
  execute:
    - markdown.parse
    - markdown.format
human_review_required: true
fallback: agent.docs-agent
audit_required: true
---

# Markdown Formatting Agent

## Purpose
Formats, cleans, validates, and standardizes markdown documents.

## Responsibilities
- Normalize headings
- Fix spacing
- Validate links
- Clean lists and tables
- Apply documentation style rules
- Generate formatting report

## Not Allowed
- Delete source documents
- Publish directly to production
- Modify legal/security docs without approval


---

Step C — Create instructions.md

# Markdown Formatting Agent Instructions

## Formatting Rules
- Use valid markdown.
- Preserve original meaning.
- Do not remove required sections.
- Do not invent unsupported content.
- Keep heading hierarchy logical.
- Convert inconsistent lists into clean markdown lists.
- Preserve code blocks exactly unless formatting is requested.

## Review Rules
Human review is required before replacing published docs.


---

Step D — Create skills.md

# Skills Used

| Skill | Purpose | Required |
|---|---|---|
| `skill.markdown-cleanup` | Clean markdown formatting | Yes |
| `skill.structure-validation` | Validate heading hierarchy | Yes |
| `skill.link-validation` | Check links | Optional |


---

5. Update Agent Registry

Add to:

/agents/AGENT_REGISTRY.md

| ID | Name | Status | Tags | Domains | Skills | Human Review |
|---|---|---|---|---|---|---|
| `agent.markdown-formatting` | Markdown Formatting Agent | active | markdown, formatting, documentation, cleanup | docs, content | markdown-cleanup, structure-validation, link-validation | Yes |


---

6. Update Agent Routing Rules

Add to:

/agents/AGENT_ROUTING_RULES.md

- route_id: route.markdown-formatting
  match:
    tags:
      - markdown
      - formatting
      - docs-quality
    intents:
      - format markdown
      - clean markdown
      - validate documentation
      - fix document structure
  agent: agent.markdown-formatting
  priority: 80
  fallback: agent.docs-agent


---

7. Create Required Skills

Example:

/skills/markdown-cleanup/SKILL.md

---
id: skill.markdown-cleanup
type: skill
name: Markdown Cleanup
status: active
version: 0.1.0
tags:
  - markdown
  - formatting
  - cleanup
  - documentation
inputs:
  - markdown_document
outputs:
  - formatted_markdown
  - change_summary
permissions:
  read:
    - docs
  write:
    - docs.draft
human_review_required: false
audit_required: true
---

# Markdown Cleanup Skill

## Purpose
Clean and normalize markdown formatting.

## Procedure
1. Parse markdown.
2. Preserve semantic meaning.
3. Normalize headings.
4. Normalize spacing.
5. Normalize lists.
6. Preserve code blocks.
7. Return cleaned markdown plus change summary.


---

8. Update Skill Registry

Add to:

/skills/SKILL_REGISTRY.md

| ID | Name | Status | Tags | Inputs | Outputs | Used By |
|---|---|---|---|---|---|---|
| `skill.markdown-cleanup` | Markdown Cleanup | active | markdown, formatting, cleanup | markdown_document | formatted_markdown, change_summary | agent.markdown-formatting |


---

9. Create Automation File

Example:

/automation/rules/markdown-formatting.rule.yml

id: automation.markdown-formatting
type: automation
name: Markdown Formatting Automation
status: active
version: 0.1.0
tags:
  - markdown
  - docs
  - formatting
  - automation
trigger:
  events:
    - doc.created
    - doc.updated
    - workflow.documentation.review
conditions:
  - file_extension: ".md"
  - status_not: "published"
workflow: workflow.documentation-formatting
agent: agent.markdown-formatting
skills:
  - skill.markdown-cleanup
  - skill.structure-validation
tools:
  - tool.filesystem
outputs:
  - formatted_markdown
  - formatting_report
permissions:
  read:
    - docs
  write:
    - docs.draft
requires_human_review: true
fallback:
  agent: agent.docs-agent
  behavior: create_review_task
audit:
  required: true
  log_to: observability/automation-runs


---

10. Update Automation Registry

Add to:

/automation/AUTOMATION_REGISTRY.md

| ID | Name | Trigger | Agent | Skills | Status | Review |
|---|---|---|---|---|---|---|
| `automation.markdown-formatting` | Markdown Formatting Automation | doc.created, doc.updated | agent.markdown-formatting | markdown-cleanup, structure-validation | active | Required |


---

11. Update Workflow Registry

Add to:

/workflows/WORKFLOW_REGISTRY.md

| ID | Name | Trigger | Agent | Output | Status |
|---|---|---|---|---|---|
| `workflow.documentation-formatting` | Documentation Formatting Workflow | doc.created, doc.updated | agent.markdown-formatting | formatted markdown + report | active |


---

12. Add Workflow Definition

/workflows/documentation-formatting.workflow.md

---
id: workflow.documentation-formatting
type: workflow
name: Documentation Formatting Workflow
status: active
tags:
  - docs
  - markdown
  - formatting
trigger:
  - doc.created
  - doc.updated
agent: agent.markdown-formatting
skills:
  - skill.markdown-cleanup
  - skill.structure-validation
human_review_required: true
audit_required: true
---

# Documentation Formatting Workflow

## Flow
1. Detect markdown document.
2. Load markdown formatting agent.
3. Inject formatting instructions.
4. Run markdown cleanup skill.
5. Run structure validation skill.
6. Produce formatted draft.
7. Generate change report.
8. Send to human review.
9. Log execution.


---

13. Update Master Files

Update these:

AI_MASTER_INDEX.md
AGENT_REGISTRY.md
SKILL_REGISTRY.md
AUTOMATION_REGISTRY.md
WORKFLOW_REGISTRY.md
INSTRUCTION_REGISTRY.md
TOOL_REGISTRY.md
OBSERVABILITY_INDEX.md

Minimum entry:

## Markdown Formatting System

Tags: `markdown`, `formatting`, `docs`, `cleanup`

Files:
- `/agents/markdown-formatting-agent/AGENT.md`
- `/skills/markdown-cleanup/SKILL.md`
- `/automation/rules/markdown-formatting.rule.yml`
- `/workflows/documentation-formatting.workflow.md`

Primary agent:
- `agent.markdown-formatting`

Primary skills:
- `skill.markdown-cleanup`
- `skill.structure-validation`

Human review:
- Required before published docs are changed.


---

14. Required Tags

Use consistent tags.

Domain Tags

frontend
backend
database
docs
security
release
support
analytics
product
operations

Capability Tags

formatting
summarization
classification
validation
generation
routing
search
metadata
analysis
reporting

Trigger Tags

manual
event-driven
scheduled
threshold
webhook
status-change

Risk Tags

safe-read
draft-write
production-write
destructive
approval-required
security-sensitive


---

15. Final Checklist

Before any AI automation is complete:

- [ ] File created in correct folder
- [ ] Metadata block added
- [ ] Tags added
- [ ] Trigger defined
- [ ] Agent assigned
- [ ] Skills assigned
- [ ] Tools assigned
- [ ] Permissions defined
- [ ] Human review rule defined
- [ ] Fallback defined
- [ ] Audit logging defined
- [ ] Registry updated
- [ ] Master index updated
- [ ] Workflow updated
- [ ] Eval/test entry added


---

16. Simple Rule

When adding anything AI-related:

Create the file.
Register the file.
Tag the file.
Route the file.
Govern the file.
Log the file.
Test the file.

That makes agents able to discover and use the correct files for the correct task.
