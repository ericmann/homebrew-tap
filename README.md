# 🍺 ericmann/homebrew-tap

A personal [Homebrew](https://brew.sh) tap for [Eric Mann](https://github.com/ericmann)'s tools. Small, sharp, local-first.

## What's on tap

| Cask | What it pours |
| --- | --- |
| [`journal`](https://github.com/ericmann/journal) | A local-first developer journal — local semantic search over your notes, plus AI synthesis via **cloud Claude or a fully local model**, your choice. |
| [`float-mcp`](https://github.com/ericmann/float-mcp) | A local stdio MCP server for [Float](https://www.float.com) time tracking — review and log your hours from Claude instead of the GUI. Your Float API token lives in the server config and **never enters the model's context**. |

## Install

```sh
brew install ericmann/tap/journal
```

That's shorthand for `brew tap ericmann/tap && brew install journal`. From then on, `brew upgrade` keeps it current.

### One thing first: journal wants a local Ollama

`journal` does its embedding and search locally via [Ollama](https://ollama.com) — nothing leaves your machine:

```sh
brew install ollama
ollama pull qwen3-embedding:4b
journal doctor          # tells you if anything's missing
```

Synthesis (`journal synth`) is optional and runs two ways: **cloud Claude** (Sonnet by default — set `ANTHROPIC_API_KEY`) or a **fully local Ollama model** (`synth_provider: ollama` — no key, zero egress). The full story lives in the [journal docs](https://github.com/ericmann/journal#readme).

## float-mcp

A local **stdio MCP server** that exposes [Float](https://www.float.com) time tracking — reviewing and logging time — as Model Context Protocol tools, so you can work your hours from Claude instead of the Float GUI.

```sh
brew install ericmann/tap/float-mcp
```

Then give it a Float API token and register it with your MCP client:

```sh
# Create a token in Float → Team Settings → Integrations (needs account-owner),
# then provide it via the FLOAT_API_TOKEN env var or ~/.config/float/config.json
float-mcp doctor                                          # verify your setup

claude mcp add float --env FLOAT_API_TOKEN=... -- float-mcp mcp
```

The token is held entirely in the server config — it never enters the model's context, and is never logged or returned in tool output.

## House rules

- Casks here are built and published automatically by [GoReleaser](https://goreleaser.com) on each tagged release — please don't hand-edit `Casks/*.rb`; they'll be overwritten.
- macOS binaries are ad-hoc signed, not Apple-notarized. The cask strips the quarantine flag on install, so the first run isn't blocked by Gatekeeper.
