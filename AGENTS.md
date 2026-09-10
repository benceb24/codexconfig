Use plain language and short sentences.

## Implementation

Before coding, inspect the relevant flow and repository instructions. Fix the root cause with the smallest correct change. Reuse existing patterns, platform features, standard-library tools, and installed dependencies. Avoid speculative abstractions, boilerplate, and unnecessary files or dependencies. Preserve unrelated work, correctness, security, validation, accessibility, and data safety. Review the actual diff and relevant behavior, run focused checks, and report missing verification evidence.

## Code understanding

Prefer Serena for symbol lookup, reference tracing, and targeted code reading when available. Read its initial instructions once and activate the correct repository or worktree. Request only the symbol bodies needed; avoid whole-file reads. Use `rg` for simple text searches or when Serena is unavailable.

## Tool calls

In Code Mode, batch independent, functions.exec-available calls within each bounded stage into one functions.exec. Use await Promise.allSettled([...]) when partial results are useful and inspect every result; use await Promise.all([...]) only when any failure should abort the batch. Keep dependent operations, waits, approvals, conflicting mutations, and investigations whose results determine the next step sequential.

## Delegation

Root owns planning, implementation, verification, and integration. Work primarily in root; keep tightly coupled reasoning and changes together. Use the helpers below for routine support; otherwise delegate bounded work when separate context or an independent check improves quality. Parallelizability alone is not a reason to delegate. These rules apply independently of skills.

Use `explorer` for substantial source discovery and `executor` for routine shell batches. Keep trivial calls direct. Create helpers on demand and reuse one executor per workspace within the session for successive batches; do not close and respawn it after each result. Their operating rules live in their profiles.

For other delegated work, use `default` or `read_only` and select a supported model and reasoning effort by difficulty: Terra for ordinary tasks; Sol or Astra for difficult, ambiguous, or high-risk work. Reassess poorly matched assignments. Do not impose planning, implementation, or review stages.

Briefly announce the model, effort, and assignment; combine batch announcements. Spawn with `fork_turns: "none"` and a compact brief containing the outcome, relevant sources and expected workspace state, allowed changes, and acceptance criteria. For follow-ups, send only changed context and the next assignment. Subagents may delegate bounded support work to the specified Luna `explorer` and `executor` roles, following the same helper selection, announcement, briefing, and reuse rules. They must keep delegation within their assigned scope and must not delegate to other roles or broaden scope. Luna helpers do not redelegate.

Keep one mutating actor per worktree; use separate worktrees for concurrent writers and transfer ownership before taking over. Keep sources stable during verification and Git finalization. Root owns integration and worktree lifecycle; preserve unrelated work and stop on unexplained drift.

Request concise evidence, source references, verification, and uncertainty. Root reads decisive sources, reviews delegated diffs, and verifies the combined result before acceptance. Do not redo delegated work except where needed to verify it. Reuse related context while useful; replace stale or overloaded helpers.

While agents run, do useful independent work or use the available blocking wait within client responsiveness limits. Batch follow-ups; avoid repeated status checks, progress pings, and full-history reads for status. Keep bulky logs out of the root context.
