## ADDED Requirements

### Requirement: Folders in the app grid
The launcher SHALL let a person group apps into named folders that appear as tiles in the grid and open as a dialog styled like the app library. Folder data SHALL consist only of the folder name and package names.

#### Scenario: Opening a folder
- **WHEN** a person focuses a folder tile and presses OK
- **THEN** a dialog lists the folder's apps and D-pad navigation inside it is deterministic

### Requirement: Number-key shortcuts
When switched on, the number keys 1 to 9 SHALL start the app assigned to that key while the home screen is in the foreground. The launcher SHALL NOT use an accessibility service for this.

#### Scenario: Pressing a number on Home
- **WHEN** number-key shortcuts are on and a person presses 2 on the home screen
- **THEN** the app in the second dock slot (or the app assigned to 2) starts

#### Scenario: Pressing a number in another app
- **WHEN** another app is in the foreground and a person presses 2
- **THEN** the launcher does nothing and the key reaches that app

### Requirement: Sleep timer
When switched on, the home screen SHALL offer a sleep timer of 15, 30, 60 or 90 minutes. It SHALL store only the chosen end time and SHALL NOT log when the TV was used.

#### Scenario: Timer runs out
- **WHEN** a 30-minute timer was set and 30 minutes pass
- **THEN** the TV goes to sleep through the firmware's own sleep function, or shows a dimmed countdown overlay where the firmware offers none

### Requirement: Accessibility view
The launcher SHALL offer a view with larger type and tiles, a high-contrast focus highlight and a dock of three apps without the grid. It SHALL respect `reduced_motion` and the system font scale.

#### Scenario: Large type for an older viewer
- **WHEN** the accessibility view is on
- **THEN** the clock, tile names and pills use the larger type and only the dock is shown

### Requirement: Export and import of non-personal settings
The launcher SHALL export dock, folders, theme and key assignments to a file and import such a file on another TV. The export SHALL contain only class A settings and SHALL NOT contain profiles, PIN hashes, recently opened entries or screen-time data.

#### Scenario: Export with profiles switched on
- **WHEN** profiles and the recently opened row are on and a person exports settings
- **THEN** the exported file contains no key from the profiles, last_opened or screen_time stores
