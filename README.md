# claude

Plugins and agent skills by Dylan. Each plugin installs into Claude Code from this marketplace, and its skills also install into Codex, Cursor and the other coding agents that the [`skills` CLI](https://github.com/vercel-labs/skills) supports.

## Install

In Claude Code, add the marketplace once, then install plugins by name:

```sh
/plugin marketplace add dylan/claude
/plugin install rigor@dylan
```

In any agent, install skills with `npx skills`. Name a skill with `--skill`, or leave it out to pick from a list:

```sh
npx skills add dylan/claude --skill deepen
```

The `skills` CLI installs skills only. A plugin's agents stay in the Claude Code version, and each section below says when a plugin depends on one.

## swift-api-design

Swift API Design Guidelines enforcer — active whenever you're writing, reviewing, or designing Swift code.

```sh
/plugin install swift-api-design@dylan    # Claude Code
npx skills add dylan/claude --skill swift-api-design    # any agent
```

Enforces the [Swift API Design Guidelines](https://www.swift.org/documentation/api-design-guidelines/) at every scope level — public APIs, internal helpers, local functions, closures, tuple members. Calls out violations with the specific guideline broken and a concrete rewrite. No hedging.

**What it covers:**
- Naming: clarity at the call site, role vs. type names, fluency, Boolean readability
- Argument labels: prepositional phrases, grammatical phrases, value-preserving conversions
- Conventions: casing, factory methods, mutating/nonmutating pairs, protocol naming
- Documentation: presence and quality of doc comments
- Overloads: ambiguous overload sets with `Any` or unconstrained generics

**What it doesn't cover:** Protocol-oriented design choices, generics architecture, performance, memory management. Guidelines scope only.

## nato-name

Placeholder project namer — picks an unused NATO reporting name so you can start building before you've named the thing.

```sh
/plugin install nato-name@dylan    # Claude Code
npx skills add dylan/claude --skill nato-name    # any agent
```

**`/nato-name` skill** — Lists every NATO reporting name (Flanker, Akula, Atoll, Kitchen, ...) not already used in the current directory and offers the first one. The list is alphabetical, so A-names go first and the letter advances as you use them up. Ask for a letter to filter.

## c64

Commodore 64 demoscene optimizer and hardware reference, for any C64 project and toolchain: hand-written assembly (ca65, ACME, KickAssembler, 64tass, DASM), C through cc65 or llvm-mos, or Zig through zig-mos.

```sh
/plugin install c64@dylan    # Claude Code
npx skills add dylan/claude --skill c64-hardware    # any agent
```

**`c64` agent** (Claude Code plugin only) — Plans and reviews 6502/6510 code the way a demo group reviews a routine before the party deadline. Before you write a hot routine, a raster or interrupt scheme, a memory map or an effect, it chooses the approach within a cycle and byte budget. After a change, it reviews the code for cycle counts, raster timing, memory layout and real-hardware resilience, and returns findings with concrete rewrites. It learns each project's toolchain and memory map from the project's own briefing, and it is read-only.

**`c64-hardware` skill** — Exact numbers instead of recalled ones, preloaded by the agent and available to any session. `npx skills` installs this skill without the agent:

| Reference | Covers |
|-----------|--------|
| `6510.md` | All 256 opcodes with cycle counts, grouped by stability; NMOS quirks |
| `vic-ii.md` | Registers, banks, display modes, raster-line cycle timing, badlines, sprites, border tricks |
| `cia.md`, `sid.md` | Timers, interrupts, keyboard and joysticks; SID registers, pitch and chip differences |
| `memory-map.md` | Banking, vectors, KERNAL interrupt costs, zero-page use, decruncher footprints |
| `interrupts.md` | Raster interrupt setup, acknowledging, missed lines, NMI ownership, stable-raster methods |
| `patterns.md` | Raster chains written as one routine, protothreads, long work inside interrupts |
| `algorithms.md` | Measured crunchers, loaders, multiply, random numbers, multiplexer sorts, and open opportunities |
| `llvm-mos.md` | llvm-mos and zig-mos: zero page, static stack, calling convention, interrupts, start-up, what compiles badly |
| `modern-practice.md` | Host-side cycle tests, headless VICE, a VICE test harness, Ultimate 64 REST API, build-time assertions |

## rigor

Holds tasks and their results to a professional's standard. Before the work, `/deepen` and `/narrow` rewrite the prompt; after it, `/prove` runs the check that could show the result is wrong.

```sh
/plugin install rigor@dylan    # Claude Code
npx skills add dylan/claude --skill deepen    # any agent
npx skills add dylan/claude --skill narrow    # any agent
npx skills add dylan/claude --skill prove    # any agent
```

**`/deepen` skill** — Rewrites a prompt so the work goes deeper without growing. It names the professional whose standards apply and answers four questions as that person: what they would do that the prompt doesn't ask for, the rawest material they would start from, the methods and tools they would use, and a check outside you and Claude that would show the result is right. It then rewrites the prompt to ask for exactly that, and offers to run it.

**`/narrow` skill** — Cuts a sprawling prompt down to the question that matters. It names the real question, what the professional would refuse to do, what can be cut or deferred, and the smallest result that would settle it. The rewritten prompt ends with a list of everything deferred, so nothing disappears unnoticed. When a task is both too broad and too shallow, run `/narrow` first and then `/deepen`.

**`/prove` skill** — Checks finished work by running checks instead of reviewing it. It splits a result into testable claims and picks a check for each that can fail: running the code, a measurement, a known-answer case or the primary source. It writes each pass condition down before running the check. Each claim comes back passed, failed or unverified, and a check that didn't run never counts as a pass. Fixes are left to you.
