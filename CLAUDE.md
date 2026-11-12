# Project brief (working title: TBD)

This file is the standing brief for Claude Code. Read it at the start of every session, along with README.md, CONTRIBUTING.md, PARITY.md, TASKS.md and docs/.

## What this is

A persistent, browser-based multiplayer game engine and world, forked from ZZTMMO
(https://github.com/shotintoeternity/zztmmo, MIT licence). ZZTMMO is a fork of
Ben Hoyt's zztgo, which was machine-converted from Adrian Siekierka's
Reconstruction of ZZT. We start from ZZT's mechanics, scripting (ZZT-OOP) and
look, then grow into our own game. It is no longer intended to be faithful ZZT.

Owner: Aisling (Hiraeth Systems). Development machine: "Saoirse", Debian 13, KDE Plasma.

## Decisions already made

- Only worlds made specifically for this project are hosted. No Museum of ZZT
  worlds, no Town of ZZT, no original Epic MegaGames content in releases.
- Classic ZZT graphics for the first playable milestone.
- Later: "Level 2" graphics (multi-colour glyphs, larger palette, new world
  format), with "Level 3" effects (lighting, animated tiles) possible after.
- A built-in pixel art tool for glyphs and palettes, inside the browser editor.
- Character classes are parked. Do not build them until asked.
- Public hosting (OVH VPS) only after moderation tools exist.

## Working rules

Upstream house rules still apply until we deliberately retire them:

- Never guess ZZT behaviour. If the Go is unclear, read the matching Pascal.
- Determinism is sacred: no global math/rand, no time.Now(), no time.Sleep, and
  no map iteration that affects game state order in simulation code.
- Never edit fixture hashes or delete replay tests to make a build pass.
  Intentional behaviour changes get a `DEVIATION:` line in the commit message.
- `go test ./...` must pass before every commit.

Our own rules:

- Keep the upstream LICENSE and NOTICE.md and their credits intact. Add our own
  copyright line alongside, never in place of, the existing ones.
- Before any change touching more than a few files, explain the plan and wait
  for approval.
- Small, focused commits with clear messages.
- After each task, explain what changed and why in plain language.
- Do not use em dashes or double hyphens as dashes in docs or comments.

## Roadmap

### Milestone 0: foundation
1. Build exactly as upstream documents: Go tests, web client build, run the
   server, open two browser tabs, confirm multiplayer works. Change nothing yet.
2. Read and summarise the codebase layout, protocol, and how rooms, players
   and saves work. Write findings to docs/notes/architecture.md.
3. Investigate which tests and fixtures depend on TOWN.ZZT or Epic help files.
   Report before removing anything, since replay tests may rely on them.
4. Plan the removal of: Museum of ZZT search, Epic content, and decide with
   Aisling whether the AI "dream world" generator and daily challenge stay.
5. Rename the project once a name is chosen.

### Milestone 1: log in and spawn into a hub
- Persistence layer using SQLite: player and character data survives restarts.
- Accounts: registration, login, securely hashed passwords, sessions.
- Characters: name, colour, persistent health, ammo, gems, torches, keys, and
  last location.
- Character creation screen in the client.
- A purpose-built sample hub board that every player spawns into.

Acceptance test: two accounts in two browser tabs each create a character,
both spawn into the hub and can see each other, log out and back in with state
restored, and characters survive a server restart.

### Later milestones (order may change)
- New world format: wider glyph codes, richer colour, per-player state.
- Level 2 renderer and the built-in pixel art and palette tool.
- Hub portals to other worlds; shared persistent worlds and private instances.
- Multiplayer-aware ZZT-OOP: which player triggered an event, per-player flags.
- Moderation: admin roles, kick, ban, mute, chat rate limits, reporting.
- Public deployment with HTTPS.
- Level 3 effects.
- Scaling, only if real player numbers call for it.

## Open questions
- Project name.
- Shared versus per-player puzzle state (do doors stay open for everyone?).
- Authentication approach (local accounts first; anything else later?).
