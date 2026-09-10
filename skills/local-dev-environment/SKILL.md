---
name: local-dev-environment
description: Create, reuse, rebuild, or stop a local development, test, or review environment using the project's native runtime or Docker Compose. Use for runnable environments, source/data isolation, readiness, and lifecycle management; not production or unrelated shared infrastructure.
---

# Local dev environment

Use the smallest environment that proves the requested behavior. Root owns sources, runtime, readiness, and lifecycle; this skill adds no delegation stages.

For browser delivery on Bence's homeserver, read [tailscale-service-delivery](../tailscale-service-delivery/SKILL.md) before provisioning so routing requirements enter the original configuration. Both skills use the same environment without an agent handoff or a second delivery stack. Headless tests need no Tailscale routing.

## Choose scope and lifetime

Read relevant repository instructions, setup documentation, and runtime runbooks. Inspect the affected sources, configuration, and existing resources. Follow project conventions; missing setup permits the smallest in-scope configuration, documentation, or ignore-rule additions, not unrelated infrastructure or data changes.

Reuse a suitable task environment. Status or resume requests do not require a new one. Choose temporary testing or retained review lifetime before starting. Prefer the project's existing native or Compose runtime; do not introduce Docker merely for a hostname. Retained services use an existing supervisor, or systemd for a simple native app, with appropriate restart/startup settings. Temporary tests need no boot service.

## Select sources without losing work

Use the appropriate existing workspace when safe. Create a task worktree before editing when repository rules, concurrent writers, or protection of existing work require one. Preserve intended uncommitted edits; do not commit or switch to a clean checkout merely to build. Any newly selected workspace must contain the changes being tested without moving or discarding unrelated work.

Record relevant paths, branches/revisions, and intended uncommitted changes. Recheck affected state at handoff and before operations whose safety depends on it. Stop on unexplained drift, not expected edits. Keep writable build output out of unrelated workspaces.

Reuse unchanged dependency sources when suitable. Read-only bind mounts do not freeze host-side edits. Use a pinned image, snapshot, or separate worktree when stable inputs are needed, even for an unchanged repository. Record actual tested inputs; HEAD alone does not describe uncommitted changes.

## Configure the environment

Keep setup in project-owned configuration. Give new environments distinct runtime identities, endpoints, writable paths, and data resources; verify ownership before reuse. Native upstreams use unique loopback ports unless established routing requires otherwise. For Compose, use project-scoped names rather than fixed container names or global task-volume names. Avoid cross-task writable mounts; only the necessary frontend joins an existing shared proxy network.

Follow the project's environment/secret-loading convention, not a mandatory single `.env`. Keep local secret files ignored and access-restricted (`0600` on Unix). Use approved secret sources; do not print secrets or blindly copy another task's environment.

Use consistent workspace, Compose files, project identity, profiles, and environment inputs across commands; pass the project identity explicitly. Validate with `docker compose config --quiet`, then inspect relevant resolved settings without exposing secrets. Account for shell overrides and service-level configuration. Before startup or data mutation, check effective source paths, mounts, ports, resource names, and database destinations. Syntax validation alone does not establish safe destinations.

Use named volumes or explicit task-owned data paths for state that must survive recreation. Rebuilding or restarting the assigned environment is normal within requested work, not permission to purge data or replace unrelated services.

## Start and verify

Inspect automatic initialization, migrations, and seeds before startup: confirm data ownership and whether operations are destructive. Reuse known task data where appropriate; resets need separate authorization or an applicable development-only reset guard.

Run the project's build, dependency, migration, seed, and readiness sequence for the selected scope. Use `docker compose up --build --wait` when supported and appropriate, or the documented alternative. Do not rebuild unrelated stacks. Verify relevant dependencies, checks, and changed behavior through tests and a live endpoint or operation. Running containers or a listening port alone do not prove readiness. For browser delivery, verify the same environment through its delivered URL. Report missing evidence.

## Retain or clean up

Leave retained review services running unless requested otherwise. Preserve their source worktrees, configuration, and data for operation and restart. Merged changes do not make a runtime-dependent worktree disposable. Verify any replacement before retiring its predecessor.

Temporary task test processes may be stopped after checks. Remove task-owned disposable runtime resources only when cleanup is in scope; retain useful failure evidence. Stopping and ordinary teardown must preserve data. Purge requires separate authorization; avoid volume-removal options and broad prune commands. Before worktree cleanup, check Git state and runtime dependencies; never force-remove dirty, unexplained, or unintegrated work. Preserve shared proxy resources.

Keep one concise environment record in existing project documentation for retained services, or the handoff for temporary tests. Include source state, runtime identity, endpoint, retained dependencies, verification results and gaps, and exact status/log/start/resume/stop and applicable teardown commands. Distinguish data purge from teardown. The Tailscale skill adds routing details to this same record.
