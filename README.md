# Ally Watch

**Crusader Kings III — keep an eye on other rulers' alliances.**

Before you declare war, the question that actually matters is who your target can call in.
CK3 never tells you when that changes. You open their window, count the allies, close it,
and do it again next year in case something moved.

Ally Watch does the counting. Mark a ruler, and the game tells you the moment their
alliances shift — including the moment they run out of allies entirely.

Built for **CK3 1.19.x (Scribe)**. Script only. No interface files replaced, no vanilla
files overwritten, works alongside other mods.

---

## How to use it

Everything lives in the **right-click menu on a character portrait**, under Diplomacy.
There is no new button on the screen and no new tab — if you do not right-click, you will
never see the mod.

### Start watching someone

Right-click the ruler's portrait → **Watch This Ruler**.

You can also click their realm on the map and right-click the portrait that comes up. There
is no distance limit; a ruler on the far side of the world can be watched.

Watch as many rulers as you like.

### See who you are watching

Right-click **your own portrait** → **My Watch List**.

> This is the one that is easy to miss. Your own portrait, not theirs.
>
> The entry only appears while you are watching at least one ruler. If your list is empty
> the line is not there at all — that is not the mod failing.

The list gives you a button per ruler. Click one and you get their own small screen, where
you can change how early they are reported, or stop watching them.

### Check a ruler's alliances right now

Right-click any portrait → **Alliance Status**.

Opens a panel with their current allies, and below it any alliances of theirs that have
broken while you were watching. Works on anyone — you do not have to be watching them first.

Names in the panel are clickable and jump to that character.

---

## What you get told

| Notification | When |
|---|---|
| **Ally Lost** | They lose one ally. Says how many are left. |
| **No Allies Left** | They just lost their last one. This is the one you are waiting for. |
| **New Ally** | They gained an ally. Bad news, marked as such. |
| **Watched Ruler Died** | With their age and who succeeded them. |

When a watched ruler dies they drop off your list — their alliances died with them, and the
heir is a different person with different friends. Watch the successor if you want to keep
following that realm.

**The game is never paused by any of this**, on purpose. Pausing in multiplayer stops the
game for everybody.

## Turning down the noise

A ruler with five allies losing them one at a time means five notifications, and you
probably only care about the last one.

Open **My Watch List**, click the ruler, and use *Report a little later* to hold the
notifications back:

- **Report every change** — the default. Every alliance they gain or lose.
- **Down to N allies or fewer** — silence until they hit that number.
- **Only when they have no allies left** — the quietest setting. Nothing until they are alone.

Each watched ruler is set separately, and **the setting is yours alone** — in multiplayer
your co-op partner can watch the same ruler with a completely different setting, and neither
of you affects the other.

*No Allies Left*, *New Ally* and death notifications ignore this setting and always arrive.
They are rare and always worth knowing.

### Sound and where notifications appear

Handled by the game's own **Settings → Message Settings → Ally Watch**. Each of the five
notification types is listed separately and can be set to:

- **Toast** — pops up on screen with a sound
- **Feed** — slides quietly into the message list, no interruption
- **Never** — off completely

So if you want silence except for the important one, set *Watched ruler loses an ally* to
Feed and leave *Watched ruler has no allies left* on Toast.

---

## Installation

Subscribe on the Steam Workshop and enable it in the launcher.

**Ally Watch - Turkce** is a separate text-only submod that translates the mod into Turkish.
CK3 has no Turkish language slot, so it replaces the English strings — the same approach the
community Turkish patches use. Load it **after** the main mod. Ignore it if you play in
English.

## Multiplayer

Works in co-op. A notification only goes to the player watching that ruler, not to everyone,
and notification settings are per player.

As with every CK3 mod, all players need an identical mod list or the checksum will not match
and you will not be able to join each other.

## Good to know

- **Broken alliances are only recorded from the moment you start watching.** The Alliance
  Status panel cannot show you history from before that — the game does not keep it.
- The broken list remembers the last five.
- The watch list has no size limit; the panel shows six at a time with a next-page button.
- Like any mod, this disables achievements in Ironman.

## Reporting a problem

Open an issue with what you did, what you expected, and what happened instead. If the game
logged anything, `Documents/Paradox Interactive/Crusader Kings III/logs/error.log` is the
useful file.

## License

MIT — see [LICENSE](LICENSE). Translate it, fork it, fix it, fold it into your own mod;
just keep the copyright notice with the source.
