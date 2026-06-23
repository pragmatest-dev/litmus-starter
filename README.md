# Litmus starter

A clean GitHub Codespace for building your own hardware-test solution with
[Litmus](https://github.com/pragmatest-dev/litmus) — no local install, no
hardware.

This repo is **not** the Litmus source. It's a [template
repository](https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template):
you make your own copy, and it becomes your project.

## Use it

1. Click **Use this template ▸ Create a new repository** (or **Create a
   codespace** to try it without keeping a repo).
2. In the new repo: **Code ▸ Codespaces ▸ Create codespace.**

The container installs the latest `litmus-test` and scaffolds a starter
project against **mock instruments** right in the workspace root.

## First commands

```bash
pytest                         # tests pass against mock instruments
litmus runs                    # the runs those tests produced
litmus serve --host 0.0.0.0    # operator UI; port 8000 auto-forwards
```

Bind `0.0.0.0` so the forwarded port resolves through the Codespaces proxy.
Then edit the tests and station YAML, commit, and it's your solution.

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
