## v1.6.0 — 365 Daily Scripture Library

### Scope
This is an additive Scripture-only update. Existing Tasks, Create Task, Due Date Alert, Today's Three, Archives, Themes, `YYYY/MM/DD` rules, JSON Backup/Restore, Journal, Prayer & Reflection, Gratitude, Morning Intention, and PWA behavior are preserved.

### 365-verse Local Library
STEWARD now creates a local library of exactly **365 English Scripture verses**.

Source:
- World English Bible (WEB)
- Public-domain Scripture text
- Seed source: public machine-readable `midvash/bible-data` WEB book files
- No API key, account, backend, token, or secret is required

The first-time seed draws from devotional-oriented books including Psalms, Proverbs, Isaiah, Matthew, John, Romans, Corinthians, Galatians, Ephesians, Philippians, Colossians, Thessalonians, Timothy, Hebrews, James, Peter, and 1 John.

Candidate verses are filtered toward practical devotional themes such as faith, hope, love, wisdom, grace, mercy, peace, prayer, trust, strength, courage, gratitude, service, rest, and guidance.

New storage key:
- `steward.scriptureLibrary.v1`

### First-seed behavior
When a device does not yet have the 365 library:
1. STEWARD immediately renders from the existing built-in 31-verse fallback so startup is never blocked.
2. While online, it retrieves public-domain WEB book data.
3. It selects 365 unique devotional verse records.
4. The 365 records are saved to localStorage.
5. Daily verse selection thereafter uses the local 365-verse library.

If first-time seeding cannot complete because the device is offline, the app continues using the existing 31-verse fallback and retries on a later online opening.

### Daily random lock
New storage key:
- `steward.dailyVerse.v1`

Rules:
- On the first opening of a new local calendar date, one verse is randomly selected.
- The selected verse is locked to that date.
- Refreshing, closing/reopening Chrome, reopening the installed PWA, navigating pages, or switching themes on the same date does not change it.
- On the next local calendar date, a new random verse is selected.
- The immediately previous verse is excluded from the next day's pool to avoid back-to-back repetition.

Conceptual state:
```json
{
  "date": "2026-08-30",
  "verse": {
    "id": "Ps.46.10",
    "ref": "Psalms 46:10",
    "text": "..."
  }
}
```

### Backup / Restore
v1.6.0 adds these optional fields to JSON backup:
- `scriptureLibrary`
- `dailyVerse`

Restore accepts them when present. Older backup files remain compatible.

### UI
No new controls are added. `VERSE FOR TODAY` keeps the existing visual design and still displays only:
- verse text
- Scripture reference

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
- **Current version:** v1.6.0 — 365 Daily Scripture Library
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
- Service-worker cache bumped to `steward-pwa-v1.6.0`.

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
- `steward-pwa-v1.6.0`

## Mandatory Documentation Synchronization Rule
`index.html` and `STEWARD_PROJECT.md` are a synchronized pair. Every meaningful update must keep both aligned, including service-worker cache/version documentation.

## Version History
### v1.6.0 — 365 Daily Scripture Library
- Added 365-verse local Scripture library
- Added first-time public-domain WEB seeding without API keys
- Added one-random-verse-per-local-date behavior
- Added same-day verse lock across refresh/reopen
- Prevented immediate consecutive-day duplicates
- Preserved existing 31-verse fallback for first-seed/offline resilience
- Added Scripture library and current Daily Verse to JSON backup/restore
- Preserved all v1.5.0 and earlier features
- Bumped cache to `steward-pwa-v1.6.0`

### v1.5.0 — Due Date Alert
- Added startup Due Date Alert Focus Popup
- Alerts for overdue, due-today, and next-7-day unfinished tasks
- Excludes completed/no-date/far-future tasks
- Added View Tasks shortcut
- Added backdrop-safe modal behavior
- No notification permission or backend required
- Preserved all prior features and storage logic
- Bumped cache to `steward-pwa-v1.6.0`


### v1.4.1 — Task Save Hotfix
- Fixed Create Task Save button regression
- Removed obsolete `tdue` DOM reference
- Added due-date validation
- Preserved all v1.4.0 themes and planner data
- Bumped cache to `steward-pwa-v1.6.0`

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
