# Bounded delegation

Use these rules only when a subtask warrants delegation. The root remains accountable for the combined result.

## Choose capability for the work

- Use Luna for clear extraction, focused source discovery, and mechanical changes with cheap, decisive checks.
- Use Terra for ordinary implementation and exploration that needs judgment.
- Use Astra for delegated architecture and planning. The root may do this work itself.
- Use Sol or Astra for difficult implementation, debugging, or review that needs deeper reasoning.
- For custom allocations, start with moderate reasoning effort and increase it for demonstrated difficulty. Named profiles use the settings below.

The local profiles are `explorer` (Luna, read-only, xhigh effort), `worker_luna` (Luna, xhigh effort), `worker` (Terra, medium effort), and `architect` (Astra, low effort). Both worker profiles follow the product-worker contract below. The root chooses between them based on task complexity, uncertainty, verification, and cost. Favor Luna for well-defined changes with decisive checks and Terra when more implementation judgment is needed; these are guidelines, not fixed routing rules.

The root owns the combined result; an architect may design and implement its assigned domain directly. Use `default` with an explicit model and effort for a different allocation, and supply the applicable boundaries below. Custom profiles can pin model settings; do not assume a spawn override changes them. An unavailable optional profile is not a blocker when the root can safely do the work.

## Brief and handoff

Spawn with `fork_turns: "none"`. Supply only:

- The concrete question or outcome, acceptance checks, and relevant instructions.
- Exact workspace paths, expected base and existing changes, dependencies, and source references.
- Allowed changes, no-touch boundaries, architecture authority, and who owns mutation.

The recipient checks its assigned state before mutation. It reports blockers instead of crossing boundaries. Return a concise result with changed files or source references, actual revisions and workspace state where relevant, verification commands and outcomes, uncertainty, and remaining risks. Keep bulky logs in artifacts and identify the evidence needed for review. Commit only when the repository workflow or task requires it.

**Product worker:** implement and verify the assigned scope. Architecture authority is no-touch. Report architecture gaps and semantic integration conflicts to the supervisor. Do not delegate, manage worktrees, clean resources, or broaden scope.

**Explorer:** answer a precise read-only question. Return paths, symbols, revisions, supporting evidence, coverage limits, contradictions, and unresolved questions. Separate findings from inference and Current from Proposed. Do not mutate files, refs, or runtime resources. The receiving agent reads decisive source material when needed for judgment; a summary is not a substitute for critical evidence.

**Architect:** own only the assigned domain's design, architecture pages, implementation, and acceptance. Implement directly or delegate a bounded worker when useful. Send cross-domain decisions to the root. Return actual diff and verification evidence; leave global integration and resource cleanup to the root. Do not create further supervisory layers.

## Coordinate with little overhead

Do useful independent work while agents run. Otherwise use the available blocking agent wait within client responsiveness limits. Avoid repeated status listings, full-history reads, and messages asking whether work is finished. Do not assume completion notifications eliminate model resumptions; use the wait behavior actually available in the client.

Report meaningful blockers, decisions, and completion. Batch correction findings. Reuse an agent for related follow-up; replace or escalate when its context or capability no longer fits. Never have a replacement and the previous agent mutate the same worktree concurrently.
