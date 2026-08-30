## v1.5.0 — Due Date Alert

### Purpose
STEWARD now provides an in-app Focus Popup when the app/site is opened and there are unfinished tasks requiring due-date attention.

### Trigger Rules
On app startup, STEWARD scans existing task data from `steward.tasks.v1`.

The popup includes:
- every unfinished overdue task
- unfinished tasks due today
- unfinished tasks due within the next 7 calendar days

The popup excludes:
- completed tasks
- tasks without a Due Date
- tasks more than 7 days away

### Due-Date Language
- overdue: `Overdue by N days`
- today: `Due Today`
- future: `N days remaining`

The task row also shows:
- category
- priority
- Due Date in `YYYY/MM/DD`

### Focus Popup Interaction
The popup title is:
- **DUE DATE ALERT**
- *Steward what needs your attention.*

Actions:
- **View Tasks** closes the alert and switches directly to the Tasks page
- **Close** dismisses the popup

Interaction rule:
- clicking outside/backdrop does not dismiss the alert
- Escape/Cancel is intercepted and closes cleanly
- no browser/system notification permission is required

### Architecture
This is an app-internal alert only.
- no backend
- no push service
- no cloud dependency
- no notification permission
- works from existing local task data
- compatible with offline/local-first PWA behavior

### Non-Regression Rule
v1.5.0 is additive only.
No existing v1.4.1 task, date, archive, theme, backup, Journal, Reflection, Gratitude, or Morning Intention behavior was intentionally changed.

# STEWARD — Christian Daily Planner

## Project Status
- **Current version:** v1.5.0 — Due Date Alert
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
- Service-worker cache bumped to `steward-pwa-v1.5.0`.

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
- `steward-pwa-v1.5.0`

## Mandatory Documentation Synchronization Rule
`index.html` and `STEWARD_PROJECT.md` are a synchronized pair. Every meaningful update must keep both aligned, including service-worker cache/version documentation.

## Version History
### v1.5.0 — Due Date Alert
- Added startup Due Date Alert Focus Popup
- Alerts for overdue, due-today, and next-7-day unfinished tasks
- Excludes completed/no-date/far-future tasks
- Added View Tasks shortcut
- Added backdrop-safe modal behavior
- No notification permission or backend required
- Preserved all prior features and storage logic
- Bumped cache to `steward-pwa-v1.5.0`


### v1.4.1 — Task Save Hotfix
- Fixed Create Task Save button regression
- Removed obsolete `tdue` DOM reference
- Added due-date validation
- Preserved all v1.4.0 themes and planner data
- Bumped cache to `steward-pwa-v1.5.0`

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
