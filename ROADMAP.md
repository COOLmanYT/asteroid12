# Asteroid12 — Project Roadmap

> A general-purpose, self-hosted Discord bot written in Python. Users host the
> bot themselves to allow maximum customization of commands, behavior, and
> integrations.

This roadmap captures the key milestones from the current empty-scaffold state
toward a stable, self-hostable, customizable release. Each milestone lists its
goal, scope, and a definition of "done." Milestones are sequential but later
ones can overlap; items within a milestone are not strictly ordered.

Status legend: ☐ not started · 🚧 in progress · ✅ done

---

## Milestone 0 — Project Foundation
**Goal:** Establish a runnable, documented, contributor-friendly skeleton.

Scope:
- ☐ Non-empty `bot.py` that boots a `discord.py` client and logs in from a
  `.env`-loaded token (`DISCORD_TOKEN`).
- ☐ `requirements.txt` / `pyproject.tom` pinning `discord.py` and a `.env`
  loader (e.g. `python-dotenv`).
- ☐ `README.md` with: what the bot is, how to self-host (create app, invite,
  set token, run), and Python version.
- ☐ `CONTRIBUTING.md` with branch/commit/PR conventions and local dev setup.
- ☐ `.gitignore` review (already covers `venv/`, `.env`, `__pycache__/`).
- ☐ Minimal CI: lint + import smoke test on push/PR.

**Done when:** Anyone can clone, set `DISCORD_TOKEN`, `python bot.py`, and see
the bot online in a test server; CI is green.

---

## Milestone 1 — Command Framework & Cog Architecture
**Goal:** A maintainable, extensible command structure.

Scope:
- ☐ Migrate from a single `bot.py` to a `cogs/` package with a loader that
  discovers and registers cogs at startup.
- ☐ Establish `bot.py` (or `main.py`) as the bootstrap: config load, intents,
  cog loading, graceful shutdown.
- ☐ Shared config module (`config.py` or `core/config.py`) reading from env /
  `.env` with sane defaults and documented options.
- ☐ A convention for per-cog help text and permissions.
- ☐ A sample "utility" cog (e.g. ping, info, uptime) demonstrating the
  pattern.

**Done when:** A new command can be added by dropping a cog file in `cogs/`
with no edits to the bootstrap; reload command works without restart.

---

## Milestone 2 — Configuration & Self-Hosting Story
**Goal:** Make customization and self-hosting first-class.

Scope:
- ☐ Documented environment variables for all tunable behavior.
- ☐ Optional config file (e.g. `config.yaml`/`config.toml`) layered over env,
  with documented schema.
- ☐ Per-guild settings store (owner opt-in) so hosts can enable/disable
  feature groups per server.
- ☐ A `!help` / slash-command help system that reflects enabled features.
- ☐ Hardening: token never logged, intents minimal, errors surfaced to host
  logs not chat.

**Done when:** A host can enable/disable feature groups and change behavior
without editing source; deployment docs cover venv, systemd, and Docker.

---

## Milestone 3 — Core Feature Cogs
**Goal:** Deliver the general-purpose feature set that defines the bot.

Scope (representative — owners choose which to enable):
- ☐ Moderation cog (kick/ban/mute, audit logging, role tools).
- ☐ Fun/utility cog (polls, reminders, dice, random).
- ☐ Information cog (user/server/role info, avatar lookup).
- ☐ Music/voice cog (if in scope) or clearly documented as optional extension.
- ☐ Per-cog tests where logic is testable (pure functions first).

**Done when:** Core feature group is usable end-to-end in a real server and
documented in the README feature list.

---

## Milestone 4 — Persistence & Data
**Goal:** Reliable, portable state for self-hosters.

Scope:
- ☐ Pluggable storage backend (default SQLite, optionally PostgreSQL) behind
  a single async data-access interface.
- ☐ Migrations/versioned schema for the default backend.
- ☐ Backup/export guidance for hosts.
- ☐ No secrets or PII logged; documented retention notes.

**Done when:** Settings, reminders, and moderation logs persist across
restarts; switching backends is documented.

---

## Milestone 5 — Slash Commands & UX Polish
**Goal:** Modern, discoverable interaction model.

Scope:
- ☐ Migrate interactive commands to Discord application/slash commands where
  appropriate, keeping prefix commands for host flexibility.
- ☐ Consistent embed styling and error messages.
- ☐ Rate-limit and cooldown handling.
- ☐ Accessible copy (clear wording, no emoji-only state).

**Done when:** Slash commands registered and visible in target servers; UX
reviewed against the feature set in Milestone 3.

---

## Milestone 6 — Quality, Testing & Release Readiness
**Goal:** Confidence to tag a stable release.

Scope:
- ☐ Unit tests for pure logic; integration smoke tests for boot + cog load.
- ☐ Linting + type checking enforced in CI (e.g. ruff, mypy).
- ☐ Changelog (`CHANGELOG.md`) and semantic versioning.
- ☐ Release packaging: versioned tags, GitHub Release notes, install
  instructions pinned to a version.
- ☐ Self-host deployment guide finalized (venv, Docker, systemd).

**Done when:** `v1.0.0` tagged with passing CI, a release artifact/notes, and
a host can deploy from the tag in under ~15 minutes.

---

## Milestone 7 — Community & Long-Term Maintenance
**Goal:** Sustainable project after first stable release.

Scope:
- ☐ Issue/PR templates and `CONTRIBUTING.md` finalized.
- ☐ Security policy (`SECURITY.md`) for responsible disclosure.
- ☐ Plugin/extension docs so self-hosters add their own cogs cleanly.
- ☐ Roadmap reviewed per release cycle.

**Done when:** Maintainers can triage contributions predictably and
self-hosters can write and load their own cogs from docs alone.

---

## How to update this roadmap
- Move items ☐ → ✅ as they ship; mark in-progress with 🚧.
- Add new milestones only for sizable new directions; small work belongs in an
  existing milestone or its own issue.
- Keep each milestone's "Done when" concrete and verifiable.
