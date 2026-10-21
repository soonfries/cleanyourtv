## ADDED Requirements

### Requirement: Comfort features are off by default
Every comfort feature in `launcher-comfort` and `launcher-profiles` SHALL be switched off after a fresh install and after an upgrade from a version without it.

#### Scenario: Fresh install
- **WHEN** the launcher is installed on a TV for the first time
- **THEN** folders, number-key shortcuts, sleep timer, accessibility view, profiles, kids mode, the recently opened row and the screen-time limit are all off
- **AND** no preferences file for a class B feature exists

#### Scenario: Upgrade
- **WHEN** a TV upgrades from a launcher version without these features
- **THEN** the home screen looks and behaves as before the upgrade

### Requirement: Features are switched on and off on the TV
Each comfort feature SHALL have an on/off entry in the launcher settings that works with the remote alone, without ADB, `config.xml` or a theme.

#### Scenario: Switching on with the remote
- **WHEN** a person opens launcher settings and selects a comfort feature
- **THEN** the feature can be switched on with D-pad and OK

### Requirement: Switch-on notice for personal data
Switching on a feature that stores personal or usage data (class B) SHALL first show one sentence stating what is stored, that it stays on this TV, and how to delete it.

#### Scenario: Turning on the recently opened row
- **WHEN** a person switches on the recently opened row
- **THEN** a notice says the launcher remembers when it last opened each app, keeps it on this TV for at most 30 days, and deletes it when the row is switched off
- **AND** the feature is on only after the person confirms

### Requirement: Switching off erases the feature's data
Switching a comfort feature off SHALL delete every value the feature stored. The launcher settings SHALL offer "Delete all launcher data", which removes all class B data and resets all comfort features to off.

#### Scenario: Erase on switch-off
- **WHEN** a person switches off profiles
- **THEN** the profiles preferences file, including PIN hashes, app allow-lists, recently opened entries and screen-time totals, no longer exists

#### Scenario: Delete all
- **WHEN** a person selects "Delete all launcher data" and confirms
- **THEN** no class B preferences file exists and every comfort feature is off

### Requirement: No new permissions
The launcher manifest SHALL NOT gain `INTERNET`, `PACKAGE_USAGE_STATS`, location, microphone, camera or account permissions through any comfort feature, and `android:allowBackup` SHALL remain `false`.

#### Scenario: Manifest check in CI
- **WHEN** the test suite runs
- **THEN** a test compares the manifest's permissions with an allow-list and fails on any addition
