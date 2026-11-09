# dylan/skills

Plugins and agent skills by Dylan. Each plugin installs into Claude Code from this marketplace, and its skills also install into Codex, Cursor and the other coding agents that the [`skills` CLI](https://github.com/vercel-labs/skills) supports.

## Install

In Claude Code, add the marketplace once, then install plugins by name:

```sh
/plugin marketplace add dylan/skills
/plugin install rigor@dylan
```

In any agent, install skills with `npx skills`. Name a skill with `--skill`, or leave it out to pick from a list:

```sh
npx skills add dylan/skills --skill deepen
```

The `skills` CLI installs skills only. A plugin's agents stay in the Claude Code version, and each section below says when a plugin depends on one.

## swift-api-design

Enforces the [Swift API Design Guidelines](https://www.swift.org/documentation/api-design-guidelines/) whenever you write, review or design Swift code.

```sh
/plugin install swift-api-design@dylan    # Claude Code
npx skills add dylan/skills --skill swift-api-design    # any agent
```

The skill applies the guidelines at every scope, from public APIs down to internal helpers, local functions, closures and tuple members. For each violation, it names the guideline broken and gives a concrete rewrite, without hedging. It checks:

- Naming: clarity at the call site, names that state a role instead of a type, fluent call sites, and Boolean names that read as assertions.
- Argument labels: prepositional and grammatical phrases, and the dropped first label on value-preserving conversions.
- Conventions: casing, factory methods, mutating and nonmutating pairs, and protocol names.
- Documentation: whether doc comments exist and say enough.
- Overloads: ambiguous overload sets involving `Any` or unconstrained generics.

The skill stays within the guidelines, so it doesn't judge protocol-oriented design, generics architecture, performance or memory management.

## nato-name

Picks an unused NATO reporting name as a placeholder project name, so you can start building before you've named the thing.

```sh
/plugin install nato-name@dylan    # Claude Code
npx skills add dylan/skills --skill nato-name    # any agent
```

The `/nato-name` skill lists every NATO reporting name (Flanker, Akula, Atoll, Kitchen and so on) that the current directory doesn't already use, and offers the first one. Because the list is alphabetical, it offers A-names first and moves to the next letter as you use them up. Ask for a letter to filter the list.

## c64

A Commodore 64 demoscene optimizer and hardware reference for any C64 project and toolchain: hand-written assembly (ca65, ACME, KickAssembler, 64tass, DASM), C through cc65 or llvm-mos, or Zig through zig-mos.

```sh
/plugin install c64@dylan    # Claude Code
npx skills add dylan/skills --skill c64-hardware    # any agent
```

The `c64` agent, which comes only with the Claude Code plugin, plans and reviews 6502/6510 code the way a demo group reviews a routine before the party deadline. Before you write a hot routine, a raster or interrupt scheme, a memory map or an effect, it picks the approach that fits a cycle and byte budget. After a change, it reviews cycle counts, raster timing, memory layout and how the code holds up on real hardware, and returns findings with concrete rewrites. It reads each project's toolchain and memory map from the project's own briefing, and it never edits files.

The `c64-hardware` skill gives exact numbers instead of recalled ones. The agent preloads it, any session can use it, and `npx skills` installs it without the agent. It holds these references:

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
npx skills add dylan/skills --skill deepen    # any agent
npx skills add dylan/skills --skill narrow    # any agent
npx skills add dylan/skills --skill prove    # any agent
```

The `/deepen` skill rewrites a prompt so the work goes deeper without growing. It names the professional whose standards apply and answers four questions as that person: what they would do that the prompt doesn't ask for, the rawest material they would start from, the methods and tools they would use, and a check outside you and the agent that would show the result is right. It then rewrites the prompt to ask for exactly that, and offers to run it.

The `/narrow` skill cuts a sprawling prompt down to the question that matters. It names the real question, what the professional would refuse to do, what can be cut or deferred, and the smallest result that would settle the question. The rewritten prompt ends with a list of everything deferred, so you can see every cut. When a task is both too broad and too shallow, run `/narrow` first and then `/deepen`.

The `/prove` skill tests finished work. It splits a result into testable claims and picks a check for each that can fail: running the code, taking a measurement, a known-answer case or the primary source. It writes down each pass condition before running the check. Each claim comes back passed, failed or unverified, and a check that didn't run never counts as a pass. It leaves fixes to you.
