## ADDED Requirements

### Requirement: Network features ship as modules
Any comfort feature that needs the network, such as weather, calendar, smart home or a photo screensaver, SHALL be a separate module app using the card contract in `docs/specs/card.md`. The launcher SHALL NOT pass data to modules beyond what the card contract defines and SHALL show a module's card only after the owner chose Show.

#### Scenario: No module installed
- **WHEN** no module app is installed
- **THEN** the TV has no network traffic caused by CleanYourTV

### Requirement: Privacy rules for project modules
Modules published by this project SHALL hold their own `INTERNET` permission, SHALL name the service they contact and the data sent (at least IP address and time) on first start, SHALL NOT use device identifiers, accounts, analytics or advertising SDKs or third-party crash reporting, and SHALL fetch only while their card is visible and at most every 30 minutes.

#### Scenario: Weather module
- **WHEN** a person sets up the weather module
- **THEN** it asks for a town or postcode instead of requesting location permission
- **AND** it names the weather service before the first request

#### Scenario: Calendar module on a shared screen
- **WHEN** the calendar module shows today's events
- **THEN** event titles are hidden by default and only the number of events is shown

### Requirement: Excluded features
The launcher and project modules SHALL NOT offer cloud voice search, content recommendations, "Watch Next" from other apps, accounts or cloud sync, or per-app usage reports.

#### Scenario: Request for usage reports
- **WHEN** a contribution adds weekly or per-app usage reports
- **THEN** it does not meet this spec and is declined
