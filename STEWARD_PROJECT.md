# STEWARD — Christian Daily Planner

## Project Status
- **Current version:** v1.4.0 — New Theme Update
- **Primary platform:** Android + Google Chrome
- **Architecture:** Local-first Progressive Web App (PWA)
- **Hosting:** GitHub Pages over HTTPS

## v1.4.0 Theme Update
STEWARD keeps one shared functional framework while each user/device can choose its own appearance.

### Available themes
- Royal Purple
- Calm Blue
- Hobbiton — warm moss green, parchment, earthy brown, brass/gold
- Rivendell — silver blue, slate, mist, restrained gold
- Lothlórien — golden green, ivory, luminous olive
- Rohan — saddle brown, wheat gold, warm parchment, muted olive
- Gondor — charcoal, steel blue, ivory, restrained antique gold
- Custom RGB color

### Theme behavior
- Theme selection changes the full STEWARD color system: header, Scripture hero, page background, cards, form surfaces, borders, progress bars, buttons, and navigation accents.
- Theme preference is stored locally in `steward.theme.v1`.
- Different devices using the same STEWARD URL can keep different themes.
- Theme changes never alter planner content.
- Theme preference remains included in JSON backup/restore.
- Reset returns to Royal Purple.

### Asset rule
v1.4.0 uses CSS palettes, gradients, typography treatment, and generic symbols only. No movie artwork, logos, film stills, character images, or proprietary visual assets are embedded.

## Existing Baseline Features
- Daily Scripture rotation
- Today's Three
- Today's Tasks
- Morning Intention + Saved Intentions Archive
- Task management
- Journal + Journal Archive
- Prayer & Reflection dated archive
- Gratitude
- Reflection + Gratitude combined archive
- Date and keyword search
- Global user-facing date format `YYYY/MM/DD`
- JSON backup/restore
- Android PWA install support

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
Current service-worker cache:
- `steward-pwa-v1.4.0`

## Data Safety Rules
1. Never silently delete localStorage data.
2. Theme changes must never modify planner records.
3. User-facing dates remain `YYYY/MM/DD`.
4. Backup must include all archives and theme preference.
5. Preserve backward compatibility where reasonably possible.

## Mandatory Documentation Synchronization Rule
`index.html` and `STEWARD_PROJECT.md` are a synchronized pair. Every meaningful change must update both and keep service-worker cache/version documentation aligned.

## Version History
### v1.4.0 — New Theme Update
- Added Hobbiton theme
- Added Rivendell theme
- Added Lothlórien theme
- Added Rohan theme
- Added Gondor theme
- Preserved Royal Purple, Calm Blue, and Custom RGB
- Expanded theme engine to full palette presets
- Preserved per-device persistence and backup/restore
- Bumped cache to `steward-pwa-v1.4.0`

### v1.3.0 — Review Complete
- Global `YYYY/MM/DD`
- Journal Archive
- Dated Reflection
- Reflection + Gratitude Archive
- Royal Purple / Calm Blue / Custom theme system

### v1.2.0 — Today Page Complete
- Scripture polish and Saved Intentions Archive

### v1.1.0 — Today Page Update
- Daily Scripture rotation and explicit Save Intention

### v1.0.1 — Interaction Hotfix
- Fixed deployed JavaScript interactions

### v1.0.0 — Android PWA Prototype
- Initial installable STEWARD PWA
