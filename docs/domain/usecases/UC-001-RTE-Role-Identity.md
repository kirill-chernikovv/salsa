# UC-001: RTE Agent — Role Identity & Scope

> **Use Case ID:** UC-001
> **WBS Reference:** WBS-002.1 (RTE Agent — Role Identity, P0)
> **Domain Context:** ART / Program Coordination
> **Author:** Analyst Agent
> **Date:** 2026-07-19
> **Status:** ⬜ Draft — Awaiting HITL Gate #1
> **Related:** [[UC-002-RTE-PI-Planning-Workflow]], [[glossary]]

---

## 1. Summary

Establish the **RTE Agent** as a specialized AI role that augments the human Release Train Engineer at the ART (Agile Release Train) level. The agent's identity defines what it is authorized to do autonomously, what it must escalate to the human RTE, and the boundaries of its authority within the SAFe AOS.

---

## 2. Actors

- **Primary Actor:** Release Train Engineer (human) — owns the ART, delegates routine facilitation and artifact preparation to the agent.
- **Secondary Actor:** Meta-Agent — instantiates and configures the RTE Agent's rules, workflow, and skills.
- **Supporting Actors:** Agile Teams, Product Management Agent, System Architect Agent (consumers of RTE Agent outputs).

---

## 3. Preconditions

- The Meta-Agent Infrastructure is operational (WBS-004 complete).
- Program Coordination context is initialized (WBS-002 Inception complete).
- The ART's teams and their backlogs are represented as Markdown in the Git repository.
- `project-brief.md` domain boundaries and language policy are loaded.

---

## 4. Main Success Scenario

1. The Meta-Agent instantiates the RTE Agent with its Role Identity (authority scope, constraints, deliverables).
2. The human RTE reviews the agent's declared scope and confirms which activities are delegated.
3. The RTE Agent registers the ART's teams, their capacities, and their backlog locations from the Git repository.
4. The RTE Agent stands ready to perform delegated activities (see [[UC-002-RTE-PI-Planning-Workflow]]): facilitating PI Planning, building the Program Board, and surfacing cross-team dependencies.
5. For any decision outside its authority scope (e.g., resolving a contested dependency, changing PI scope), the RTE Agent prepares a recommendation and escalates to the human RTE for a decision (Human-in-the-Loop).
6. The human RTE decides; the RTE Agent records the decision in Git with full traceability.

---

## 5. Alternative Flows

- **5a. Incomplete team representation:** If a team's backlog or capacity is missing from Git, the RTE Agent flags the gap and requests the human RTE (or Scrum Master) to supply it before proceeding — it does NOT invent data.
- **5b. Authority boundary reached mid-task:** If the agent encounters a decision it is not authorized to make while executing a delegated activity, it pauses that activity, escalates, and continues only after the human decides.
- **5c. Conflicting standards:** If a requested action would violate a SAFe principle or a project-brief constraint, the RTE Agent refuses and cites the specific rule (Built-in Quality / compliance).

---

## 6. Postconditions

- **Success:** The RTE Agent is registered, scoped, and ready to facilitate ART-level ceremonies and artifacts. Its authority boundaries are documented and human-approved.
- **Failure:** The agent is not activated; the gap (missing precondition or unresolved scope conflict) is recorded in the active `.backlog/` task.

---

## 7. Authority Scope (What the Agent MAY Do vs MUST Escalate)

| Activity | Autonomous | Escalate to Human RTE |
|----------|:---------:|:---------------------:|
| Draft/facilitate PI Planning agenda & artifacts | ✅ | |
| Generate Program Board (Mermaid.js) | ✅ | |
| Detect and list cross-team dependencies | ✅ | |
| Prepare dependency-resolution recommendations | ✅ | |
| **Resolve a contested dependency** | | ✅ |
| **Change PI scope or commitment** | | ✅ |
| **Re-prioritize another team's backlog** | | ✅ |
| Record human decisions to Git | ✅ | |

---

## 8. Acceptance Criteria (Given / When / Then)

- **AC-1 — Scope is explicit**
  - **Given** the RTE Agent has been instantiated,
  - **When** the human RTE inspects its Role Identity,
  - **Then** every activity is unambiguously classified as either *autonomous* or *escalate-to-human*, with no undefined cases.

- **AC-2 — Escalation on out-of-scope decisions**
  - **Given** the RTE Agent is executing a delegated activity,
  - **When** it reaches a decision outside its authority scope,
  - **Then** it pauses, prepares a recommendation, and requests human sign-off before proceeding.

- **AC-3 — No fabricated data**
  - **Given** required ART data (team capacity, backlog) is missing from Git,
  - **When** the RTE Agent needs that data,
  - **Then** it flags the gap and requests it, rather than inventing values.

- **AC-4 — Traceability**
  - **Given** a human decision has been made,
  - **When** the RTE Agent records it,
  - **Then** the decision and its rationale are committed to Git and are auditable in commit history.

- **AC-5 — Compliance refusal**
  - **Given** a requested action violates a SAFe principle or project-brief constraint,
  - **When** the RTE Agent evaluates it,
  - **Then** it refuses and cites the specific violated rule.

---

## 9. Open Questions (for HITL Gate #1)

- **Q-1 (Denis):** Which dependency-resolution decisions can the agent make autonomously (if any), versus always escalate?
- **Q-2 (Denis):** Should the RTE Agent be authorized to notify teams directly, or only via the human RTE?
- **Q-3 (Dima):** What is the integration point between RTE Agent outputs and the Backlog Bus (WBS-004.3)?

---

## 10. Traceability

- **Feeds:** [[UC-002-RTE-PI-Planning-Workflow]] (the agent's core workflow)
- **Implements WBS:** WBS-002.1
- **Downstream:** Architect Agent → C4 model of Program Coordination context (WBS-002.5); Programmer → RTE Agent role file (`.agents/rules/rte.md`)
