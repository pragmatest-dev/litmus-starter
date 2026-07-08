# Litmus starter

A clean GitHub Codespace for building your own hardware-test solution with
[Litmus](https://github.com/pragmatest-dev/litmus) — no local install, no
hardware.

This repo is **not** the Litmus source. It's a [template
repository](https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template):
you make your own copy, and it becomes your project.

## Use it

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/pragmatest-dev/litmus-starter)

Click the badge (or **Use this template ▸ Open in a codespace**). A codespace
boots with the latest `litmus-test` installed and a starter project scaffolded
against **mock instruments** — no local install, no hardware. A getting-started
task prints the commands to run in a terminal when the workspace opens.

It's a **sandbox**: nothing lands on GitHub until you publish it. See
[Keep your work](#keep-your-work) below.

## First commands

From the terminal:

```bash
pytest                         # tests pass against mock instruments
litmus runs                    # the runs those tests produced
litmus serve                   # operator UI on forwarded port 8000
```

Edit the tests and station YAML and re-run — that loop is your test development.

## Running the operator UI

In a codespace, run `litmus serve` in a terminal — when it launches, the forwarded 
port opens in a tab.

On your own machine it's identical:

```bash
litmus serve            # http://localhost:8000
```

For an always-on UI, run it under a process manager. A minimal systemd unit:

```ini
# /etc/systemd/system/litmus-serve.service
[Unit]
Description=Litmus operator UI
After=network.target

[Service]
WorkingDirectory=/path/to/your/project
ExecStart=/usr/local/bin/litmus serve --host 0.0.0.0 --port 8000
Restart=on-failure
User=youruser

[Install]
WantedBy=multi-user.target
```

```bash
sudo systemctl enable --now litmus-serve
```

Use the absolute path to `litmus` in `ExecStart` (find it with `which litmus`) —
systemd doesn't inherit your shell's `PATH`. On macOS, the launchd equivalent
is a user agent running the same `litmus serve` command.

## Keep your work

This codespace is a **sandbox** — your changes live only here until you publish
them. Nothing is on GitHub until you do.

To save it as your own project: open the **Source Control** panel ▸ **Publish to
GitHub** ▸ choose **Private** (or Public). That creates a fresh repo from the
codespace — your solution, your visibility. If your test specs are sensitive,
choose **Private**.

(Just kicking the tires? Do nothing — delete the codespace and it's gone.)

## AI-ready (Copilot)

The codespace runs `litmus setup copilot` on create, wiring the project for
GitHub Copilot:

- `.github/copilot-instructions.md` and `AGENTS.md` — project context for
  Copilot (and Copilot CLI / other agents).
- `.github/skills/` — the packaged Litmus **Agent Skills**; Copilot reads their
  `SKILL.md` natively (VS Code / JetBrains agent mode, Copilot CLI, and the
  coding agent all discover them automatically).
- `.vscode/mcp.json` — the Litmus **MCP server** (`litmus mcp serve`), exposing
  your test data — runs, steps, measurements, channels, files, metrics — to
  Copilot's agent mode.

Open Copilot Chat, switch to **agent mode**, and ask about your test data.
(Requires Copilot access for your account or org; Codespaces must have Copilot
enabled.)

### Use Litmus MCP in any AI client

To wire Litmus's MCP server into any AI client by hand, give it this launcher
(`litmus-test` must be installed):

```json
{
  "command": "litmus",
  "args": ["mcp", "serve"]
}
```

`litmus setup claude-code | claude-desktop | copilot | cursor | codex | cline`
do it for you — each writes the MCP config in that tool's native location (plus
the skill and instruction files where the tool supports them).

## No drift

Nothing Litmus-specific is committed here — only `.devcontainer/`. The
starter project is generated at codespace-create time by the same
`litmus-test` version that was just installed, so the scaffold always
matches the release. There's nothing to rebuild when Litmus updates.

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
  litmus data prune --older-than 7d --dry-run   # preview
  litmus data prune --older-than 7d             # delete
  ```

`data/` is git-ignored, so it never bloats your repo. Deletion stays
manual on purpose — Litmus never removes run data behind your back.

## Maintainer note

For "Use this template" to appear, mark this repo as a template:
**Settings ▸ General ▸ Template repository.**
