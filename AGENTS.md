Use plain language and short sentences.

## Implementation

Before coding, inspect the relevant flow and repository instructions. Fix the root cause with the smallest correct change. Reuse existing patterns, platform features, standard-library tools, and installed dependencies. Avoid speculative abstractions, boilerplate, and unnecessary files or dependencies. Preserve unrelated work, correctness, security, validation, accessibility, and data safety.

## Code understanding

Prefer Serena for symbol lookup, reference tracing, and targeted code reading when available. Read its initial instructions once and activate the correct repository or worktree. Request only the symbol bodies needed; avoid whole-file reads. Use `rg` for simple text searches or when Serena is unavailable.

## Tool calls

In Code Mode, batch independent, functions.exec-available calls within each bounded stage into one functions.exec. Use await Promise.allSettled([...]) when partial results are useful and inspect every result; use await Promise.all([...]) only when any failure should abort the batch. Keep dependent operations, waits, approvals, conflicting mutations, and investigations whose results determine the next step sequential.

## Delegation

Work directly unless a bounded subtask materially benefits from separate context or parallel execution. These rules apply independently of skills.

When spawning agents, briefly tell the user which profile, model, and reasoning effort each uses and what it will handle. Combine announcements for a batch into one concise update.

Use the `explorer` profile (Luna, read-only) for precise source discovery and extraction. Do trivial lookups directly. Handle ambiguous causal analysis in the root or with a stronger agent. Use the `architect` profile (Astra) for delegated architecture and planning.

Spawn with `fork_turns: "none"` and a compact brief containing the task, relevant sources, boundaries, and acceptance criteria. Request concise evidence, source references, and uncertainty. Read decisive sources when needed for judgment. Reuse an agent for related follow-up while its context remains useful; use a fresh agent for independent work. Keep delegation shallow.

While agents run, do useful independent work or use the available blocking wait within client responsiveness limits. Batch follow-ups; avoid repeated status checks, progress pings, and full-history reads for status. Keep bulky logs out of the root context.
