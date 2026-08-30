# STEWARD — Christian Daily Planner

## Project Status
- **Current version:** v1.4.1 — Task Save Hotfix
- **Primary platform:** Android + Google Chrome
- **Architecture:** Local-first Progressive Web App (PWA)
- **Hosting:** GitHub Pages over HTTPS

## v1.4.1 Task Save Hotfix
A regression after the `YYYY/MM/DD` date-control refactor prevented Create Task from saving.

### Root Cause
The Task Due Date UI had been migrated from the old `tdue` element to:
- `tdueText` — user-facing `YYYY/MM/DD`
- `tdueNative` — internal date picker

The Save Task handler still referenced the removed `tdue` element. Pressing Save therefore threw a JavaScript error before the task could be persisted.

### Fix
- Save Task now reads `tdueText`.
- Non-empty dates are validated as `YYYY/MM/DD`.
- Task due dates are stored internally as `YYYY-MM-DD`.
- Due Date remains optional.
- Invalid dates show a clear validation message instead of silently failing.
- After a successful save, both date controls are cleared.
- Existing tasks, archives, settings, and themes are unchanged.
- Service-worker cache bumped to `steward-pwa-v1.4.1`.

## Themes Preserved
- Royal Purple
- Calm Blue
- Hobbiton
- Rivendell
- Lothlórien
- Rohan
- Gondor
- Custom RGB

## Global Date Rule
- User-facing dates: `YYYY/MM/DD`
- Internal storage: `YYYY-MM-DD`

## LocalStorage Keys
- `steward.tasks.v1`
- `steward.journal.v1`
- `steward.gratitude.v1`
- `steward.intention.v1`
- `steward.intentions.v1`
- `steward.reflection.v1`
- `steward.reflections.v1`
- `steward.theme.v1`

## PWA
Current cache:
- `steward-pwa-v1.4.1`

## Mandatory Documentation Synchronization Rule
`index.html` and `STEWARD_PROJECT.md` are a synchronized pair. Every meaningful update must keep both aligned, including service-worker cache/version documentation.

## Version History

### v1.4.1 — Task Save Hotfix
- Fixed Create Task Save button regression
- Removed obsolete `tdue` DOM reference
- Added due-date validation
- Preserved all v1.4.0 themes and planner data
- Bumped cache to `steward-pwa-v1.4.1`

### v1.4.0 — New Theme Update
- Added Hobbiton
- Added Rivendell
- Added Lothlórien
- Added Rohan
- Added Gondor
- Preserved Royal Purple, Calm Blue, Custom RGB

### v1.3.0 — Review Complete
- Added global `YYYY/MM/DD`
- Added Journal Archive
- Added dated Reflection + Reflection Archive
- Added theme system

### v1.2.0 — Today Page Complete
- Added Saved Intentions Archive

### v1.1.0 — Today Page Update
- Added daily Scripture rotation and Save Intention

### v1.0.1 — Interaction Hotfix
- Fixed initial deployed JavaScript interaction failure

### v1.0.0 — Android PWA Prototype
- Initial installable STEWARD PWA
