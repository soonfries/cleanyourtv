# Tasks

## 1. Privacy groundwork (launcher-privacy)
- [ ] 1.1 Test: manifest permissions match an allow-list; fails on `INTERNET`, `PACKAGE_USAGE_STATS`, location, microphone
- [ ] 1.2 Feature switch helper: each feature gets its own prefs file; switching off deletes it
- [ ] 1.3 "Delete all launcher data" entry in `LauncherSettingsActivity`
- [ ] 1.4 One-sentence data notice shown when a class B feature is switched on (all `values-*`)
- [ ] 1.5 Test per feature: off after install, prefs file gone after switching off

## 2. Class A comfort features (launcher-comfort)
- [ ] 2.1 Folders in the app grid (tile + glass dialog like the app library)
- [ ] 2.2 Number keys 1 to 9 as shortcuts while Home is in front, off by default
- [ ] 2.3 Sleep timer (resolve open question in design.md first)
- [ ] 2.4 Accessibility view: large type, high contrast focus, three-app dock without grid
- [ ] 2.5 Settings export/import through `tools/theme.sh` and `ThemeProvider`, class A keys only; test that class B keys are never written

## 3. Class B features (launcher-profiles)
- [ ] 3.1 Profiles: up to five, name and colour only, profile chip top left
- [ ] 3.2 Kids mode: allow-list of apps, PIN hashed with PBKDF2, back-off after five failures
- [ ] 3.3 "Recently opened" row from `LastOpened`, one timestamp per app, 30-day expiry, per profile
- [ ] 3.4 Screen-time limit per kids profile: today's minutes only, reset at midnight, lock screen with PIN
- [ ] 3.5 Migration of existing `last_opened` data (see design.md)

## 4. Modules (launcher-modules)
- [ ] 4.1 Add the module privacy requirements to `docs/specs/card.md` and `docs/modules.md`
- [ ] 4.2 Optional reference module: weather with manually entered place, no location permission

## 5. Docs and verification
- [ ] 5.1 "Privacy" section in `README.md` listing what each feature stores and how to delete it
- [ ] 5.2 Verify each feature on a real TV with screenshots, D-pad from every edge
- [ ] 5.3 `openspec validate add-opt-in-comfort-features --strict`
