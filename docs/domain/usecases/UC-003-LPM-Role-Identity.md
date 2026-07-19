# UC-003: LPM Agent — Role Identity & Scope

> **Use Case ID:** UC-003
> **WBS Reference:** WBS-001.3 (LPM Agent — Role Identity, P1)
> **Domain Context:** Lean Portfolio Orchestration
> **Author:** Analyst Agent
> **Date:** 2026-07-19
> **Status:** ⬜ Draft — Awaiting HITL Gate #1
> **Related:** [[UC-004-LPM-Strategic-Themes]], [[glossary]]

---

## 1. Summary

Establish the **LPM Agent** (Lean Portfolio Management) as a specialized AI role that augments Portfolio leadership. The agent monitors the portfolio for alignment with **Strategic Themes** and **Investment Horizons**, enforces **budget Guardrails**, and prepares compliance findings — while all portfolio investment decisions remain with human leadership (Human-in-the-Loop).

---

## 2. Actors

- **Primary Actor:** Lean Portfolio Management / Portfolio leadership (human) — owns strategy, budgets, and investment decisions.
- **Secondary Actor:** Meta-Agent — instantiates and configures the LPM Agent.
- **Supporting Actors:** Epic Owner Agent (supplies Lean Business Cases & epics), RTE Agent (consumes portfolio guardrails at the ART level).

---

## 3. Preconditions

- The Meta-Agent Infrastructure is operational (WBS-004 complete).
- Portfolio Management context is initialized (WBS-001 Inception complete).
- Strategic Themes and Investment Horizons are defined and represented as Markdown in Git.
- Epics are represented as MD-files with the fields the agent must read (theme alignment, horizon, budget).

---

## 4. Main Success Scenario

1. The Meta-Agent instantiates the LPM Agent with its Role Identity (authority scope, constraints, deliverables).
2. Portfolio leadership reviews the agent's declared scope and confirms which monitoring activities are delegated.
3. The LPM Agent registers the portfolio's Strategic Themes, Investment Horizons, and budget Guardrails from Git.
4. The LPM Agent stands ready to perform delegated monitoring (see [[UC-004-LPM-Strategic-Themes]]): checking epic alignment, tracking horizon distribution, and flagging Guardrail breaches.
5. For any decision outside its authority (e.g., approving an epic's funding, changing a Guardrail), the LPM Agent prepares a finding with a recommendation and escalates to human leadership.
6. Human leadership decides; the LPM Agent records the decision to Git with full traceability.

---

## 5. Alternative Flows

- **5a. Missing epic metadata:** If an epic MD-file lacks the fields needed to assess theme/horizon/budget, the LPM Agent flags the epic as "Unassessable" and requests the missing metadata — it does not guess alignment.
- **5b. Guardrail breach detected:** If monitoring reveals a portfolio state that violates a budget Guardrail, the LPM Agent raises a compliance finding and escalates; it does not alter budgets itself.
- **5c. Conflicting strategy signals:** If two Strategic Themes appear to conflict for a given epic, the LPM Agent surfaces the conflict for human resolution rather than choosing.

---

## 6. Postconditions

- **Success:** The LPM Agent is registered, scoped, and ready to monitor portfolio alignment. Its authority boundaries are documented and human-approved.
- **Failure:** The agent is not activated; the blocking gap is recorded in the active `.backlog/` task.

---

## 7. Authority Scope (What the Agent MAY Do vs MUST Escalate)

| Activity | Autonomous | Escalate to Human |
|----------|:---------:|:-----------------:|
| Read epics and assess Strategic Theme alignment | ✅ | |
| Track Investment Horizon distribution | ✅ | |
| Detect budget Guardrail breaches | ✅ | |
| Prepare compliance findings & recommendations | ✅ | |
| **Approve / reject epic funding** | | ✅ |
| **Change a Strategic Theme or Guardrail** | | ✅ |
| **Re-allocate portfolio budget** | | ✅ |
| Record human decisions to Git | ✅ | |

---

## 8. Acceptance Criteria (Given / When / Then)

- **AC-1 — Scope is explicit**
  - **Given** the LPM Agent has been instantiated,
  - **When** Portfolio leadership inspects its Role Identity,
  - **Then** every activity is classified as either *autonomous* or *escalate-to-human*, with no undefined cases.

- **AC-2 — Monitoring, not deciding**
  - **Given** the LPM Agent detects a misalignment or Guardrail breach,
  - **When** it responds,
  - **Then** it raises a finding and escalates — it never changes budgets, themes, or funding autonomously.

- **AC-3 — No fabricated alignment**
  - **Given** an epic lacks the metadata to assess alignment,
  - **When** the LPM Agent evaluates it,
  - **Then** it marks the epic "Unassessable" and requests metadata, rather than guessing.

- **AC-4 — Traceability**
  - **Given** a human portfolio decision has been made,
  - **When** the LPM Agent records it,
  - **Then** the decision and rationale are committed to Git and auditable in commit history.

- **AC-5 — Guardrail enforcement is surfaced**
  - **Given** a portfolio state breaches a budget Guardrail,
  - **When** the LPM Agent monitors,
  - **Then** the breach is raised as a compliance finding with the specific Guardrail cited.

---

## 9. Open Questions (for HITL Gate #1)

- **Q-1 (Anatoli):** What is the canonical set of Strategic Themes and Investment Horizons for the SALSA portfolio (for the demo epic)?
- **Q-2 (Anatoli):** What budget Guardrails should the agent enforce, and at what thresholds?
- **Q-3 (Anatoli):** Which epic MD-file fields are mandatory for the agent to assess alignment?
- **Q-4 (Dima):** Is portfolio data read directly from epic MD-files, from a tracking system via MCP, or both?

---

## 10. Traceability

- **Feeds:** [[UC-004-LPM-Strategic-Themes]] (the agent's core monitoring workflow)
- **Implements WBS:** WBS-001.3
- **Downstream:** Architect Agent → C4 model of Lean Portfolio Orchestration context; Programmer → LPM Agent role file (`.agents/rules/lpm.md`)
