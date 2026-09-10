---
name: tailscale-service-delivery
description: Deliver local web apps and review interfaces on this homeserver through Caddy at a dev.benceb.hu domain over Tailscale. Use when starting, updating, or handing off a browser-accessible local service; supports native services and Docker Compose.
---

# Tailscale service delivery

On this host, deliver browser-accessible work at a verified `https://<service>.dev.benceb.hu` URL. Keep it running after the task ends. A localhost URL alone is not the default handoff. This applies to runnable web work, not ordinary document or library edits.

## Inspect the existing path

Read the project's instructions and runtime runbook. Inspect `/home/benceb/Caddyfile` (normally symlinked from `/etc/caddy/Caddyfile`) and `/home/benceb/homeserver/README.md`. Recheck current service ownership, routing, DNS, ports and runtime before modifying them. Preserve unrelated services and user data.

The existing wildcard terminates TLS in Caddy and normally forwards to Traefik at `127.0.0.1:13100`. Containers opt into the external `workspace-dev-proxy` network with unique Traefik host labels. Native apps can use a host-specific `handle` inside the wildcard, with the remaining wildcard in a fallback `handle`. Reuse wildcard TLS; do not create duplicate sites or certificates unnecessarily.

## Choose the smallest suitable runtime

- Reuse the project's existing Compose or native service mechanism.
- Use systemd for a simple native app. Keep its upstream bound to loopback, use the owner account, restart on failure and enable startup after reboot. Store the unit template and lifecycle commands in the project.
- Use Compose when the app already needs it or isolation/dependencies justify it. Use a unique project identity and `workspace-dev-proxy`; publish no application host ports. Keep data and internal services off the shared proxy network. Follow project worktree rules when applicable.
- Do not introduce Docker solely to obtain a hostname.

Keep access within the intended Tailscale scope. Check existing access controls; for an unauthenticated native app, a Caddy remote-address allowlist for the tailnet and loopback can enforce it. Do not trust client-supplied forwarded headers as proof of tailnet membership. Keep the upstream Host/Origin contract correct; do not remove application checks just to make the proxy work.

## Apply and verify

Prepare concrete project-owned configuration first. Validate it before activating it. Back up shared configuration, recheck it for drift, and change only the task's route. Reload Caddy rather than restarting unrelated services. Avoid printing DNS-provider credentials or environment secrets. Native Caddy validation may require its service environment; load it privately if needed.

Verify runtime health, startup persistence, routing, TLS certificate validation and the application response through the actual domain. A forced `curl --resolve` is useful for routing/TLS tests but does not prove client DNS: report DNS results separately. Check the configured tailnet resolver when system DNS differs. Test access restrictions where relevant. Do not claim validation from merely listing a process or obtaining an HTTP response on its direct port.

Update the project's runtime/architecture documentation with the domain, service or Compose identity, route ownership, status/log/start/stop commands, verification and limitations. Leave the review service running unless the user requests shutdown. Retire only task-owned temporary listeners after the replacement is verified.

Use existing authorization for requested local delivery. This convention does not authorize public Internet exposure, production replacement, unrelated shared infrastructure changes, or deletion of data. Report any environmental approval block and complete independent work.
