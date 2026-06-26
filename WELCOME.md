# 👋 Welcome — you're running Litmus

This codespace has Litmus installed and a starter project scaffolded against
**mock instruments**. No hardware, nothing to install. Here's the 30-second
tour.

## Start the operator UI

Run it yourself — one command:

```bash
litmus serve --host 0.0.0.0
```

When it binds port 8000, the forwarded port opens in a tab. That command *is*
the UI — the same one you'd run on your own machine.

## What to try

No hardware needed — everything here runs on mock instruments:

1. **Run the tests** — `pytest`. The example test passes; its limit is checked
   and the result recorded. Then `litmus runs` to list it.
2. **Browse the operator UI** — run `litmus serve --host 0.0.0.0`, then open
   port 8000: runs, measurements, and the metrics page (yield, Ppk, Pareto).
3. **Author a test** — add a pytest function and edit the station YAML in
   `stations/`, then re-run. That edit-run loop is test development.
4. **Drive it with AI** — open Copilot Chat in **agent mode** and ask about
   your runs; it calls Litmus's MCP tools. (Needs Copilot access.)

**Where the sandbox stops:** real instrument control — PyVISA/serial to an
actual bench — needs a local install. See *On your own machine* below.

## Keep your work (and keep it private)

This codespace is a **sandbox** — your changes live only here until you publish.
To save it: open **Source Control** ▸ **Publish to GitHub** ▸ choose **Private**.
That creates your own repo from the codespace. Nothing is on GitHub until then,
so sensitive specs stay off GitHub unless you publish (choose **Private**).

## On your own machine

Exactly the same, no codespace required:

```bash
pip install litmus-test     # PyPI package; the import name is `litmus`
litmus init --starter
pytest
litmus serve               # operator UI at http://localhost:8000
```

For an always-on UI, run `litmus serve` as a service — see the
[README](./README.md#running-the-operator-ui).
