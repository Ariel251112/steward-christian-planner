# STEWARD — Christian Daily Planner

## Project Status
- **Current version:** v1.3.0 — Review Complete
- **Primary platform:** Android + Google Chrome
- **Architecture:** Local-first Progressive Web App (PWA)
- **Hosting:** GitHub Pages over HTTPS
- **Tagline:** *Plan with purpose. Work with faith.*

## Product Philosophy
STEWARD supports stewardship, purposeful work, prayer, reflection, gratitude, journaling, service, and healthy rest without productivity-shaming.

## Visual Identity
Default theme is **Royal Purple** with warm gold accents and subtle butterflies. v1.3.0 adds per-device theme personalization while preserving the same STEWARD design language.

### Appearance
Settings now includes:
- Royal Purple preset — default
- Calm Blue preset
- Custom color picker / RGB display
- Reset to Royal Purple
- Theme changes update the whole visual system, not only buttons
- Theme preference is stored locally as `steward.theme.v1`
- Different people/devices using the same deployed STEWARD URL can keep different themes
- Theme preference is included in JSON backup/restore

## Global Date Rule
This is a sealed global interaction rule:
- **Every user-facing date display and date-entry field must use `YYYY/MM/DD`.**
- Example: `2026/08/29`
- Internal storage keys/values may continue to use ISO `YYYY-MM-DD`.
- Browser/OS localized placeholders such as `年/月/日` must not be exposed as the STEWARD user-facing date format.

v1.3.0 applies this rule to:
- Task Due Date
- Morning Intention Archive search
- Journal date selection
- Journal Archive search
- Reflection Archive search
- Existing task/journal/archive date labels

## Today Page — Baseline
### Verse for Today
- Built-in 31-verse World English Bible (WEB, Public Domain) rotation
- Deterministic by local calendar date
- Same date = same verse
- Offline capable
- UI shows Scripture and reference only
- Source/license remains documented but is not displayed in the hero
- Double quotation issue fixed
- YouVersion integration remains a future enhancement

### Today's Three
- Shows up to three incomplete tasks selected as top priorities
- Review passed; no v1.3.0 behavior change

### Today's Tasks
- Shows all tasks, completion count, and Daily Stewardship percentage
- Review passed; no v1.3.0 behavior change

### Morning Intention
- One dated intention per day
- Explicit Save Intention
- Saved / Unsaved Changes status
- View Saved Intentions
- Archive supports `YYYY/MM/DD` date search and keyword search
- Same-day save updates that day's record
- Legacy `steward.intention.v1` safely migrates into dated archive
- Dated archive key: `steward.intentions.v1`

## Tasks Page
Purpose:
> Central task list and Add Task entry point.

Current behavior:
- My Tasks / All active tasks
- Add task
- Task name
- Purpose / Why does this matter?
- Category
- Priority
- Due Date
- Today's Three flag
- Complete/incomplete
- Delete
- Due dates display as `YYYY/MM/DD`
- Review passed; no feature expansion required in v1.3.0

## Journal
### Daily Journal
- One entry per date
- User-facing date format: `YYYY/MM/DD`
- Internal key format: `YYYY-MM-DD`
- Save Journal updates that date rather than overwriting other dates

### Journal Archive
v1.3.0 adds:
- View Journal Archive
- Exact `YYYY/MM/DD` date search
- Keyword search
- Date + keyword combined filtering
- Newest-first records
- Selecting an archive entry loads that date into the editor

Storage remains:
- `steward.journal.v1`

## Reflect
### Prayer & Reflection
v1.3.0 upgrades Reflection from a single mutable value to dated records:
- One Reflection per date
- Explicit Save Reflection
- Saved / Unsaved Changes status
- Legacy `steward.reflection.v1` safely migrates into today's dated record
- New archive key: `steward.reflections.v1`
- Legacy key remains for backward compatibility

### Gratitude
- Dated Gratitude entries remain supported
- New entries include both user-facing `YYYY/MM/DD` and internal ISO date metadata

### Reflection Archive
One combined archive searches both:
- Prayer & Reflection
- Gratitude

Supports:
- exact `YYYY/MM/DD` date search
- keyword search
- date + keyword filtering
- newest-first grouping by date

This avoids separate competing archives on the Reflect page.

## Settings
### Appearance
- Royal Purple
- Calm Blue
- Custom color
- RGB readout
- Reset to Royal Purple
- Local persistence

### Local Data
Review passed and remains intentionally simple:
- Export JSON Backup
- Import JSON Backup
- Reminder that clearing browser site data can erase local content

## LocalStorage Keys
- `steward.tasks.v1`
- `steward.journal.v1`
- `steward.gratitude.v1`
- `steward.intention.v1` — compatibility
- `steward.intentions.v1` — dated Morning Intention archive
- `steward.reflection.v1` — compatibility
- `steward.reflections.v1` — dated Prayer & Reflection archive
- `steward.theme.v1` — appearance preference

## Backup / Restore
v1.3.0 JSON Export includes:
- Tasks
- Journals
- Gratitude
- Morning Intention compatibility value
- Full Saved Intentions archive
- Reflection compatibility value
- Full dated Reflections archive
- Theme preference

Restore:
- Restores current archive structures
- Older backups with only a single `intention` remain importable and migrate safely
- Older backups with only a single `reflection` remain importable and migrate safely
- Restores theme when present

## PWA
Core files:
- `index.html`
- `manifest.json`
- `service-worker.js`
- `icons/icon-192.png`
- `icons/icon-512.png`
- `icons/maskable-512.png`

Current cache:
- `steward-pwa-v1.3.0`

Strategy:
- Network-first while online
- Cache fallback while offline
- App shell pre-cached

## Data Safety Rules
1. Never silently delete saved localStorage data.
2. Preserve backward compatibility when reasonably possible.
3. All user-facing dates are `YYYY/MM/DD`.
4. Internal date storage may use `YYYY-MM-DD`.
5. Journal, Intention, Reflection, and Gratitude history must survive normal refresh/reopen.
6. JSON backup must include all dated archives.
7. JSON restore must restore all dated archives.
8. Theme changes must never alter planner content.
9. Clearing Chrome site data can erase local content; regular JSON backup is recommended.

## Known Limitations
- No cloud sync
- No multi-device data sync
- Each device has its own local planner data and theme
- Recurring task execution is not yet implemented
- Scripture is local WEB rotation, not YouVersion
- Archive search is date/keyword based; no tags yet

## Mandatory Documentation Synchronization Rule
`index.html` and `STEWARD_PROJECT.md` are a synchronized pair.

For every meaningful future update:
1. Read latest `index.html`.
2. Read latest `STEWARD_PROJECT.md`.
3. Compare documentation with actual implementation.
4. Make requested changes incrementally.
5. Update `index.html`.
6. Update `STEWARD_PROJECT.md`.
7. Verify version, storage, interaction, cache, backup, and UI rules match.

## Version History

### v1.3.0 — Review Complete
- Enforced global `YYYY/MM/DD` user-facing date rule
- Replaced localized browser date presentation in STEWARD date controls
- Added Journal Archive with date and keyword search
- Upgraded Prayer & Reflection to dated records
- Added safe legacy Reflection migration
- Added combined Reflection + Gratitude Archive
- Added date and keyword search for Reflect history
- Added Royal Purple / Calm Blue / Custom theme system
- Added per-device theme persistence
- Added theme to JSON backup/restore
- Bumped PWA cache to `steward-pwa-v1.3.0`
- Tasks and Local Data reviews passed without unnecessary feature expansion

### v1.2.0 — Today Page Complete
- Fixed Scripture quotation rendering
- Removed user-facing WEB badge
- Added dated Morning Intention archive
- Added date and keyword search
- Added intention archive backup/restore

### v1.1.0 — Today Page Update
- Added daily Scripture rotation
- Added explicit Morning Intention save

### v1.0.1 — Interaction Hotfix
- Fixed JavaScript initialization and interaction failures after deployment
- Switched runtime service-worker fetch to network-first

### v1.0.0 — Android PWA Prototype
- Initial mobile-first installable STEWARD PWA
