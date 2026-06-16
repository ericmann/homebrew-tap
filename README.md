# 🍺 ericmann/homebrew-tap

A personal [Homebrew](https://brew.sh) tap for [Eric Mann](https://github.com/ericmann)'s tools. Small, sharp, local-first.

## What's on tap

| Cask | What it pours |
| --- | --- |
| [`journal`](https://github.com/ericmann/journal) | A local-first developer journal — semantic search and AI synthesis over your notes, running entirely on your machine. |

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

Cloud synthesis (`journal synth`) is optional and needs an `ANTHROPIC_API_KEY` — but `journal` runs fully local too (`synth_provider: ollama`). The full story lives in the [journal docs](https://github.com/ericmann/journal#readme).

## House rules

- Casks here are built and published automatically by [GoReleaser](https://goreleaser.com) on each tagged release — please don't hand-edit `Casks/*.rb`; they'll be overwritten.
- macOS binaries are ad-hoc signed, not Apple-notarized. The cask strips the quarantine flag on install, so the first run isn't blocked by Gatekeeper.

---

<sub>🚚 Moved here from <code>displacetech/tap</code> as of <code>journal</code> v2.4.1. The old tap is deprecated — update with <code>brew install ericmann/tap/journal</code>.</sub>
