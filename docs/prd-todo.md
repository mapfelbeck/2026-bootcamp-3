# Product Requirements Document (PRD) - TODO App Upgrade (Due Dates, Priority, and Filters)

## 1. Overview

We are upgrading the current TODO app (title + completed only) to make task management more practical while staying simple and teachable.

The primary user need is better day-to-day prioritization and urgency tracking. MVP will introduce due dates, priority levels, and focused filtering views without backend changes. The app will continue to use local storage only.

Scope decisions in this PRD are based on the requirements meeting and the follow-up Slack alignment, with Slack serving as final scope confirmation for MVP vs Post-MVP.

---

## 2. MVP Scope

- Add task due date field `dueDate` as optional.
- Store and process due dates in ISO format `YYYY-MM-DD`.
- Add task priority field `priority` with enum values `P1 | P2 | P3`.
- Default `priority` to `P3` when not specified.
- Add filter tabs/views: All, Today, Overdue.
- Filter behavior:
- All view includes both completed and incomplete tasks.
- Today and Overdue views include incomplete tasks only.
- Keep architecture and persistence local only (no backend API/database changes, no external storage).
- Data validation rules:
- `title` is required.
- `priority` must be one of `P1 | P2 | P3`.
- invalid `dueDate` values are ignored and treated as not set.

---

## 3. Post-MVP Scope

- Add visual highlighting for overdue tasks (for example, red treatment) so urgency stands out.
- Add deterministic list sorting in this order:
- overdue tasks first
- then by priority (`P1` before `P2` before `P3`)
- then by due date ascending
- tasks without due dates last

---

## 4. Out of Scope

- Notifications/reminders.
- Recurring tasks.
- Multi-user support.
- Keyboard navigation/accessibility enhancements beyond current baseline.
- External storage or backend persistence changes.
