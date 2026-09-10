---
name: isolated-dev-stack
description: Create or rebuild a testing-ready local Docker Compose development stack in the necessary Git worktrees, with isolated project identity, sources, data, and endpoints. Use when a coding task needs its own runnable development environment; do not use for production, shared, or preserved-data environments.
---

# Isolated Dev Stack

Use task-owned worktrees only for repositories changed by the task, then create the smallest stack that proves the requested behavior. Leave primary checkouts, existing containers, and existing data untouched.

## Read the project runbook first

Read the applicable `AGENTS.md` files, project setup documentation, and the authoritative project testing-readiness runbook before creating a worktree or container.

The project-owned runbook is the single source for:

- test scope, Compose profiles, and service selection;
- the location and required keys of the task environment;
- source paths for every repository used by the selected profile;
- migrations, seeds, health checks, endpoints, and readiness criteria;
- native commands for status, logs, resume, stop, and teardown.

Use the smallest profile and service set that proves the requested behavior. Project-specific profile names, routes, credentials, seed data, and startup order belong in that runbook, not in this generic skill.

Runbook specifics cannot weaken authorization, data safety, source isolation, or resource isolation. Stop on conflict and do not invent an alternate launch mechanism.

## Inspect and choose sources

- Inspect Git status, branches, worktrees, exact revisions, Compose files, profiles, migrations, seeds, running Compose projects, routes, and required external networks.
- Inventory each repository independently. Create or reuse a worktree only for a repository changed by the task.
- Reuse unchanged canonical sources at exact rechecked revisions and mount or consume them read-only where the tracked Compose contract permits.
- If an unchanged dependency needs writable source or build output, use a project-scoped image or volume defined by tracked Compose; otherwise stop and report the conflict.
- Treat changes in the primary checkout as user-owned. Do not move, copy, commit, clean, or discard them.
- If the request is only to inspect or resume an existing environment, do not create another one.

## Create the worktree and one environment

- Resolve the intended base branch or commit.
- Create a `codex/<task-slug>` branch and worktree only for a changed repository, or reuse a supplied clean task worktree whose branch and revision still match.
- Refuse to reuse an occupied branch, directory, or worktree without confirming that it is the same task.
- Run all task commands from the selected worktree.
- Use the project-owned tracked Compose file. Its parameters must express the selected source paths and task identity. If they cannot, stop and request an authorized implementation change before starting anything.
- Use one ignored task-local `.env` file with mode `0600`. It must contain the exact absolute source paths for all selected repositories and the complete identity and endpoint values required by the runbook.
- Recheck every dependency SHA, clean task-worktree state, protected state, and Compose owner immediately before configuration, build, and handoff.
- Never copy another worktree's environment or secrets. Never stage or commit `.env`. If the repository does not ignore it, stop and report the issue without changing ignore rules.

## Isolate Compose state

- Use the unique Compose project identity and endpoint values defined by the runbook. Pass the project identity explicitly to every native Compose command.
- Use either unique loopback ports or the existing external reverse-proxy network with a unique development hostname, according to the runbook.
- Ensure unique identity for the Compose project, containers, router and service labels, hostnames or ports, ordinary networks, application volumes, dependency volumes, upload volumes, and writable build output.
- Reject `container_name`, global application resource names, shared writable build trees, and cross-task writable bind mounts. The only intentionally shared network may be the external reverse-proxy network named by the runbook.
- Confirm every bind mount resolves inside the selected worktree or an explicitly approved read-only canonical source. Inspect Compose labels before reusing an existing project identity and refuse labels belonging to another working directory.

## Validate, start, and seed

- Validate the fully resolved tracked configuration with `docker compose config --quiet` before creating containers.
- Inspect whether initialization, migrations, and seeds are idempotent or destructive. Use only new isolated resources for task data.
- Start dependencies in the order required by the runbook. Run the documented project migration and seed commands with the task environment.
- Use `docker compose up --build --wait` when the installed Compose version supports it. If it does not, use the runbook's native readiness sequence and report the limitation.
- Verify build completion, migration result, seed result or `N/A` with a reason, container health, application endpoints, database or supporting-service access, Compose labels, source revisions, and isolation of containers, networks, volumes, and writable output.

Testing readiness requires evidence for the selected scope, profile, Compose project identity, source revisions, build, migrations, seed or `N/A`, health, endpoint reachability, labels, and isolation. A process listing or direct port check alone is not readiness evidence.

## Lifecycle safety

Status and logs are non-mutating. Stop preserves task data and resources. Teardown removes only task containers and networks after cleanup authorization; volume or database purge is a separate destructive action. If readiness fails, preserve the worktree, containers, volumes, logs, and evidence unless cleanup is explicitly authorized.

Keep the worktree, containers, and volumes after handoff unless cleanup is authorized. Treat volume deletion, database reset, and resource replacement as separate destructive actions requiring explicit authorization or an existing development-only reset guard.

## Report the environment

Return:

- worktree path, branch, and exact base revision;
- selected test scope, profile, and services;
- `.env` path without its values and Compose project name;
- source paths and revisions without secrets;
- named resources and endpoints or hostnames;
- build, migration, seed or `N/A`, health, label, and isolation evidence;
- exact native Compose commands for status, logs, resume, stop, and teardown;
- retained worktrees, containers, volumes, and any limitation or risk.
