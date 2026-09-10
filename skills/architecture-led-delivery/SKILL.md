---
name: architecture-led-delivery
description: Implement and verify changes against maintained architecture authority, with one accountable agent and optional bounded delegation. Use for implementation work with authoritative architecture sources, not planning-only requests or work without maintained architecture authority.
---

# Architecture-led delivery

Deliver a locally integrated, verified change. The root is the owner: it may design, update architecture, implement, review, and integrate directly.

## Choose the smallest workflow

Work directly unless a bounded subtask benefits materially from separate context, expertise, or parallel execution. Large repositories, multiple repositories, and worktree isolation do not themselves require delegation. Keep tightly coupled reasoning and implementation together.

When delegation helps, dispatch workers or explorers directly. Add an architect only for a substantial domain that needs its own design and acceptance authority. The architect may implement directly; it need not dispatch workers. State the reason for delegation briefly, without formal mode declarations or mandatory design templates.

Read [agent-contracts.md](references/agent-contracts.md) only when delegating. Use a compact brief and return evidence, not repeated copies of the whole task history.

The root chooses between `worker_luna` and `worker` using its judgment about task complexity, uncertainty, verification, and cost. See the agent contracts for their settings and shared boundaries.

## Establish scope and authority

Before editing, inspect the relevant flow, repository instructions, architecture sources, and tests. Record the affected repositories, worktree paths, branches, HEADs, existing changes, and intended integration targets. Include untracked work that must be preserved. Identify the exact architecture revision and any relevant uncommitted architecture changes. Inspect dependency, remote, or runtime state only where it affects the operation.

Keep the initial state and track intentional changes well enough to distinguish them from drift. Recheck affected state at handoff, before integration or cleanup, and before operations whose safety depends on it. A continuous local edit does not need a repeated global inventory. Pause affected work on unexplained drift or conflicting authority; never overwrite it to restore an expected baseline.

Resolve the outcome, important invariants, architecture impact, and acceptance checks before dependent implementation. Scale design detail to uncertainty and failure impact. Missing authority blocks dependent work; implementation evidence does not replace it.

The root owns cross-cutting architecture decisions and documents. It may assign specific architecture pages and decisions to an architect. Keep one responsible author per page. Product workers do not edit architecture authority; they report gaps to their supervisor. The root or assigned architect resolves and records the decision before dependent work proceeds. Respect project rules for Current and Proposed states; working code does not automatically promote a proposal.

## Implement and verify

Make the smallest correct change. The responsible agent reviews the actual diff and relevant surrounding behavior, including contracts, validation, security, accessibility, data safety, and regressions where affected. Delegated work needs the supervisor's review; a worker summary or passing tests alone is not acceptance. Add independent review when risk or uncertainty warrants it, not as a ritual for every change.

Run the required checks and focused behavioral verification. Use the project readiness runbook when runtime behavior, containers, migrations, or deployment configuration are affected. Verify configuration before creating resources; use the intended source revisions and isolated task identity where needed. Verify applicable builds, migrations, seed, health, endpoints, and changed live scenarios. Explain missing runtime evidence or why runtime checks are unnecessary. Do not rebuild unrelated stacks.

For corrections, reuse the same worker while its context remains useful. After one substantive failed correction, reassess the brief, evidence, and model. Repeated conceptual failures call for a stronger agent or direct root implementation, not an unbounded retry loop. Transfer mutation ownership before taking over.

## Isolation and integration

Choose worktree isolation separately from delegation. Use the current worktree when safe and permitted; create isolated task worktrees when repository rules, parallel writes, or protection of existing work require them. The root manages task worktrees and their lifecycle.

Keep one mutating actor per worktree. Independent writers may share a repository only through separate worktrees with clear boundaries. Serialize changes that share contracts, architecture pages, generated outputs, migrations, runtime resources, or data. Give dependent work an accepted exact prerequisite revision or immutable input.

The root integrates accepted changes in dependency order and reviews the combined result. Incremental integration is allowed when prerequisites are accepted and intermediate states are safe. Incorporate the governing architecture before dependent product integration. Resolve semantic conflicts as design decisions and reverify affected behavior. Do not require a separate integration worker or a global wait for unrelated slices.

Before integration across repositories, establish exact inputs, target states, order, and safe recovery points. If it fails, stop dependent actions and recover only task-owned changes when this can preserve user work. Never reset through drift or perform destructive rollback without authorization. Report partial state and retain recovery evidence when safe recovery is blocked. Completion requires verification of the actual combined targets, not just isolated slices.

## Completion and cleanup

The root accepts the result only after required checks pass and no blocker or major finding remains. Record the disposition of smaller findings and unavailable evidence. Report the outcome, relevant architecture changes, actual branches/worktrees and revisions, verification, and material remaining risks. Include integration or rollback details only when applicable.

After acceptance, the root may remove task-created resources that are no longer needed for review or recovery. Recheck ownership and state first. Remove only clean, inactive, noncanonical task worktrees whose changes are integrated or preserved in accepted recovery evidence; remove worktrees before their task branches. Never force-remove dirty, drifted, unintegrated, current, canonical, or user-owned work. Remove only exact task containers and nonshared task networks whose use has ended. Preserve volumes and databases unless deletion is explicitly authorized. Report removed resources and retained exceptions.

This skill grants no additional authorization for remote mutation, publication, deployment, destructive operations, or discarding user work. Honor authorization already given; request missing authorization only for the affected action.

## Local browser delivery on the homeserver

When delivering runnable browser work on Bence's homeserver, apply `/home/benceb/.codex/skills/tailscale-service-delivery/SKILL.md`. Use the project's existing native or Compose runtime and hand off a verified persistent HTTPS `.dev.benceb.hu` URL. Containers are optional. Respect the project's architecture and isolation rules; the local delivery convention does not grant permission for unrelated or public deployments.
