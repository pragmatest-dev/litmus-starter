# TesterKit starter

A clean GitHub Codespace for building your own hardware-test solution with
[TesterKit](https://github.com/pragmatest-dev/testerkit) — no local install, no
hardware.

This repo is **not** the TesterKit source. It's a [template
repository](https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template):
you make your own copy, and it becomes your project.

## Use it

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/pragmatest-dev/testerkit-starter)

Click the badge (or **Use this template ▸ Open in a codespace**). A codespace
boots with the latest `testerkit` installed and a starter project scaffolded
against **mock instruments** — no local install, no hardware. A getting-started
task prints the commands to run in a terminal when the workspace opens.

It's a **sandbox**: nothing lands on GitHub until you publish it. See
[Keep your work](#keep-your-work) below.

## First commands

From the terminal:

```bash
pytest                         # tests pass against mock instruments
testerkit runs                    # the runs those tests produced
testerkit serve                   # operator UI on forwarded port 8000
```

Edit the tests and station YAML and re-run — that loop is your test development.

## Running the operator UI

In a codespace, run `testerkit serve` in a terminal — when it launches, the forwarded 
port opens in a tab.

On your own machine it's identical:

```bash
testerkit serve            # http://localhost:8000
```

For an always-on UI, run it under a process manager. A minimal systemd unit:

```ini
# /etc/systemd/system/testerkit-serve.service
[Unit]
Description=TesterKit operator UI
After=network.target

[Service]
WorkingDirectory=/path/to/your/project
ExecStart=/usr/local/bin/testerkit serve --host 0.0.0.0 --port 8000
Restart=on-failure
User=youruser

[Install]
WantedBy=multi-user.target
```

```bash
sudo systemctl enable --now testerkit-serve
```

Use the absolute path to `testerkit` in `ExecStart` (find it with `which testerkit`) —
systemd doesn't inherit your shell's `PATH`. On macOS, the launchd equivalent
is a user agent running the same `testerkit serve` command.

## Keep your work

This codespace is a **sandbox** — your changes live only here until you publish
them. Nothing is on GitHub until you do.

To save it as your own project: open the **Source Control** panel ▸ **Publish to
GitHub** ▸ choose **Private** (or Public). That creates a fresh repo from the
codespace — your solution, your visibility. If your test specs are sensitive,
choose **Private**.

(Just kicking the tires? Do nothing — delete the codespace and it's gone.)

## AI-ready (Copilot)

The codespace is already wired for GitHub Copilot on create — TesterKit's Agent
Skills, project instructions, and MCP server are installed for you. Nothing to
set up.

Open Copilot Chat, switch to **agent mode**, and ask about your test data — it
uses `testerkit runs`, the Query API, and the TesterKit MCP tools instead of poking at
files. (Requires Copilot access for your account or org; Codespaces must have
Copilot enabled.)

Using a different assistant (Claude, Cursor, Codex…)? Full per-tool setup lives
in the [TesterKit docs](https://github.com/pragmatest-dev/testerkit).

## No drift

Nothing TesterKit-specific is committed here — only `.devcontainer/`. The
starter project is generated at codespace-create time by the same
`testerkit` version that was just installed, so the scaffold always
matches the release. There's nothing to rebuild when TesterKit updates.

## Staying under storage limits

Codespaces bill storage by GB-month for the whole codespace — running *or*
stopped. Two independent levers:

- **Account storage (the big one):** set a **retention period** so idle
  codespaces auto-delete, at
  [github.com/settings/codespaces](https://github.com/settings/codespaces)
  (or via org policy). A forgotten stopped codespace keeps costing storage;
  pruning run data barely moves this.
- **Disk inside the codespace:** test runs accumulate under `data/`. Prune
  it explicitly when it grows — it's reference-aware and keeps anything a
  run still points at:

  ```bash
  testerkit data prune --older-than 7d --dry-run   # preview
  testerkit data prune --older-than 7d             # delete
  ```

`data/` is git-ignored, so it never bloats your repo. Deletion stays
manual on purpose — TesterKit never removes run data behind your back.

## Maintainer note

For "Use this template" to appear, mark this repo as a template:
**Settings ▸ General ▸ Template repository.**
