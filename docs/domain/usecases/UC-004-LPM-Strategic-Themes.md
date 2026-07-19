# UC-004: LPM Agent — Strategic Themes & Investment Horizon Tracking

> **Use Case ID:** UC-004
> **WBS Reference:** WBS-001.4 (LPM Agent — Strategic Themes & Investment Horizon Tracking, P1)
> **Domain Context:** Lean Portfolio Orchestration
> **Author:** Analyst Agent
> **Date:** 2026-07-19
> **Status:** ⬜ Draft — Awaiting HITL Gate #1
> **Related:** [[UC-003-LPM-Role-Identity]], [[glossary]]

---

## 1. Summary

The **LPM Agent** continuously monitors the portfolio's epics against defined **Strategic Themes** and tracks the distribution of investment across **Investment Horizons**. It detects drift (epics that no longer serve a theme, or a horizon mix that breaches budget Guardrails), raises compliance findings, and recommends corrections — while human leadership makes every reallocation decision.

---

## 2. Actors

- **Primary Actor:** Lean Portfolio Management / Portfolio leadership (human) — acts on findings.
- **System:** LPM Agent — assesses alignment, tracks horizon distribution, raises findings.
- **Supporting Actors:** Epic Owner Agent (author of epic MD-files and Lean Business Cases).

---

## 3. Preconditions

- LPM Agent Role Identity is established and human-approved ([[UC-003-LPM-Role-Identity]]).
- Strategic Themes, Investment Horizons, and budget Guardrails are defined in Git.
- Epics exist as MD-files carrying theme alignment, horizon classification, and budget fields.

---

## 4. Main Success Scenario

1. The LPM Agent is triggered (on epic change, on schedule, or on human request) to assess portfolio alignment.
2. The LPM Agent reads all epic MD-files and, for each epic, evaluates **Strategic Theme alignment** (does this epic advance a declared theme?).
3. The LPM Agent classifies each epic by **Investment Horizon** (e.g., Horizon 1 = maintain/now, Horizon 2 = emerging, Horizon 3 = future bets) and computes the **current investment distribution** across horizons.
4. The LPM Agent compares the distribution and per-theme spend against the budget **Guardrails**.
5. The LPM Agent produces an **alignment report**: theme coverage, horizon distribution, and any Guardrail breaches — with a Mermaid.js visualization of the horizon/theme mix.
6. For each misalignment or breach, the LPM Agent attaches a **recommendation** (e.g., "Epic X no longer serves any theme — consider sunset"; "Horizon 3 spend exceeds the 20% Guardrail — rebalance").
7. Portfolio leadership reviews the report and decides on any reallocation.
8. The LPM Agent records the decisions to Git with full traceability.

---

## 5. Alternative Flows

- **5a. Unassessable epic:** If an epic lacks theme/horizon/budget metadata, the LPM Agent lists it as "Unassessable" with the missing fields, and excludes it from distribution math (reporting the exclusion) rather than guessing.
- **5b. Orphan epic:** If an epic aligns to no Strategic Theme, the LPM Agent flags it as an orphan and recommends review (sunset or re-align).
- **5c. Guardrail breach:** If the horizon mix or per-theme spend breaches a Guardrail, the LPM Agent raises it as a top-priority finding and escalates.
- **5d. Theme with zero coverage:** If a declared Strategic Theme has no epics serving it, the LPM Agent flags the coverage gap for leadership.

---

## 6. Postconditions

- **Success:** An alignment report (with horizon/theme visualization), a list of findings with recommendations, and any recorded human decisions exist in Git.
- **Failure:** No report is produced; the blocking gap (e.g., undefined themes/guardrails) is logged in the active `.backlog/` task.

---

## 7. Acceptance Criteria (Given / When / Then)

- **AC-1 — Theme alignment assessed per epic**
  - **Given** epics with theme metadata and a defined set of Strategic Themes,
  - **When** the LPM Agent runs,
  - **Then** every assessable epic is marked as aligned to a specific theme or flagged as an orphan.

- **AC-2 — Horizon distribution computed**
  - **Given** epics classified by Investment Horizon,
  - **When** the LPM Agent reports,
  - **Then** the report shows the percentage of investment in each horizon and renders it as a Mermaid.js diagram.

- **AC-3 — Guardrail breaches raised**
  - **Given** a defined budget Guardrail (e.g., max % per horizon or per theme),
  - **When** the current distribution breaches it,
  - **Then** the breach is raised as a finding citing the specific Guardrail and the actual vs. allowed value.

- **AC-4 — Recommendations attached**
  - **Given** a misalignment, orphan, or breach,
  - **When** the LPM Agent reports it,
  - **Then** each finding carries a concrete, actionable recommendation.

- **AC-5 — Unassessable epics are transparent**
  - **Given** an epic missing required metadata,
  - **When** the LPM Agent runs,
  - **Then** it is listed as "Unassessable" with the missing fields and excluded from distribution math, with the exclusion noted.

- **AC-6 — Human owns reallocation**
  - **Given** findings and recommendations,
  - **When** a reallocation is made,
  - **Then** it is recorded only after explicit human decision — the agent never reallocates budget itself.

- **AC-7 — Coverage gaps flagged**
  - **Given** a declared Strategic Theme with no epics serving it,
  - **When** the LPM Agent reports,
  - **Then** the zero-coverage theme is explicitly flagged.

---

## 8. Open Questions (for HITL Gate #1)

- **Q-1 (Anatoli):** What are the exact Investment Horizon definitions and the target/Guardrail percentages for each in the SALSA portfolio?
- **Q-2 (Anatoli):** What makes an epic "aligned" to a theme — a declared field, or a semantic judgment by the agent? (affects autonomy vs. escalation)
- **Q-3 (Anatoli):** What is the trigger cadence — on every epic change, scheduled, or on-demand only?
- **Q-4 (Dima):** What is the canonical schema of an epic MD-file (fields the agent depends on)?

---

## 9. Traceability

- **Depends on:** [[UC-003-LPM-Role-Identity]]
- **Implements WBS:** WBS-001.4
- **Consumes:** Epic MD-files & Lean Business Cases (Epic Owner Agent)
- **Produces:** Alignment report, horizon/theme visualization (feeds WBS-006.1 Portfolio diagrams), findings list
- **Downstream:** Architect Agent → Lean Portfolio Orchestration C4 & data-flow models
