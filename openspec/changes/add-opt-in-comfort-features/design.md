# Design: opt-in comfort features

## Context

The launcher runs on TVs with about 1 GB of RAM and has no network, no polling and no background
service (`CONTRIBUTING.md`). Several people share one TV, including children and guests, and
whatever the launcher shows is visible to everyone in the room. The person who installs
CleanYourTV is often not the person who watches (the "parents' TV" case in `docs/REMOTE.md`).

## Goals / Non-Goals

- Goals: useful conveniences on the TV; nothing collected until a person switches a feature on;
  every stored value deletable from the TV with the remote; no new permission in the launcher.
- Non-Goals: parental control that resists a determined child; usage analytics of any kind;
  syncing between TVs beyond a manual settings file.

## Decisions

- **Feature classes.** A: no personal data. B: personal or usage data, kept only on the TV.
  C: network. Class C never lives in the launcher; it ships as module apps on the card contract,
  so the launcher keeps no `INTERNET` permission and a household that installs no module has no
  extra traffic.
- **Storage.** Class B data lives in its own private `SharedPreferences` file per feature
  (`profiles`, `last_opened`, `screen_time`), so switching a feature off can delete the whole file
  and a test can assert the file is gone. Android backup stays off (`allowBackup="false"`).
- **Export excludes class B.** The settings export (K-5) writes only class A keys. Profiles and
  usage describe people and do not travel to another TV, even when asked.
- **PIN.** Stored as PBKDF2-HMAC-SHA256 with a random salt and at least 100,000 iterations, never in
  logs. Five wrong attempts start a growing wait. A forgotten PIN is reset only by clearing the
  launcher's data over ADB or in system settings: no recovery question, no back door.
- **"Recently opened" uses the launcher's own timestamps.** `LastOpened` already records the time
  Home opened an app. The row reuses it, keeps one timestamp per app, expires entries after 30
  days, and never reads `UsageStatsManager` or other apps' "Watch Next" channels.
- **Number keys only in the foreground.** Digits are handled in `MainActivity`'s key dispatch. No
  accessibility service, because one would see every key press in every app.
- **Kids mode is a convenience lock, not child protection.** The voice button and the remote's app
  buttons can still start apps. The switch-on text says so.

## Risks / Trade-offs

- Screen time without a background service is approximate: the launcher can only measure from
  profile activation and screen on/off broadcasts while its process is alive. Accepted; the limit
  is a household convenience.
- Folders and app allow-lists reveal app choices to anyone opening settings. Accepted, as the data
  stays on the TV and is visible only to people already in the room.

## Open Questions

- **Sleep timer:** an ordinary app cannot put the TV to sleep (`DEVICE_POWER` is a system
  permission). Options are opening the TV's own sleep timer setting where the firmware exposes one,
  or a dim overlay with a countdown. Needs testing on Google TV, TCL and Xiaomi firmware.
- **Screen-time enforcement:** an `AlarmManager` alarm at the computed limit that brings Home to
  the front with a lock screen, without a service. Needs checking against Android TV 9 to 14
  background-start restrictions.
- Whether the existing `last_opened` data (cinematic home) migrates into the new feature switch or
  is dropped on upgrade. Proposal: keep it only if cinematic home is on, otherwise delete it.
