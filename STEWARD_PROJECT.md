# STEWARD — Christian Daily Planner

## Project Status
- **Current version:** v1.0.1 Android PWA Hotfix
- **Primary platform:** Android + Google Chrome
- **Architecture:** Local-first Progressive Web App (PWA)
- **Hosting:** GitHub Pages over HTTPS

## Project Purpose
STEWARD is a Christian-inspired personal planner for purposeful work, stewardship, prayer, gratitude, reflection, and journaling.

> **Plan with purpose. Work with faith.**

## Visual System
- Deep purple `#2F153F`
- Dark purple `#44215B`
- Primary purple `#6F4589`
- Lavender `#9D76B7`
- Soft lavender `#F4EDF8`
- Warm gold accent for the cross
- Subtle butterfly elements symbolize transformation, renewal, hope, and new life

## Navigation
1. Today
2. Tasks
3. Journal
4. Reflect
5. Settings

## Current Features
- Daily Scripture
- Today's Three
- Add / complete / delete tasks
- Task purpose, category, priority, due date
- Daily completion progress
- Morning Intention
- Prayer & Reflection
- Dated Gratitude records
- Daily Journal with one entry per date
- Journal user-facing format `YYYY/MM/DD`
- Journal internal key format `YYYY-MM-DD`
- Previous journal history
- localStorage persistence
- JSON backup and restore
- Android PWA manifest
- Service worker offline app-shell cache
- 192px, 512px and maskable application icons
- Android Chrome install-prompt support

## LocalStorage Keys
- `steward.tasks.v1`
- `steward.journal.v1`
- `steward.gratitude.v1`
- `steward.intention.v1`
- `steward.reflection.v1`

## Journal Data Structure
```json
{
  "2026-08-29": {
    "displayDate": "2026/08/29",
    "content": "Journal content...",
    "updatedAt": "ISO timestamp"
  }
}
```

## PWA Files
- `index.html`
- `manifest.json`
- `service-worker.js`
- `icons/icon-192.png`
- `icons/icon-512.png`
- `icons/maskable-512.png`

## Service Worker
Current cache: `steward-pwa-v1.0.1`

The v1.0.1 service worker changes the runtime fetch strategy to network-first so newly deployed GitHub Pages updates are less likely to be hidden behind an older cached `index.html`.

## v1.0.1 Hotfix
This release fixes the first GitHub Pages deployment where the visual UI loaded but JavaScript interactions did not initialize reliably.

Changes:
- Replaced implicit HTML-ID JavaScript globals with explicit `document.getElementById(...)` references.
- Renamed ambiguous IDs such as `export`, `import`, and `install` to `exportBtn`, `importFile`, and `installBtn`.
- Explicitly bound Add Task, navigation, Journal, Reflection, Gratitude, backup, restore, and install event handlers.
- Preserved all existing localStorage keys to avoid data loss.
- Updated the service worker cache from `steward-pwa-v1.0.0` to `steward-pwa-v1.0.1`.
- Updated runtime cache behavior to prefer the latest network response when online.
- Backup export version updated to `1.0.1`.

## Data Safety Rules
1. Never silently delete saved localStorage data.
2. Warn before breaking storage migrations.
3. Keep Journal display date format `YYYY/MM/DD` unless explicitly changed.
4. JSON backup must include every journal record.
5. JSON restore must restore every journal record.
6. Existing storage keys should remain backward-compatible when reasonably possible.
7. Clearing Chrome site data can erase local content, so regular backup is recommended.

## Known Limitations
- No cloud sync or multi-device sync
- Data remains on the browser/device where it was created
- Recurring task execution is not yet implemented
- Daily Scripture is static in v1.0.1

## Mandatory Documentation Synchronization Rule
`index.html` and `STEWARD_PROJECT.md` are a synchronized project pair.

For every meaningful future update:
1. Read the latest `index.html`.
2. Read the latest `STEWARD_PROJECT.md`.
3. Compare implementation and documentation.
4. Modify the application.
5. Update `STEWARD_PROJECT.md` in the same change set.
6. Verify feature, storage, interaction, cache and version documentation match the implementation.

Do not update only `index.html` when a change affects documented project state.

## Version History

### v1.0.1 — Interaction Hotfix
- Fixed JavaScript initialization failure after GitHub Pages deployment
- Replaced implicit element globals with explicit DOM lookups
- Explicitly bound interactive controls
- Preserved localStorage schema
- Bumped service worker cache to `steward-pwa-v1.0.1`
- Switched runtime fetch handling to network-first
- Updated synchronized project documentation

### v1.0.0 — Android PWA Prototype
- Rebuilt as mobile-first Android Chrome PWA
- Added manifest and service worker
- Added offline app shell
- Added install prompt support
- Added application icons
- Added bottom navigation
- Added Today's Three and task management
- Added Morning Intention
- Added Prayer & Reflection
- Added Gratitude
- Added dated Daily Journal
- Added JSON backup and restore
- Established synchronized Markdown documentation
