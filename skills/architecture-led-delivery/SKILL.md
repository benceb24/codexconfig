---
name: architecture-led-delivery
description: Create and maintain concise, source-linked architecture maps for future context. Use for architecture mapping or design requests and changes to component boundaries, contracts, or key flows, including projects without existing maps. Do not use for routine edits with no architectural impact.
---

# Architecture-led delivery

Preserve the understanding needed to navigate and change the system in later sessions. Root owns architectural decisions and synthesis. Follow the general delegation instructions; this skill adds no agent hierarchy or delivery stages.

## Establish the relevant picture

Read repository instructions, existing architecture documentation and decisions, and the relevant implementation and tests. Follow the project's documentation conventions. Treat maps as navigation, not a substitute for inspecting decisive sources. Check the relevant revisions and uncommitted changes when they affect interpretation.

Separate descriptions of the current implementation from approved constraints, proposals, and unresolved questions. Code establishes what exists; project decisions establish what is permitted. Report contradictions rather than silently treating either as the other. Missing descriptive documentation does not block ordinary work; resolve an unclear governing decision before changes that depend on it. Do not promote a proposal merely because it has been implemented.

## Build the smallest useful map

Update the existing map. If none exists and the task needs one, start with a single concise architecture page in the project's usual documentation location. Link its entry point from the project's existing README or AGENTS.md so future sessions can find it. Split into linked domain pages only when the overview becomes hard to navigate.

Capture only what helps future reasoning: component responsibilities and boundaries, important dependencies and data/control flows, external contracts, invariants, and consequential decisions with their rationale. Link to concrete repository paths, symbols, configuration, tests, or existing decision records. Use a diagram only when it clarifies relationships. Note coverage limits and unresolved discrepancies; do not imply a partial map covers the whole system.

Avoid exhaustive file inventories, copied implementation details, session logs, mandatory HLD/LLD templates, and speculative target designs. Reuse existing decision records and runtime runbooks rather than duplicating them. Planning-only work may describe a proposed state, clearly separated from what is implemented.

## Keep the map aligned

For implementation work, resolve architectural decisions before dependent edits and update affected documentation alongside the change. Scale detail to the uncertainty and impact. Keep one author per page at a time. A delegated task may update descriptive documentation within its assigned scope; root retains decisions and final acceptance.

Before completion, compare the affected map and decisions with the actual diff, relevant code, configuration, and checks. Verify source links, distinguish implemented behavior from unverified runtime claims, and remove stale statements in the touched scope. Do not rewrite unrelated maps or update documents merely because a task occurred. Report changed architecture sources and material gaps.

Repository verification, isolation, integration, runtime delivery, cleanup, and authorization rules still apply through project instructions and the relevant skills; this skill does not redefine them.
