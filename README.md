# Ally Watch

A Crusader Kings III mod that watches other rulers' alliances for you.

Planning a war is mostly a question of who your target can call in. CK3 never tells you
when that changes — you have to keep opening the character window to check. Ally Watch
turns that into a notification.

Built for **CK3 1.19.x (Scribe)**. Script only, no `.gui` files touched, no vanilla file
overwritten.

---

## What it does

Right-click any landed ruler's portrait. Three entries appear under Diplomacy:

| Entry | What it does |
|---|---|
| **Watch This Ruler** | Adds them to your watch list. No limit on how many. |
| **Stop Watching** | Removes them again. |
| **Alliance Status** | Opens a panel showing their current allies and, if you were watching, the alliances that have broken since. Works on anyone, tracked or not. |

While a ruler is watched you get a notification when they:

- **lose an ally** — with how many they have left
- **lose their last ally** — the moment they are worth attacking
- **gain an ally** — bad news, flagged accordingly
- **die** — with their age and successor, after which they drop off the list

Every notification is a real CK3 message, so each one can be switched off individually
under Settings → Message Settings → *Ally Watch*.

Nothing pauses the game. That is deliberate — this is meant to be usable in multiplayer,
where a forced pause hits everyone.

## Multiplayer

Works in co-op. Notifications only go to the player who is watching that ruler, not to
everyone. As with any CK3 mod, all players need the identical mod list or the checksum
will not match.

## Installation

Subscribe on the Steam Workshop, or drop the folder into
`Documents/Paradox Interactive/Crusader Kings III/mod/` with a matching `.mod` file.

`AllyWatchTR` is a separate text-only submod. CK3 has no Turkish language slot, so it
overrides the English strings the same way the community Turkish patches do. Load it
**after** the main mod. Skip it entirely if you want English.

---

## How it works

### Hooks

Four vanilla on_actions, no polling:

| on_action | Used for |
|---|---|
| `on_alliance_added` | ally gained |
| `on_alliance_removed` | alliance ended because its reason went away |
| `on_alliance_broken` | alliance actively broken |
| `on_death` | watched ruler died |

on_actions with the same key in different files are merged by the game, so vanilla's own
handlers keep running untouched and other mods hooking the same on_actions still work.

The alliance on_actions hand over `scope:first` and `scope:second` without saying which
is which, so each check runs in both directions.

### State

The watch list is a variable list `allywatch_tracked` on the **watching player** and
nowhere else. Lookups go through `every_player` + `is_target_in_variable_list`. There is
no reverse index on the watched character, so there is nothing that can fall out of sync.

Broken alliances are recorded as `allywatch_ex_allies` on the watched character, capped
at 5 entries, and only while somebody is watching — the rest of the map stays clean.
Re-allying removes the entry so nobody shows up as a current and a former ally at once.

### Cost

Every effect starts with a single list check and returns immediately if nobody is
watching. AI alliances churning across the map cost effectively nothing.

### The status panel

CK3 loc has no loops, so a dynamic list cannot be written as plain text. The panel is a
message with `display = popup` and `desc = event_message_effect` — the body is whatever
the sending effect renders. `show_as_tooltip` renders without executing, and inside a
loop `custom_tooltip` prints one line per element with `[THIS...]` bound to the current
one. Same technique vanilla uses for `MIGRATION_CB_TITLE`.

## Layout

```
AllyWatch/
  common/
    character_interactions/   watch / stop watching / status panel
    on_action/                the four hooks
    scripted_effects/         notification + report logic
    scripted_triggers/        "is tracked" and duplicate-event guard
    script_values/            ally count
    messages/                 6 message types
    message_filter_types/     5 filters, all toggleable
    message_group_types/      own section in Message Settings
  localization/english/       all strings
AllyWatchTR/
  localization/english/       Turkish strings, overrides the above
```

## Known limits

- Broken alliances are only recorded from the moment you start watching. There is no way
  to recover history from before that.
- The broken list keeps the last 5.
- No date on broken alliances yet.
- Tracking does not carry over to the heir when a watched ruler dies; you re-add the
  successor if you want to keep following that realm.

## Ideas for later

- Dates on broken alliances
- Optionally follow the successor instead of dropping the entry
- Notification when a watched ruler is deposed or loses their title
- A single panel listing everyone you are watching at once
