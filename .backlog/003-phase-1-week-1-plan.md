# План Phase 1 — Неделя 1 (Analysis & Design)

> **Status:** Ready for Execution  
> **Phase:** 1 (Analysis & Design)  
> **Timeline:** Week 3 (Assignment-002 v2.0)  
> **Date Created:** 19/07/2026  
> **HITL Gate:** #1 (UC Review & Approval)

---

## 🤖 АГЕНТ 1: Analyst Agent

### Название агента
Analyst (Requirements Analyst & Domain Modeler)

### Где работает
- `/docs/domain/usecases/` — новые файлы Use Cases
- `/docs/domain/glossary.md` — обновления Ubiquitous Language

### Инструменты
- OpenCode (VS Code)
- Markdown editor
- Template: Use Case Format (Actor, Preconditions, Main Flow, Alternative Flows, Postconditions, Acceptance Criteria)

### Задачи (неделя 1)

- Прочитать WBS-002 (Program Coordination), WBS-002.1 (RTE Role), WBS-002.2 (RTE Workflow), WBS-001.3 (LPM Role), WBS-001.4 (LPM Strategic Themes) из `.backlog/wbs-002-salsa.md`
- Прочитать project-brief.md и process-overview.md для domain boundaries
- Запросить clarifying questions у Product Owner (Kirill) и LPM (Anatoli) про:
  - Точные acceptance criteria для каждого UC
  - Edge cases в PI Planning flow
  - WSJF scoring rules в Strategic Themes workflow
- Написать 4 Use Case документа:
  - `UC-001-RTE-Role-Identity.md` (RTE агент, роль и ответственности)
  - `UC-002-RTE-PI-Planning-Workflow.md` (RTE workflow: зависимости, синхронизация)
  - `UC-003-LPM-Role-Identity.md` (LPM агент, роль)
  - `UC-004-LPM-Strategic-Themes.md` (LPM: стратегические темы, инвестиционные горизонты)
- Обновить `/docs/domain/glossary.md` с новыми терминами:
  - Programmatic Integration Test (PIT)
  - Lean Business Case (LBC)
  - Weighted Shortest Job First (WSJF)
  - Strategic Theme
  - Investment Horizon
  - Program Increment (PI)
  - Release Train Engineer (RTE)
- Создать черновики UI mock descriptions в Markdown (если нужны интерфейсы для RTE/LPM workflow)

### На входе
- WBS-002-salsa.md (50 tasks, 260 hours)
- Assignment-002 v2.0 (кто какую задачу делает)
- project-brief.md, process-overview.md
- Существующий glossary.md

### На выходе
- `/docs/domain/usecases/UC-001-RTE-Role-Identity.md`
- `/docs/domain/usecases/UC-002-RTE-PI-Planning-Workflow.md`
- `/docs/domain/usecases/UC-003-LPM-Role-Identity.md`
- `/docs/domain/usecases/UC-004-LPM-Strategic-Themes.md`
- Обновленный `/docs/domain/glossary.md`
- Summary report для handoff Архитектору
- **HITL Gate #1 слайд:** Drafts ready for human review

---

## 👥 УЧАСТНИК 1: Kirill Chernikov

### Команда
Product Management (Team Level)

### Где работает
- `.backlog/` (комментарии, clarifications)
- Sync meetings (async в PR comments или meetings)

### Инструменты
- GitHub (PR review comments)
- Slack / Meeting tool для clarifications
- Acceptance Criteria template (Given/When/Then)

### Задачи (неделя 1)

- Прочитать WBS-002.3 (Product Management Agent — Role) и WBS-002.4 (Product Management — Feature-to-Story) из `.backlog/wbs-002-salsa.md`
- Ответить на Analyst clarifying questions про:
  - Какие criteria считать успехом для RTE PI Planning workflow?
  - Какой format Feature→Story decomposition?
  - Какие edge cases в Program coordination?
- Утвердить (или запросить правки) первые черновики Use Cases от Analyst (неделя 1, примерно пятница):
  - UC-001-RTE-Role-Identity.md
  - UC-002-RTE-PI-Planning-Workflow.md
  - UC-003-LPM-Role-Identity.md
  - UC-004-LPM-Strategic-Themes.md
- Добавить замечания / suggestions в PR (если Use Cases не совпадают с реальностью)

### На входе
- Черновики Use Cases от Analyst (mid-week)
- Clarifying questions от Analyst

### На выходе
- Approved / comments на UC drafts
- **HITL Gate #1 signoff:** ✅ Kirill одобрил Program-level UC, или 🔄 requested changes

---

## 👥 УЧАСТНИК 2: Anatoli Sanko

### Команда
Portfolio Management Level (LPM / SPCT)

### Где работает
- `.backlog/` (комментарии)
- WBS-001.3, WBS-001.4 задачи в Assignment-002

### Инструменты
- GitHub (PR comments)
- Markdown notes в `.backlog/`

### Задачи (неделя 1)

- Прочитать собственные assigned задачи:
  - WBS-001.3: LPM Agent — Role Identity (6h) — Дима это делает, нужна твоя input
  - WBS-001.4: LPM Agent — Strategic Themes & Investment Horizon Tracking (4h) — ты это делаешь, но нужны specifications
- Дать input Analyst про:
  - Точное определение Strategic Theme (в твоём понимании SALSA project)
  - Investment Horizon levels (какие периоды в рамках 8 недель SALSA?)
  - WSJF scoring criteria для SALSA epic
  - LPM monitoring constraints (какие budget guardrails?)
- Ответить на Dima's вопросы про LPM Agent role (когда он нужен для UC-003)
- Утвердить UC-003-LPM-Role-Identity.md и UC-004-LPM-Strategic-Themes.md от Analyst

### На входе
- Clarifying questions от Analyst / Dima
- WBS задачи твои (готовиться к неделе 4 implementation)

### На выходе
- LPM specifications для UC-003 и UC-004
- Approved UC-003 и UC-004

---

## 👥 УЧАСТНИК 3: Denis Opalinskiy

### Команда
Program Coordination (ART Level, RTE / Agile Coach)

### Где работает
- `.backlog/` (комментарии)
- WBS-002.1, WBS-002.2, WBS-002.7 задачи в Assignment-002

### Инструменты
- GitHub (PR review)
- Markdown

### Задачи (неделя 1)

- Прочитать собственные assigned задачи:
  - WBS-002.1: RTE Agent — Role Identity (6h, week 2 конец — неделя 1 это подготовка)
  - WBS-002.2: RTE Agent — Workflow (8h, week 3) — Dmitry это делает, но нужна твоя guidance
  - WBS-002.7: Program Board Mermaid Templates (8h, week 3) — ты это делаешь
- Дать Analyst input про:
  - Точное определение RTE role в SALSA framework (какие decisions RTE принимает? какие escalations?)
  - PI Planning workflow: какие artifacts нужны, какой sequence, какие зависимости между teams?
  - Program Board что именно показывает (dependency map, team topology, burndown?)
- Ответить на Dmitry's вопросы по WBS-002.2 (когда напишет draft)
- Утвердить UC-001-RTE-Role-Identity.md и UC-002-RTE-PI-Planning-Workflow.md

### На входе
- Clarifying questions от Analyst / Dmitry
- WBS-002.1, WBS-002.2, WBS-002.7 specifications

### На выходе
- RTE specifications для UC-001 и UC-002
- Approved UC-001 и UC-002
- Готовность к week 2: RTE Role Identity implementation (WBS-002.1)

---

## 👥 УЧАСТНИК 4: Dima Shapievskii

### Команда
Architecture & Security (System Architect / Enterprise Architect)

### Где работает
- `.backlog/` (комментарии)
- Читает черновики от Analyst, готовится к Architect работе (week 2)

### Инструменты
- GitHub (PR comments)

### Задачи (неделя 1)

- Прочитать черновики Use Cases от Analyst (особенно Program & Portfolio level)
- Задать Architect-level questions про:
  - Какие system integration points между Portfolio/Program/Team levels?
  - Какие data flows для Lean Business Case → PI Planning → Story decomposition?
  - Какие non-functional requirements (latency, security, scalability) для каждого UC?
- Утвердить UC-001, UC-002, UC-003, UC-004 с архитектурной точки зрения
- Подготовиться к week 2: начать C4 modeling (WBS-002.5, WBS-002.6)

### На входе
- Черновики UC от Analyst
- WBS-001.3, WBS-002.5, WBS-002.6 задачи

### На выходе
- Architecture-level comments на UC
- Approved UC (с точки зрения feasibility)
- Готовность к week 2: C4 Model writing

---

## 🎯 Итоговый Timeline (неделя 1)

### 📅 День 1–2 (Пн–Вт)
- Analyst: читает WBS, project-brief, glossary
- Все участники: читают Assignment-002 v2.0
- Analyst: готовит clarifying questions

### 📅 День 2–3 (Вт–Ср)
- Analyst: встреча с Kirill, Anatoli, Denis — отвечают на questions
- Analyst: пишет первые черновики UC-001, UC-002
- Dima: начинает читать черновики

### 📅 День 4 (Чт)
- Analyst: завершает UC-001, UC-002, UC-003, UC-004 черновики
- Analyst: обновляет glossary.md
- Открывает PR для HITL Gate #1

### 📅 День 5 (Пт)
- Kirill: review UC-001, UC-002
- Anatoli: review UC-003, UC-004
- Denis: review UC-001, UC-002
- Dima: review все UC архитектурно
- **HITL Gate #1: Approve / Request changes**

---

## 📊 Входы / Выходы (сводно)

| Роль | На входе | На выходе |
|------|----------|----------|
| **Analyst** | WBS-002, project-brief, glossary | 4 Use Case файла + обновленный glossary + PR для review |
| **Kirill (PO)** | UC черновики | Approval comments + HITL signoff |
| **Anatoli (LPM)** | UC черновики + clarifying questions | LPM specifications + approval |
| **Denis (RTE)** | UC черновики + clarifying questions | RTE specifications + approval |
| **Dima (Architect)** | UC черновики | Architecture feasibility check + approval |

---

## ✅ Контрольный список

- [ ] Analyst запущен, читает WBS-002 и project-brief
- [ ] Kirill получил clarifying questions, готов отвечать
- [ ] Anatoli получил clarifying questions, готов отвечать
- [ ] Denis получил clarifying questions, готов отвечать
- [ ] Dima на standby для архитектурного review
- [ ] PR создан в GitHub на день 4–5
- [ ] HITL Gate #1 passed — все UC одобрены

---

## 🚀 Следующие шаги (неделя 2)

После HITL Gate #1 approval:
- Architect Agent начинает C4 Modeling (WBS-002.5, WBS-002.6)
- Programmer Agent готовится к implementation (WBS-002.1, WBS-002.2)
- QA Agent готовит contract analysis tests
