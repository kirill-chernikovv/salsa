# UC-002: RTE Agent — PI Planning & Dependency Management Workflow

> **Use Case ID:** UC-002
> **WBS Reference:** WBS-002.2 (RTE Agent — Workflow, P0)
> **Domain Context:** ART / Program Coordination
> **Author:** Analyst Agent
> **Date:** 2026-07-19
> **Status:** ⬜ Draft — Awaiting HITL Gate #1
> **Related:** [[UC-001-RTE-Role-Identity]], [[glossary]]

---

## 1. Summary

The **RTE Agent** facilitates a virtual **PI Planning** event, automatically constructs the **Program Board** as a Mermaid.js diagram, and surfaces **cross-team dependencies** — eliminating the hand-off delays that are the primary source of latency in SAFe. The human RTE retains all commitment and scope decisions (Human-in-the-Loop).

---

## 2. Actors

- **Primary Actor:** Release Train Engineer (human) — facilitates the ART, approves the plan.
- **System:** RTE Agent — prepares agenda, drafts the Program Board, detects dependencies.
- **Supporting Actors:** Agile Teams (supply capacity & candidate features), Product Management Agent (supplies prioritized features), Epic Owner Agent (supplies approved epics).

---

## 3. Preconditions

- RTE Agent Role Identity is established and human-approved ([[UC-001-RTE-Role-Identity]]).
- A prioritized set of Features is available in the Git backlog (from Product Management).
- Each participating team's capacity and velocity are represented in Git.
- The current Program Increment (PI) boundaries (start, end, iterations) are defined.

---

## 4. Main Success Scenario

1. The human RTE triggers a PI Planning cycle for the upcoming PI.
2. The RTE Agent gathers inputs from Git: prioritized Features, team capacities, and the Definition of Ready state of each candidate item.
3. The RTE Agent drafts the **PI Planning agenda** and a proposed **draft plan** — mapping candidate Features to teams and iterations within capacity.
4. The RTE Agent analyzes the draft plan and **detects cross-team dependencies** (a Feature on Team A that requires an enabler from Team B).
5. The RTE Agent generates the **Program Board** as a Mermaid.js diagram: teams × iterations, with Features placed and dependency arrows drawn between them.
6. The RTE Agent produces a **dependency list** with a recommendation for each (sequence, swap iteration, or flag as risk).
7. The human RTE reviews the draft plan, Program Board, and dependency recommendations.
8. The human RTE resolves contested dependencies and confirms the PI commitment (scope decisions remain human).
9. The RTE Agent records the committed plan, final Program Board, and decisions to Git with full traceability.
10. The RTE Agent publishes the confirmed artifacts to the Backlog Bus for downstream agents.

---

## 5. Alternative Flows

- **5a. Over-capacity plan:** If candidate Features exceed a team's capacity, the RTE Agent flags the overflow, proposes options (defer lowest-WSJF Feature, or escalate scope), and does NOT silently drop work.
- **5b. Item not Ready:** If a candidate Feature fails the Definition of Ready, the RTE Agent excludes it from the committed plan and lists it as "Not Ready" with the missing criteria.
- **5c. Circular dependency:** If dependencies form a cycle across teams, the RTE Agent highlights the cycle explicitly on the Program Board and escalates — it does not auto-resolve.
- **5d. Late input change:** If a Feature's priority changes mid-cycle, the RTE Agent recomputes the affected portion of the draft plan and notifies the human RTE of the delta.

---

## 6. Postconditions

- **Success:** A human-committed PI plan, a Program Board (Mermaid.js), and a resolved dependency list exist in Git and are published to the Backlog Bus.
- **Failure:** No commitment is recorded; blockers (over-capacity, not-Ready items, unresolved cycles) are logged in the active `.backlog/` task for follow-up.

---

## 7. Acceptance Criteria (Given / When / Then)

- **AC-1 — Draft plan within capacity**
  - **Given** team capacities and a prioritized Feature set,
  - **When** the RTE Agent produces a draft plan,
  - **Then** no team is planned above its stated capacity without an explicit over-capacity flag.

- **AC-2 — Program Board is generated and valid**
  - **Given** a draft plan exists,
  - **When** the RTE Agent generates the Program Board,
  - **Then** the output is valid Mermaid.js showing teams × iterations with all Features placed and all detected dependencies drawn as arrows.

- **AC-3 — Dependencies are surfaced, not hidden**
  - **Given** a Feature depends on another team's work,
  - **When** the RTE Agent analyzes the plan,
  - **Then** the dependency appears in both the dependency list and on the Program Board, each with a recommendation.

- **AC-4 — Human owns commitment**
  - **Given** a draft plan and dependency recommendations,
  - **When** the plan is committed,
  - **Then** the commitment is recorded only after explicit human RTE approval — the agent never self-commits scope.

- **AC-5 — Not-Ready exclusion**
  - **Given** a candidate Feature fails the Definition of Ready,
  - **When** the RTE Agent builds the committed plan,
  - **Then** that Feature is excluded and listed with the specific missing readiness criteria.

- **AC-6 — Circular dependency escalation**
  - **Given** cross-team dependencies form a cycle,
  - **When** the RTE Agent detects it,
  - **Then** the cycle is visibly flagged and escalated, never silently reordered.

- **AC-7 — Traceability & handoff**
  - **Given** a committed PI plan,
  - **When** the RTE Agent finalizes,
  - **Then** the plan, board, and decisions are committed to Git and published to the Backlog Bus for downstream agents.

---

## 8. Open Questions (for HITL Gate #1)

- **Q-1 (Denis):** What is the canonical Program Board layout (teams as rows, iterations as columns)? Any required legend/color conventions?
- **Q-2 (Denis):** Which dependency recommendations may the agent apply automatically vs. always present for human choice?
- **Q-3 (Kirill):** What is the exact Definition of Ready the agent should check Features against?
- **Q-4 (Dima):** How is the "publish to Backlog Bus" step realized as a contract (WBS-004.3)?

---

## 9. Traceability

- **Depends on:** [[UC-001-RTE-Role-Identity]]
- **Implements WBS:** WBS-002.2
- **Consumes:** Prioritized Features (Product Management Agent), approved Epics (Epic Owner Agent)
- **Produces:** PI Plan, Program Board (feeds WBS-002.7 templates & WBS-006.3 diagrams), dependency list
- **Downstream:** Architect Agent → Program Coordination C4 & sequence models
