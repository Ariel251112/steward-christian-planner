# STEWARD — Christian Daily Planner

## Project Status
- **Current version:** v1.2.0 — Today Page Complete
- **Primary platform:** Android + Google Chrome
- **Architecture:** Local-first Progressive Web App (PWA)
- **Hosting:** GitHub Pages over HTTPS

## Project Purpose
STEWARD is a Christian-inspired personal planner for purposeful work, stewardship, prayer, gratitude, reflection, and journaling.

> **Plan with purpose. Work with faith.**

## Today Page — v1.2.0 Baseline

### Verse for Today
- Uses a built-in local library of 31 English Bible verses.
- Verse text source is World English Bible (WEB), Public Domain.
- Source/licensing information is documented here, but not displayed in the user-facing Scripture hero.
- Verse selection is deterministic by the user's local calendar date.
- The same verse stays stable throughout the same date.
- A different date automatically selects a different verse.
- The UI displays only the section label, Scripture text, and Scripture reference.
- The double quotation issue is fixed: the `<q>` element supplies the quotation marks and JavaScript no longer injects a second pair.
- YouVersion integration remains a future enhancement.

### Today's Three
- Displays up to three incomplete tasks marked for Today's Three.
- Purpose: `What matters most today?`
- No behavior change in v1.2.0.

### Today's Tasks
- Displays all current tasks.
- Shows total task count, completed count, and Daily Stewardship completion percentage.
- Supports Add, complete, and delete.
- No behavior change in v1.2.0.

### Morning Intention
- Displays today's date as `YYYY/MM/DD`.
- User writes today's intention and presses **Save Intention**.
- Editing displays `Unsaved changes`; successful save displays `Saved`.
- One intention record is stored per local calendar date.
- Saving again on the same date updates that date rather than creating a duplicate.

#### Saved Intentions Archive
- **View Saved Intentions** expands an archive below the current entry.
- Records are sorted newest-first.
- Search supports:
  - exact date
  - keyword
  - date + keyword together
- Archive entries display the saved date and full content.

#### Intention storage
New dated archive key:
- `steward.intentions.v1`

Conceptual structure:
```json
{
  "2026-08-29": {
    "displayDate": "2026/08/29",
    "content": "Focus on serving well and not rushing.",
    "updatedAt": "ISO timestamp"
  }
}
```

Legacy compatibility key:
- `steward.intention.v1`

On first load after upgrading, an existing legacy Morning Intention is migrated into today's dated record if today's archive record does not already exist. The legacy key is preserved for backward compatibility.

## Current Features
- Daily rotating Scripture
- Today's Three
- Today's Tasks with completion progress
- Morning Intention with dated archive
- Intention archive date search
- Intention archive keyword search
- Prayer & Reflection
- Gratitude
- Daily Journal
- localStorage persistence
- JSON backup and restore
- Android PWA manifest
- Offline app shell
- Android Chrome install support

## LocalStorage Keys
- `steward.tasks.v1`
- `steward.journal.v1`
- `steward.gratitude.v1`
- `steward.intention.v1`
- `steward.intentions.v1`
- `steward.reflection.v1`

## Backup / Restore
JSON export now includes:
- tasks
- journals
- gratitude
- current intention compatibility value
- full dated `intentions` archive
- reflection

JSON restore:
- restores the full `intentions` archive when present
- remains compatible with older backups containing only a single `intention`

## PWA
Current service worker cache:
- `steward-pwa-v1.2.0`

Runtime strategy:
- network-first while online
- cache fallback while offline
- core app shell pre-cached

## Data Safety Rules
1. Never silently delete saved localStorage data.
2. Warn before breaking storage migrations.
3. Journal and Intention user-facing dates remain `YYYY/MM/DD`.
4. JSON backup must include all Journal and Saved Intention records.
5. JSON restore must restore Journal and Saved Intention records.
6. Preserve existing storage keys when reasonably possible.
7. Clearing browser site data can erase local content; regular JSON backups are recommended.

## Known Limitations
- No cloud sync or multi-device sync
- Data remains on the browser/device where it was created
- Recurring task execution is not yet implemented
- Daily Scripture uses the local WEB verse library rather than YouVersion
- Saved Intentions support date and text search, but not tags/categories

## Mandatory Documentation Synchronization Rule
`index.html` and `STEWARD_PROJECT.md` are a synchronized project pair.

For every meaningful future update:
1. Read the latest `index.html`.
2. Read the latest `STEWARD_PROJECT.md`.
3. Compare implementation and documentation.
4. Modify the application.
5. Update `STEWARD_PROJECT.md` in the same change set.
6. Verify feature, storage, interaction, cache and version documentation match the implementation.

Do not update only one when a change affects documented project state.

## Version History

### v1.2.0 — Today Page Complete
- Fixed Scripture double quotation rendering
- Removed user-facing `WEB · Public Domain` badge
- Preserved date-based daily Scripture rotation
- Added dated Morning Intention records
- Added Saved Intentions Archive
- Added date and keyword archive search
- Added safe legacy Morning Intention migration
- Added full intention archive to JSON backup/restore
- Bumped service worker cache to `steward-pwa-v1.2.0`
- Established Today page v1.2.0 baseline pending acceptance test

### v1.1.0 — Today Page Update
- Added date-based daily Scripture rotation
- Added local WEB Scripture library
- Added explicit Save Intention
- Added saved/unsaved status

### v1.0.1 — Interaction Hotfix
- Fixed JavaScript initialization after GitHub Pages deployment
- Replaced implicit element globals with explicit DOM lookups
- Switched service worker runtime strategy to network-first

### v1.0.0 — Android PWA Prototype
- Initial mobile-first PWA
- Added task management, Journal, Reflection, Gratitude, backup/restore and install support
