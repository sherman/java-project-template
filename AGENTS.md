## Navigation

| Area of work | File to read |
| -------- | -------- |
| Coding standard | CODING_STANDARDS.md |


## Review conditions

If package-info.java declares @NonNullByDefault, all parameters, return values, and fields are non-null unless explicitly annotated with @Nullable. Reviews must enforce this contract.

## Context management

Protect the primary agent context from repository exploration noise.

Before substantive repository exploration, state the initial scope and delegation
decision in the first progress update.

Start with applicable instructions and obvious entry points. When repository
changes are relevant, inspect path-scoped status and diffs. Use targeted searches
and narrow file excerpts. Avoid loading unfiltered repository-wide results, full
logs, generated files, or entire large files when filtered output is sufficient.

Delegate broad, cross-module, or unfamiliar exploration as a bounded, read-only
task when subagent capacity is available. Treat search and file counts as
heuristics, not hard thresholds. When no subagent capacity is available,
explore incrementally and keep searches and output scoped.

Use the `explorer` agent defined in
[.codex/agents/explorer.toml](.codex/agents/explorer.toml)
for delegated repository exploration. Provide a self-contained task with
relevant context and constraints. If named-agent selection is unavailable,
read that configuration and apply its model, reasoning effort, and instructions
explicitly with `fork_turns: "none"`.

Before expanding beyond path-scoped status, diffs, and obvious entry points,
reassess the cumulative exploration scope. If it is broad, cross-module, or
unfamiliar and subagent capacity is available, stop further primary-agent
exploration and delegate a bounded, read-only task. A sequence of individually
targeted reads can still constitute broad exploration.

Explorers should report concise conclusions, relevant paths, symbols, line
references, uncertainties, and the small set of files the primary agent should
inspect next—not raw output or non-decision-relevant evidence.

The primary agent remains responsible for understanding the user's requirements,
architectural reasoning, decisions, implementation, and final verification. It
must inspect every file it changes and independently validate decision-critical
findings. It need not repeat non-critical exploratory work.

## Gradle dependencies management

When adding or updating dependencies, read and follow [GRADLE.md](GRADLE.md).

## Worklog

Keep one worklog of the goal, current instructions, owners, unfinished work, and decisions. Reconcile new guidance with work already underway and update the relevant entries. Record decisions and their consequences, and notify affected agents directly, one-to-one. After compaction or handoff, read the worklog and check current state before continuing.
