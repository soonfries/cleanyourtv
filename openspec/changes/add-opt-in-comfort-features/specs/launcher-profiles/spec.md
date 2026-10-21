## ADDED Requirements

### Requirement: Local profiles without identity data
When switched on, the launcher SHALL support up to five profiles, each with its own dock, folders and visible apps. A profile SHALL store only a free-text name, a colour or symbol and its app choices; it SHALL NOT ask for a real name, photo, birth date or account. The active profile SHALL be shown on the home screen.

#### Scenario: Creating a profile
- **WHEN** a person creates a profile
- **THEN** the launcher asks only for a name and a colour
- **AND** the profile's name appears top left while it is active

#### Scenario: Profiles are separate
- **WHEN** a person switches from profile A to profile B
- **THEN** B's dock, recently opened row and screen-time total do not show A's data

### Requirement: Kids mode behind a PIN
A profile MAY be marked as a kids profile. In a kids profile only allowed apps SHALL be shown, and leaving the profile or opening launcher settings SHALL require a PIN. The PIN SHALL be stored only as a salted PBKDF2 hash and SHALL NOT appear in logs. After five wrong entries the launcher SHALL impose a growing wait. A forgotten PIN SHALL be resettable only by clearing the launcher's data.

#### Scenario: Wrong PIN
- **WHEN** a wrong PIN is entered five times
- **THEN** further attempts are refused for a waiting period that grows with each further failure

#### Scenario: Switch-on notice states the limits
- **WHEN** a person switches on kids mode
- **THEN** the notice says kids mode is a convenience lock and that the voice button and the remote's app buttons can still start apps

### Requirement: Recently opened row
When switched on, the home screen SHALL show apps recently opened from Home. The launcher SHALL keep only the latest timestamp per app per profile, recorded when Home opens the app, and SHALL delete entries older than 30 days. It SHALL NOT read system usage statistics or content from other apps, including Android TV "Watch Next" channels.

#### Scenario: Entry expires
- **WHEN** an app was last opened from Home 31 days ago
- **THEN** it no longer appears in the row and its timestamp is deleted

#### Scenario: Removing one entry
- **WHEN** a person long-presses an app in the row and chooses Remove
- **THEN** that app's timestamp is deleted

### Requirement: Daily screen-time limit
A kids profile MAY have a daily limit and quiet hours. The launcher SHALL store only today's total minutes per profile, SHALL delete it at midnight, and SHALL NOT keep history or per-app times. The remaining time SHALL be visible on the home screen. When the limit is reached the launcher SHALL show a lock screen that needs the PIN.

#### Scenario: Limit reached
- **WHEN** a kids profile with a 120-minute limit reaches 120 minutes today
- **THEN** the launcher shows the lock screen
- **AND** after midnight the total starts again at zero with no record of the previous day
