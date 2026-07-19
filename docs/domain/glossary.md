# SALSA Domain Glossary — Ubiquitous Language

> **Purpose:** Single source of truth for domain terms used across Use Cases, specs, and agent artifacts.
> **Author:** Analyst Agent
> **Date:** 2026-07-19
> **Status:** ⬜ Draft — Awaiting HITL Gate #1
> **Scope (this iteration):** Terms introduced by UC-001–UC-004 (RTE & LPM agents). Expanded each analysis cycle.

All terms are English-only per `project-brief.md` language policy. Each term lists: **Definition**, **Context/Usage**, **Related terms**.

---

## A

### Agile Release Train (ART)
- **Definition:** A long-lived team-of-teams that plans, commits, and delivers value together on a common cadence (the Program Increment).
- **Context/Usage:** The scope the RTE Agent coordinates. All cross-team dependency management in [[UC-002-RTE-PI-Planning-Workflow]] happens within one ART.
- **Related:** Release Train Engineer, Program Increment, Program Board.

### Acceptance Criteria
- **Definition:** The concrete, testable conditions under which a deliverable is considered done and correct, preferably expressed as Given/When/Then.
- **Context/Usage:** Every Use Case in `/docs/domain/usecases/` ends with Acceptance Criteria; the QA Agent later checks the architecture against them.
- **Related:** Definition of Ready, Definition of Done.

---

## B

### Backlog Bus
- **Definition:** The cross-agent task-handoff mechanism realized through tracking files in `.backlog/`, where each agent appends links to the artifacts it produced.
- **Context/Usage:** The RTE Agent publishes committed PI artifacts to the Backlog Bus for downstream agents (UC-002, AC-7).
- **Related:** Hand-off Delay, Traceability.

### Budget Guardrail
- **Definition:** A pre-approved constraint on how portfolio budget may be spent (e.g., a maximum percentage of investment allowed in a given Investment Horizon or Strategic Theme).
- **Context/Usage:** The LPM Agent monitors the portfolio for Guardrail breaches and escalates them; it never changes a Guardrail itself ([[UC-003-LPM-Role-Identity]], [[UC-004-LPM-Strategic-Themes]]).
- **Related:** Lean Portfolio Management, Investment Horizon, Strategic Theme.

---

## D

### Definition of Ready (DoR)
- **Definition:** The checklist a backlog item must satisfy before it can be committed into a Program Increment.
- **Context/Usage:** In UC-002, the RTE Agent excludes Features that fail the Definition of Ready from the committed plan and lists the missing criteria (AC-5).
- **Related:** Feature, Acceptance Criteria.

### Dependency (Cross-Team)
- **Definition:** A relationship where a work item owned by one team cannot be completed without an output from another team.
- **Context/Usage:** The RTE Agent detects, lists, and visualizes cross-team dependencies on the Program Board (UC-002, AC-3); circular dependencies are escalated, never auto-resolved (AC-6).
- **Related:** Program Board, Program Increment, Enabler.

---

## E

### Enabler
- **Definition:** A piece of work that supports future business functionality (e.g., architectural runway, infrastructure) rather than delivering direct end-user value.
- **Context/Usage:** A common source of cross-team dependencies surfaced during PI Planning (UC-002).
- **Related:** Dependency, Feature.

### Epic
- **Definition:** A significant portfolio-level initiative, described as an MD-file, that requires a Lean Business Case and is realized through multiple Features.
- **Context/Usage:** The unit the LPM Agent assesses for Strategic Theme alignment and Investment Horizon classification (UC-004).
- **Related:** Lean Business Case, Strategic Theme, Investment Horizon, WSJF.

### Epic Owner Agent
- **Definition:** The AI role that analyzes market data, assembles the Lean Business Case, and computes projected WSJF for an epic.
- **Context/Usage:** Upstream supplier of epics and Lean Business Cases consumed by the LPM Agent (UC-004) and the RTE Agent (UC-002).
- **Related:** Lean Business Case, WSJF, LPM Agent.

---

## F

### Feature
- **Definition:** A service or capability, sized to fit within a single Program Increment, that delivers business value and is decomposed into stories.
- **Context/Usage:** The unit the RTE Agent maps to teams and iterations during PI Planning (UC-002).
- **Related:** Program Increment, Definition of Ready, Story.

---

## H

### Hand-off Delay
- **Definition:** Wait time introduced when work (and its context) is passed between roles or levels in SAFe — the primary source of latency the SAFe AOS aims to eliminate.
- **Context/Usage:** The motivation for the RTE Agent and the Backlog Bus: instant context transfer between levels.
- **Related:** Backlog Bus, Agentic Flow.

### Human-in-the-Loop (HITL)
- **Definition:** The governance principle that a human makes and approves every key decision; agents prepare, recommend, and record but do not decide autonomously on scope, budget, or commitments.
- **Context/Usage:** Enforced across all four use cases — the RTE Agent never self-commits PI scope; the LPM Agent never reallocates budget.
- **Related:** Authority Scope, Escalation.

---

## I

### Investment Horizon
- **Definition:** A time/maturity classification of portfolio investment (commonly: Horizon 1 = maintain/now, Horizon 2 = emerging, Horizon 3 = future bets) used to balance short-term delivery against long-term innovation.
- **Context/Usage:** The LPM Agent classifies each epic by horizon and reports the investment distribution against Guardrails (UC-004, AC-2).
- **Related:** Strategic Theme, Budget Guardrail, Lean Portfolio Management.

---

## L

### Lean Business Case (LBC)
- **Definition:** A lightweight, structured justification for an epic covering the problem, proposed solution, expected outcomes, and cost — enough to make a go/no-go investment decision without heavy documentation.
- **Context/Usage:** Produced by the Epic Owner Agent; referenced by the LPM Agent when assessing portfolio alignment.
- **Related:** Epic, WSJF, Epic Owner Agent.

### Lean Portfolio Management (LPM)
- **Definition:** The function that aligns strategy and execution by governing portfolio budgets, Strategic Themes, and Investment Horizons with minimal overhead.
- **Context/Usage:** The human function the LPM Agent augments ([[UC-003-LPM-Role-Identity]]).
- **Related:** LPM Agent, Strategic Theme, Budget Guardrail, Investment Horizon.

### LPM Agent
- **Definition:** The AI role that monitors epics for Strategic Theme alignment and Investment Horizon distribution, enforces budget Guardrails by surfacing breaches, and recommends corrections.
- **Context/Usage:** Defined in [[UC-003-LPM-Role-Identity]]; its monitoring workflow is [[UC-004-LPM-Strategic-Themes]].
- **Related:** Lean Portfolio Management, Strategic Theme, Investment Horizon, Budget Guardrail.

---

## M

### Meta-Agent
- **Definition:** The central governance agent that generates and maintains the rules, workflows, and skills of all other agents and enforces compliance with SAFe principles and company standards.
- **Context/Usage:** Instantiates the RTE Agent (UC-001) and the LPM Agent (UC-003).
- **Related:** Built-in Quality, Compliance.

### Mermaid.js
- **Definition:** A text-based diagramming syntax (stored in Markdown) that both humans and AI agents can read and generate, used as the canonical visualization format in the SALSA repository.
- **Context/Usage:** The Program Board (UC-002) and the horizon/theme distribution report (UC-004) are rendered as Mermaid.js.
- **Related:** Program Board, Single Source of Truth.

---

## P

### PI Planning
- **Definition:** The cadence-based event where the teams of an ART align on a shared plan and commit to objectives for the next Program Increment.
- **Context/Usage:** Facilitated virtually by the RTE Agent, which drafts the agenda, plan, and Program Board (UC-002).
- **Related:** Program Increment, Program Board, Release Train Engineer.

### Program Board
- **Definition:** The visual artifact of PI Planning showing Features placed across teams (rows) and iterations (columns) with cross-team dependencies drawn as connecting arrows.
- **Context/Usage:** Auto-generated by the RTE Agent as Mermaid.js (UC-002, AC-2).
- **Related:** PI Planning, Dependency, Mermaid.js.

### Program Increment (PI)
- **Definition:** A fixed timebox (typically several iterations) during which an ART delivers incremental value toward its objectives.
- **Context/Usage:** The planning unit for the RTE Agent (UC-002); its boundaries are a precondition for PI Planning.
- **Related:** PI Planning, Feature, Iteration.

---

## R

### Release Train Engineer (RTE)
- **Definition:** The servant leader and chief facilitator of an ART, responsible for coordinating PI Planning, managing dependencies and risks, and driving relentless improvement.
- **Context/Usage:** The human role the RTE Agent augments ([[UC-001-RTE-Role-Identity]]).
- **Related:** RTE Agent, ART, PI Planning.

### RTE Agent
- **Definition:** The AI role that facilitates virtual PI Planning, auto-builds the Program Board, and surfaces cross-team dependencies for the human RTE to resolve.
- **Context/Usage:** Defined in [[UC-001-RTE-Role-Identity]]; its workflow is [[UC-002-RTE-PI-Planning-Workflow]].
- **Related:** Release Train Engineer, Program Board, Dependency.

---

## S

### Single Source of Truth
- **Definition:** The principle that one Git repository (Markdown + Mermaid.js) holds all process, plan, and architecture state, versioned and auditable.
- **Context/Usage:** Every agent reads inputs from and writes outputs to Git; nothing authoritative lives outside it.
- **Related:** Traceability, Framework-as-Code.

### Strategic Theme
- **Definition:** A differentiating business objective that connects the portfolio to enterprise strategy and guides investment decisions.
- **Context/Usage:** The LPM Agent assesses whether each epic advances a declared Strategic Theme and flags orphans and coverage gaps (UC-004).
- **Related:** Investment Horizon, Epic, Lean Portfolio Management.

---

## T

### Traceability
- **Definition:** The property that every decision and artifact can be followed back through Git commit history to its origin and rationale.
- **Context/Usage:** Both agents record human decisions to Git so they are auditable (UC-001 AC-4, UC-003 AC-4).
- **Related:** Single Source of Truth, Backlog Bus, Human-in-the-Loop.

---

## W

### WSJF (Weighted Shortest Job First)
- **Definition:** A prioritization model that ranks work by Cost of Delay divided by job size/duration, to maximize economic value delivered.
- **Context/Usage:** Computed by the Epic Owner Agent; referenced when the RTE Agent must choose which lower-priority Feature to defer under capacity pressure (UC-002, 5a).
- **Related:** Lean Business Case, Epic, Feature.

---

## Change Log

| Date | Terms Added | Source |
|------|-------------|--------|
| 2026-07-19 | 26 terms (ART, RTE, LPM, PI Planning, Program Board, Strategic Theme, Investment Horizon, Budget Guardrail, etc.) | UC-001–UC-004 |
