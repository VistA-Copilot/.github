# VistA-Copilot

**AI-integrated developer tools for VistA.**

VistA — the VA's MUMPS-based electronic health record — is one of the largest and
longest-lived health IT systems in the world: thousands of routines and globals,
hundreds of FileMan files, RPCs, options, and KIDS builds, plus a sprawling
documentation corpus. That depth is exactly what makes it hard to *start* working
on. VistA-Copilot builds tools that close that gap — bringing the whole system,
code and data and docs alike, into the places developers (and their AI assistants)
already work.

Our tools are built so that **humans and AI read VistA the same way**: every
capability is exposed as a CLI command, an AI/MCP tool, a REST endpoint, a web
form, and an interactive TUI — all generated from one typed source of truth, so a
human in a terminal and an agent over MCP get identical, structured answers.

---

## Start here: the `vista` CLI

**[`vista-info-hub`](https://github.com/VistA-Copilot/vista-info-hub) is the
primary onboarding tool for new VistA developers.** It's a single static binary —
no runtime dependencies — that lets you explore *every code and data facet* of a
VistA system right in your normal workflow, without leaving the terminal.

```sh
go install github.com/VistA-Copilot/vista-info-hub/cmd/vista@latest
```

Point it at a VistA system and ask questions about how it actually fits together:

```sh
vista routine PRCA45PT      # code-model facts for a routine + the docs that describe it
vista package PRCA          # a package's namespaces, files, RPCs, options
vista file 200              # FileMan file structure (NEW PERSON), fields, globals
vista global DPT            # global usage across the code base
vista rpc XWB EGCHO STRING  # RPC availability, inputs, docs
vista search "sign-on"      # full-text search across the VA documentation corpus
vista context PRCA45PT      # an AI-ready markdown bundle: code facts + linked docs
vista tui                   # interactive operation palette — explore by browsing
```

Routines, RPCs, options, FileMan files, globals, patches, packages, and the VA
Document Library are all queryable — and *linked together*, so you can walk from a
routine to the globals it touches to the files those globals back to the docs that
explain them. Add `--json` (or `--ndjson` to stream) to any read command for
machine-readable output that drops straight into scripts and pipelines.

### Built for AI workflows, too

The same engine that powers the CLI runs as an **MCP server** (`vista serve mcp`),
so an AI coding assistant can call every read-only operation as a tool and reason
over a real VistA system with grounded, structured facts instead of guesses. One
operation registry projects into all faces — CLI, AI/MCP, REST, web, and TUI — so
they can't drift apart.

---

## Repositories

| Repo | What it is |
|------|------------|
| [`vista-info-hub`](https://github.com/VistA-Copilot/vista-info-hub) | The `vista` CLI / MCP / REST / web / TUI tool — start here. |

More tooling is on the way. If you're new to VistA, install the CLI and run
`vista tui` — it's the fastest way to get your bearings.
