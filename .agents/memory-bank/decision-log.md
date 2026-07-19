# Decision Log

## 2026-07-19 — Phase 1 Week 1 Plan Created (Analysis & Design)

### Context
After HITL approval and merge of Assignment-002 v2.0 (10 members, 260h, 8 weeks), Phase 1 (Analysis & Design) execution plan for Week 1 has been created.

### Decision
Created detailed execution plan `.backlog/003-phase-1-week-1-plan.md` that outlines:
- **Analyst Agent** tasks: 4 Use Cases (UC-001 through UC-004) for RTE, LPM, Program Coordination roles + glossary updates
- **4 Human Team Members** (Kirill, Anatoli, Denis, Dima): clarifications, review, approval tasks
- **Timeline**: 5-day week (Mon–Fri) with HITL Gate #1 (UC Review & Approval) on Friday
- **Deliverables**: UC files, updated glossary, summary report ready for Architect handoff

### Rationale
- Structured phase execution prevents scope creep and ensures clear hand-offs
- Agent-centric work (Analyst writes UC) + Human-in-the-loop gates (review, approval) balance automation with validation
- Parallel clarity on who does what, when, and what's expected at each step

### Files Created
- `.backlog/003-phase-1-week-1-plan.md` — detailed week 1 plan

### Files Updated
- `.agents/memory-bank/active-context.md` — updated Next Actions to point to Phase 1 Week 1

### Decision-Maker
Human (via plan approval in Claude Code).

---

## 2026-07-19 — Resource Re-Assignment: 3 New Members Onboarded, Assignment-002 Re-run

### Context
3 new team members joined (Anatoli Sanko, Dmitry Busygin, Roman Nyatin — all SAFe/Agile-coaching/RTE profiles with no technical/engineering skills). PM Agent re-ran the Greedy + Local Search algorithm (ADR-002) across all 50 WBS-002 tasks with 10 performers instead of 7.

### Decision
Retained the existing 7-member assignment as baseline (validated near-optimal per ADR-002's own local search) rather than re-deriving all 50 task scores from scratch. Re-scored and reassigned 6 tasks (26h total) from Ruslan/Denis/Kirill to Anatoli/Dmitry/Roman based on skill-category fit (SAFe Portfolio, ART Coordination, Agile Coaching) and load-balancing soft-constraint precedent already established in ADR-002 §Trade-offs.

### Rationale
- **Anatoli's SPCT-tier LPM/OKR/RTE expertise outscores incumbents** on SAFe-Portfolio-level tasks (3 score-improving moves: WBS-001 20.0>19.0, WBS-007.1 20.0>19.0, WBS-001.4 20.0>12.6). Reduces Ruslan from 100%→50% and Denis from 52.5%→35%.
- **Dmitry/Roman lack the score to outscore incumbents** but were given low-risk, non-critical-path tasks matching their profiles (RTE workflow, PM assignment map, Program coordination inception), to productively use otherwise-idle new capacity (3 onboarding moves, intentional soft-constraint trade-off per ADR-002 precedent).
- **Ilya (135% capacity, corrected) and Andrey (117% capacity) overload explicitly NOT resolved** by this re-run — none of the 3 new members carry any rating above 3/10 in Mermaid, DevOps/CI-CD, RAG/AI Engineering, Security/AppSec, or Meta-Agent Infrastructure. This is an **unresolved risk carried forward** to be addressed separately.

### Data-Quality Note
While re-summing the 50-task matrix to compute new totals, found the original assignment-002.md's summary tables (312h/292h total effort stated, per-performer totals in Performer Load Analysis) did not match the underlying 50-row task matrix. Corrected baseline: **260h true total effort** (not 312h/292h). Used corrected totals throughout the re-run; flagged for future cleanup of pre-existing typos (Kirill's printed Score 8.0 vs formula 10.4, Ruslan's WBS-007.1 printed 18.0 vs formula 19.0).

### Files Updated
- `.backlog/member-matrix-temp.md` — added Anatoli/Dmitry/Roman rows with skill ratings (0-10) and experience weights (1.3-2.0)
- `.backlog/greedy-assignment-log.md` — appended re-run section with new 10-performer starting budgets (444h total), 6-task reassignment table, data-quality notes
- `docs/architecture/adr/assignment-002.md` — v2.0: updated Task-Performer Matrix (6 rows), Performer Load Analysis (10 performers), Weekly Distribution Summary (verified row totals), Constraint Validation, Total Project Score (841.0, −6.3 points), Trade-offs; version bumped to 2.0, date added as "Re-run: 19/07/2026"
- `.agents/memory-bank/progress.md` — checked off task-resource-matching checkbox, added re-run note
- `.agents/memory-bank/active-context.md` — updated "Last Action", "Next Actions"

### Decision-Maker
PM Agent, per human-confirmed decision (full algorithmic re-run + full supporting-file consistency update via plan approval).

---

## 2026-06-29 — PM Agent WBS Preparation Workflow Created

### Context
Executing `.backlog/002-pm-agent-creation.md` - creating PM-agent workflow for WBS preparation.

### Decision
Created separate workflow file `.agents/workflows/pm-wbs-preparation.md` instead of extending existing `pm-task-resource-matching.md`.

### Rationale
- **Separation of concerns:** WBS preparation (Phase 1-5) is conceptually different from task-resource matching (Greedy + Local Search algorithm)
- **Sequential flow:** WBS must be completed and approved before resource matching begins
- **Clear handoff:** Each workflow has explicit inputs/outputs and HITL gates
- **Language compliance:** Workflow file in English (per meta-agent rules), WBS output in `.backlog/` supports Russian (per project-brief)

### WBS Scope Parameters
- **Timeline:** 8 weeks
- **Domain:** Agentic SAFe (SAFe Agentic Operating System)
- **WBS Level:** L3 (deliverables)
- **Excludes:** Already completed onboarding (`.backlog/001-fast-sdlc-onboarding.md`)

### Files Created
- `.agents/workflows/pm-wbs-preparation.md` — WBS preparation workflow

### Files Updated
- `.agents/memory-bank/progress.md` — added PM workflows to completed list
- `.agents/memory-bank/active-context.md` — will be updated after task completion

---

## 2026-06-29 — OpenCode Agent Provisioning with Redirect Files

### Context
Executing point 4 from `.backlog/001-fast-sdlc-onboarding.md` - provisioning agents in OpenCode runtime environment.

### Approach
Instead of copying full files, created redirect files that contain instructions to read source files from `/.agents/`.

### Changes Made

1. **Created `.clinerules/` directory** — container for agent rules
2. **Created `.clinerules/workflows/` directory** — container for agent workflows
3. **Deployed 6 role redirect files** in `.clinerules/`:
   - `meta-agent.md` → `/.agents/rules/meta-agent.md`
   - `analyst.md` → `/.agents/rules/analyst.md`
   - `architect.md` → `/.agents/rules/architect.md`
   - `programmer.md` → `/.agents/rules/programmer.md`
   - `qa.md` → `/.agents/rules/qa.md`
   - `fast-guardian.md` → `/.agents/rules/fast-guardian.md`

4. **Deployed 10 workflow redirect files** in `.clinerules/workflows/`:
   - `meta-agent.md` → `/.agents/workflows/meta-agent.md`
   - `meta-agent-bootstrap-workforce.md` → `/.agents/workflows/meta-agent-bootstrap-workforce.md`
   - `analyst.md` → `/.agents/workflows/analyst.md`
   - `architect.md` → `/.agents/workflows/architect.md`
   - `programmer.md` → `/.agents/workflows/programmer.md`
   - `qa.md` → `/.agents/workflows/qa.md`
   - `qa-generate-test-suite.md` → `/.agents/workflows/qa-generate-test-suite.md`
   - `qa-execute-dynamic-testing.md` → `/.agents/workflows/qa-execute-dynamic-testing.md`
   - `qa-execute-non-functional-testing.md` → `/.agents/workflows/qa-execute-non-functional-testing.md`
   - `fast-guardian-fine-tune-agent.md` → `/.agents/workflows/fast-guardian-fine-tune-agent.md`

5. **Skipped MCP configuration** — will be done later per user request

### Rationale
- **Single Source of Truth:** Changes to `/.agents/` automatically reflect in OpenCode
- **No duplication:** No need to maintain two copies of rules
- **Human-readable:** Clear instructions in each redirect file
- **Portability:** Works across machines (no absolute paths)

### Files Created
- `/.clinerules/meta-agent.md`
- `/.clinerules/analyst.md`
- `/.clinerules/architect.md`
- `/.clinerules/programmer.md`
- `/.clinerules/qa.md`
- `/.clinerules/fast-guardian.md`
- `/.clinerules/workflows/*.md` (10 files)

### Notes
- MCP provisioning skipped (user decision)
- This approach is for human readers; OpenCode will need to follow the redirects manually or we may add auto-resolution later

## 2026-06-28 — Relative Paths for Portability

### Context
Absolute paths `/Users/sincerus/Workspace/code/external/better-reality/salsa` in configuration files prevented the project from working on other machines.

### Changes Made
Replaced absolute paths with relative `./` in 3 files:
- `/opencode.json` — MCP filesystem command
- `/DEVELOPMENT.md` — documentation example
- `/.agents/mcp/mcp-settings.json` — MCP server args

### Rationale
- `./` resolves to current working directory (project root)
- Works on any machine regardless of username or path structure
- Essential for team collaboration

### Files Modified
- `/opencode.json`
- `/DEVELOPMENT.md`
- `/.agents/mcp/mcp-settings.json`
- `/.agents/memory-bank/decision-log.md` — this entry

---

## 2026-06-28 — OpenCode Configuration Fix

### Context
Build mode was showing Kimi K2.5 instead of Minimax M2.1 in sessions. Also had duplicate MCP config in `.opencode/mcp-settings.json`.

### Root Cause
- `.opencode/mcp-settings.json` was not used by OpenCode (documentation doesn't mention it)
- Global config `~/.config/opencode/opencode.jsonc` lacked `agent` section
- Missing `agent` section in global config caused model fallback issues

### Changes Made

1. **Deleted** `.opencode/mcp-settings.json` — duplicate/unused
2. **Updated** `~/.config/opencode/opencode.jsonc` — added `agent` section with defaults:
   - `plan` → kimi-k2.5
   - `build` → minimax-m2.1
3. **Strategy**: Global config provides defaults, workspace `./opencode.json` overrides them

### Files Modified
- `/.opencode/mcp-settings.json` — deleted
- `~/.config/opencode/opencode.jsonc` — added agent section

### Testing Required
- Restart VS Code completely
- Verify Build Mode shows Minimax M2.1 in session
- Check other projects still work with their own opencode.json

---

## 2026-06-28 — MCP Configuration Migration

### Context
MCP configuration was in a separate file `mcp-config.json`, but OpenCode does not support external MCP configs via `configPath`.

### Changes Made

1. **Removed section** `"mcp": { "configPath": "..." }` from `opencode.json`
2. **Added section** `"mcpServers": { "filesystem": {...} }` to `opencode.json`
3. **Deleted file** `mcp-config.json`
4. **Updated instructions** in `/.clinerules/build.md` — role-based restrictions via instructions
5. **Updated documentation** in `DEVELOPMENT.md`

### Rationale
- OpenCode uses native `mcpServers` section
- Role-based restrictions implemented through agent instructions (not technical restrictions)
- Single configuration file is easier to maintain

### Files Modified
- `/opencode.json` — added `mcpServers` section
- `/.clinerules/build.md` — added safety rules
- `/DEVELOPMENT.md` — updated documentation
- `/.agents/memory-bank/decision-log.md` — this entry
- `/mcp-config.json` — deleted

---

## 2026-06-28 — MCP Protection for Build Agent

### Context
Need to protect Build agent from dangerous operations (rm -rf, deleting critical configs).

### Solution
Implemented MCP-based filesystem access with role-based restrictions.

### Configuration

**Created `/mcp-config.json`** — visible project-level MCP config:
- Filesystem MCP server with path restrictions
- Role-based permissions for Build agent

**Updated `/.clinerules/build.md`** — MCP usage rules:
- All filesystem operations MUST go through MCP
- Allowed without confirmation: read any file, write to `/src/`, `/tests/`, `/infra/`, `/.backlog/`
- Delete without confirmation: `/src/`, `/tests/` only
- Delete with confirmation: `/.agents/`, `/.clinerules/`, `/docs/`, `/infra/`
- STRICTLY FORBIDDEN: `/.agents/memory-bank/`, `/.clinerules.backup`

**Updated `/opencode.json`** — references MCP config:
- Added `"mcp": { "configPath": "./mcp-config.json" }`

### Files
- `/mcp-config.json` — MCP configuration with agentRoles
- `/.clinerules/build.md` — updated with MCP usage rules
- `/opencode.json` — references MCP config
- `/.opencode/mcp-settings.json` — simplified

### Rationale
- Prevents accidental deletion of critical project files
- Build agent can work safely in `/src/`, `/tests/`, `/infra/`, `/.backlog/`
- Dangerous operations require explicit human confirmation
- Memory bank and backups are protected from any modification

---

## 2026-06-28 — Unified Structure: OpenCode reads Cline files

### Context
We wanted to minimize duplication between OpenCode and Cline configurations.

### Solution
OpenCode now reads files directly from `/.clinerules/` instead of maintaining separate copies in `/.agents/rules/opencode/`.

### Changes Made

1. **Updated opencode.json:**
   - Plan: `/.clinerules/plan.md`, `/.clinerules/workflows/plan.md`
   - Build: `/.clinerules/build.md`, `/.clinerules/workflows/build.md`

2. **Deleted redundant directories:**
   - `/.agents/rules/opencode/` — removed
   - `/.agents/workflows/opencode/` — removed

3. **Result:** 4 files instead of 8 (50% reduction)

### Rationale
- Both OpenCode and Cline now use the same files from `/.clinerules/`
- Less maintenance, no duplication
- Single source of truth for Plan/Build agents

---

## 2026-06-28 — Native OpenCode Agents Structure

### Context
Needed to create unified agent structure for OpenCode (Plan/Build modes) and Cline with canonical sources in `/.agents/`.

### Solution

#### Adapter Structure
Created subdirectory `/.agents/rules/opencode/` with adapters:
- `plan.md` — adapter for OpenCode Plan Mode (based on meta-agent)
- `build.md` — adapter for OpenCode Build Mode (based on programmer)

Similarly for workflows: `/.agents/workflows/opencode/`

#### OpenCode Configuration
Updated `opencode.json` to load adapters in corresponding modes.

#### Cline Mirrors
Created `/.clinerules/` directory with runtime mirrors:
- `/.clinerules/plan.md` → mirror of opencode/plan.md
- `/.clinerules/build.md` → mirror of opencode/build.md
- `/.clinerules/workflows/` → workflow mirrors

Old file `.clinerules` renamed to `.clinerules.backup`.

### Files Created/Modified

**Adapters:**
- `/.agents/rules/opencode/plan.md` — Plan Mode adapter
- `/.agents/rules/opencode/build.md` — Build Mode adapter
- `/.agents/workflows/opencode/plan.md` — Plan workflow
- `/.agents/workflows/opencode/build.md` — Build workflow

**Cline Mirrors:**
- `/.clinerules/plan.md` — Cline mirror
- `/.clinerules/build.md` — Cline mirror
- `/.clinerules/workflows/plan.md` — Cline workflow mirror
- `/.clinerules/workflows/build.md` — Cline workflow mirror

**Config:**
- `/opencode.json` — updated configuration
- `/DEVELOPMENT.md` — documentation

**Backup:**
- `.clinerules.backup` — old file preserved

### Rationale
- OpenCode uses native Plan/Build modes
- Cline uses same structure via mirrors
- Canonical sources in `/.agents/` — single source of truth
- Adapters contain reduced versions + links to full rules

---

## 2026-06-28 — AI Model Configuration for Agents

### Context
During fast-asdlc onboarding to SALSA, we needed to define models for native OpenCode agents (plan/build).

### Options Considered

1. **Single model for all modes** (Kimi k2.5)
   - Pros: Simplicity, single context
   - Cons: Suboptimal cost and speed for routine coding

2. **Different models, global config** (`~/.config/opencode/`)
   - Pros: Works for all projects
   - Cons: Not in git, not reproducible on other machines

3. **Different models, per-workspace config** (`opencode.json`)
   - Pros: Versioned, reproducible, per-project flexibility
   - Cons: Requires creating file in each project

### Decision
Use per-workspace configuration (`opencode.json`) with separation:
- **Plan:** Kimi k2.5 (reasoning)
- **Build:** Minimax M2.1 (code)

### Rationale
- Minimax M2.1 showed good results in code generation tasks
- Separation optimizes costs (code-gen models are typically cheaper than reasoning)
- Per-workspace config ensures reproducibility for the team

### Related Files
- `/opencode.json` — Configuration
- `/AGENTS.md` — Agent instructions
- `/DEVELOPMENT.md` — Setup guide for humans
- `/README.md` — Updated with link to DEVELOPMENT.md

---

## 2024-06-28 — Fast-ASDLC Onboarding Kick-off
- **Decision:** Keep project discovery Markdown-only; do not select tech stack now.
- **Rationale:** Implementation is not imminent; architecture and analysis can proceed without stack lock-in.
- **Decision-maker:** Human supervisor.

- **Decision:** All agents run inside OpenCode; no Cursor dotfiles generated for now.
- **Rationale:** Current tooling environment is VS Code + OpenCode; other participants may use own setups.
- **Decision-maker:** Human supervisor.

- **Decision:** English-only for system artifacts; Russian permitted in `.backlog/` and `docs/domain/*Interview*.md`
- **Rationale:** Aligns with team bilingual operational reality while keeping code and specs portable.
- **Decision-maker:** Human supervisor.
