---
name: tailscale-service-delivery
description: Connect local web apps and review interfaces on Bence's homeserver to its existing private Tailscale HTTPS routing and DNS overrides at dev.benceb.hu. Use when starting, updating, or handing off browser-accessible local services; not public deployment or headless tests.
---

# Tailscale service delivery

Deliver browser-accessible work at a verified `https://<service>.dev.benceb.hu` URL. These services are reachable only through Bence's Tailscale network using existing DNS overrides, not the public Internet. Reuse that arrangement without adding authentication gateways, per-app IP allowlists, or redesigning network controls. Preserve the existing access boundary.

This skill owns hostname, routing, TLS, DNS, and URL verification. [local-dev-environment](../local-dev-environment/SKILL.md) owns runtime, source/data isolation, readiness, and lifetime. Root coordinates both on one environment without an agent handoff. A suitable running service needs no rebuild merely to gain a hostname. Leave delivered review services running under the runtime skill's retention rules.

## Reuse the homeserver path

Read project runtime instructions, `/home/benceb/homeserver/README.md`, and relevant parts of `/home/benceb/Caddyfile` (normally symlinked from `/etc/caddy/Caddyfile`). Confirm route ownership and upstream; reuse the task's hostname or select an unused one. Use existing DNS overrides, not public DNS changes.

The wildcard normally terminates TLS in Caddy and forwards to Traefik at `127.0.0.1:13100`. Follow actual host configuration if these details have changed:

- Compose frontends join `workspace-dev-proxy` with unique Traefik router/service labels and an explicit upstream port. This path needs no application host-port publishing; keep internal/data services off the shared proxy network.
- Native apps use their assigned loopback port and the existing route pattern, typically a host-specific `handle` inside the wildcard with remaining traffic in a fallback `handle`.

Reuse wildcard TLS; do not create duplicate sites, certificates, proxies, or runtimes. Configure the application's Host/Origin contract correctly rather than disabling its checks.

## Apply the scoped change

Keep task routing configuration or labels reproducible in the project. Serialize shared proxy edits even across worktrees. Before editing a shared file, preserve a recovery copy and recheck for drift; change only the task's route. Validate with the service's actual configuration/environment without printing secrets, then use the existing graceful reload procedure. Compose-label changes normally require only the relevant runtime update, not a Caddy edit.

Preserve diagnostic evidence and the last working route on failure where possible; never restore an old shared file over unrelated changes. Do not restart unrelated services, widen exposure, or change unrelated infrastructure.

## Verify and hand off

Check the actual HTTPS domain with certificate validation and a representative changed interaction, including WebSockets when relevant. Use the established tailnet resolver when host DNS differs. `curl --resolve` tests routing/TLS, not normal client DNS; distinguish those results and report missing evidence. Reuse runtime readiness evidence rather than repeating startup checks.

Add the hostname, route owner/upstream, configuration location, and DNS/TLS/application verification to the runtime's existing environment record. Hand off the HTTPS URL, not just localhost. Retire superseded task routes or listeners only after their replacement is verified and they are no longer needed; preserve shared proxy resources.
