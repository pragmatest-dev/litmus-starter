# 👋 Welcome — you're running Litmus

This codespace has Litmus installed and a starter project scaffolded against
**mock instruments**. No hardware, nothing to install. Here's the 30-second
tour.

## The operator UI is starting now

A terminal labeled **litmus serve** is running this command:

```bash
litmus serve --host 0.0.0.0
```

The UI opens automatically in a tab once it's up (port 8000). It's not magic —
that one command *is* the UI. Stop or restart it from the terminal anytime.

## Run the tests

```bash
pytest
```

Four tests pass against the mock power supply and DMM. Then see what they
recorded:

```bash
litmus runs
```

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
