# Change: Add opt-in comfort features under privacy by design and by default

## Why

Alternative launchers offer conveniences that people miss on a TV: folders, number-key shortcuts,
a sleep timer, a large-type view for older viewers, profiles with a kids mode, a "continue" row and
a daily screen-time limit. Most launchers build these on usage tracking, accounts and cloud sync.
CleanYourTV exists to remove exactly that from the TV, so these features must be built so that they
collect nothing by default, keep whatever they need on the TV, and can be switched off and erased
by anyone in the household with the remote.

The design follows Art. 25 GDPR and the Standard Data Protection Model (SDM): each feature is
checked against the protection goals data minimisation, confidentiality, unlinkability,
transparency and intervenability before it is specified.

## What Changes

- **Cross-cutting privacy rules for the launcher** (new capability `launcher-privacy`): every
  comfort feature is off after install; switching it on happens on the TV and shows what it stores;
  switching it off deletes its data; a "Delete all launcher data" entry; no new Android permission;
  no data in Android backup; one test per feature for default-off and erase-on-off.
- **Class A comfort features without personal data** (new capability `launcher-comfort`): folders
  in the app grid, number keys 1 to 9 as app shortcuts, a sleep timer, an accessibility view (large
  type, high contrast, simple dock), and export/import of non-personal settings.
- **Class B features with local personal data** (new capability `launcher-profiles`): up to five
  profiles with an optional kids mode behind a hashed PIN, a "recently opened" row that extends
  `LastOpened` with a 30-day expiry, and a daily screen-time limit that keeps only today's total.
- **Class C features needing the network** (new capability `launcher-modules`): weather, calendar,
  smart home and photo screensaver are specified as separate module apps on the existing card
  contract, never as launcher code. Requirements for those modules: own `INTERNET` permission, named
  provider, no device id, no analytics SDKs, fetch only while visible.
- **Explicit non-goals**: cloud voice search, content recommendations or "Watch Next" from other
  apps, accounts and cloud sync, per-app usage reports for parents.

No existing behaviour changes. Nothing is enabled for current installs.

## Impact

- Affected specs: `launcher-privacy`, `launcher-comfort`, `launcher-profiles`, `launcher-modules`
  (all new).
- Affected code: `launcher/app/src/main/java/com/gathin/tvhome/` (`LauncherSettingsActivity`,
  `AppAdapter`, `LastOpened`, `MainActivity`, `Config`, new `Profiles`, `Folders`, `ScreenTime`,
  `SettingsExport`), `res/values*/strings.xml`, `res/values/config.xml`, `tools/theme.sh`, `tests/`.
- Affected docs: `README.md` (privacy section), `docs/modules.md`, `docs/specs/card.md` (module
  privacy requirements).
- Manifest: unchanged permissions. This is an acceptance criterion, enforced by a test.
