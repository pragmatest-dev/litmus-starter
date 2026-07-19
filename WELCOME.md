# 👋 Welcome — you're running TesterKit

This codespace has TesterKit installed and a starter project scaffolded against
**mock instruments**. No hardware, nothing to install. Here's the 30-second
tour. TesterKit runs from the terminal and from the UI.

## Run the example test

```bash
pytest
```

## Start the operator UI

```bash
testerkit serve
```

When it launches, the forwarded port opens in a tab. That command *is*
the UI — the same one you'd run on your own machine. You can pop out the tab
into a new window.

## What to try

No hardware needed — everything here runs on mock instruments:

1. **Run the tests** — `pytest`. The example test passes; its limit is checked
   and the result recorded. Then `testerkit runs` to list it.
2. **Browse the operator UI** — run `testerkit serve`, then open port 8000: 
   check runs, measurements, and the metrics page (yield, Ppk, Pareto).
3. **Author a test** — check ou `tests/` and modify or add new pytests. Use
   the pytest extension to run and debug.
4. **Drive it with AI** — open Copilot Chat in **agent mode** and ask about
   your runs. It calls TesterKit's CLI and MCP tools. (Needs Copilot access.)

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
pip install testerkit     # PyPI package; the import name is `testerkit`
testerkit init --starter
pytest
testerkit serve               # operator UI at http://localhost:8000
```

For an always-on UI, run `testerkit serve` as a service — see the
[README](./README.md#running-the-operator-ui).
