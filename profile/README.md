# VistA-Copilot

**AI-integrated developer tools for VistA.**

VistA — the VA's nationwide electronic healthcare platform — is one of the largest and
longest-lived health IT systems in the world: tens of thousands of routines and globals,
thousands of FileMan files, RPCs, options, and KIDS builds, and a corresponding vast
documentation corpus. That depth is exactly what makes it hard to *start* working
on. VistA-Copilot builds tools that close that gap - bringing the whole system - 
code and data and documentation, into a single tool that developers 
(and their AI assistants) use directly within their workflow.

Our tools are built so that **humans and AI read VistA the same way**: every
capability is exposed as a CLI command, an AI/MCP tool, a REST endpoint, a web
form, and an interactive TUI — all generated from one typed source of truth, so a
human in a terminal and an agent over MCP get identical, structured answers.

<p align="center">
  <img src="https://github.com/VistA-Copilot/vista-info-hub/raw/master/demo/vista.gif" alt="vista browser — interactive arrow-key exploration of VistA code and data" width="850">
</p>

<p align="center"><em><code>vista browser</code> — walk packages → routines → the call graph → globals → docs, all from the keyboard.</em></p>

## One definition, every interface

`vista` reads the VistA code-model, data-model and VA Document Library into a
single **operation registry** of typed handlers, then projects that one definition
into five interfaces — so the CLI, an AI agent over MCP, a REST client, a web form
and the TUI all get identical, structured answers and can never drift apart:

```text
                        vista · one static binary, many faces
                                          │ reads the VistA code-model,
                                          │ data-model & VA Document Library
                     ┌─────────────────────────────────────────┐
                     │           operation registry            │
                     │     typed  Input → Handler → Output     │
                     │           one source of truth           │
                     └────────────────────┴────────────────────┘
                                          │ projected into 5 interfaces
          ┌───────────────┬───────────────┼───────────────┬───────────────┐
          ▼               ▼               ▼               ▼               ▼
         CLI             TUI            REST             Web          AI · MCP
     vista <op>      vista menu      POST /op/{}     forms at /       serve mcp
    → JSON / TSV      + browser       + OpenAPI     + HTML frags     → MCP tools

  command tree — every leaf is also an MCP tool, a REST op, a web form & a TUI entry
  ──────────────────────────────────────────────────────────────────────────────────
  vista
  ├─ inspect a routine      routine  where  neighbors  risk  links
  ├─ packages & catalogs    package  list  tree  layers  matrix
  ├─ rpcs · options · files rpc  option  file  global
  ├─ documentation          doc  search  coverage
  ├─ patches & history      patch  timeline
  ├─ ai bundles             context  ask
  ├─ data management        init  doctor  cache  snapshot
  ├─ introspection          commands  schema  llms
  └─ other faces            serve  menu  browser
```

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
vista browser               # interactive, ranger-style explorer (shown above)
vista tui                   # fuzzy-find palette over every operation
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
`vista browser` — it's the fastest way to get your bearings.
