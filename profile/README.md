<picture>
  <source
    media="(prefers-color-scheme: dark)"
    srcset="https://raw.githubusercontent.com/pegma-dev/.github/main/brand/pegma-lockup-horizontal-white-1600.png"
  />
  <img
    src="https://raw.githubusercontent.com/pegma-dev/.github/main/brand/pegma-lockup-horizontal-1600.png"
    alt="Pegma"
    width="360"
  />
</picture>

Composable, MIT-licensed components for building web applications — designed
to be assembled and maintained by AI coding agents. **[pegma.dev](https://pegma.dev)**

> [!IMPORTANT]
> Pegma is in early development. Published packages remain unstable `0.x`
> APIs; adopters must pin exact versions and own their deployment review.

## The idea

Most of what a site needs has been built ten thousand times: sessions, audit
trails, persistence, health probes, structured logging. Rebuilding them per
project is expensive, and having an agent generate them from scratch each time
is worse — thousands of lines of novel, unverified logic, different every run.

Pegma takes the other path. Each capability is an independent package with a
typed contract and a published conformance suite. Building a site becomes
*assembly* rather than *generation*: pick the components, wire them together
at a composition root, and let the compiler and the conformance suites prove
the wiring is correct. The hard logic is written once, verified once, and
reused — not re-rolled per project.

## Components

| Package                             | Purpose                                               | Status      |
| ----------------------------------- | ----------------------------------------------------- | ----------- |
| `@pegma/spine`                      | Shared identity, time, logging, and event contracts   | published   |
| `@pegma/storage-core`               | Schema-agnostic persistence with declared collections | published   |
| `@pegma/storage-azure-tables`       | Azure Table Storage adapter                           | published   |
| `@pegma/storage-cloudflare-d1`      | Cloudflare D1 adapter                                 | published   |
| `@pegma/storage-blobs`              | Provider-neutral object (blob) storage port           | published   |
| `@pegma/storage-azure-blob`         | Azure Blob Storage adapter                            | published   |
| `@pegma/storage-cloudflare-r2`      | Cloudflare R2 adapter                                 | published   |
| `@pegma/storage-s3`                 | AWS S3 / S3-compatible adapter                        | published   |
| `@pegma/audit`                      | Append-only audit records                             | published   |
| `@pegma/logger-tee`                 | Fan-out Spine Logger to multiple sinks                | published   |
| `@pegma/logger-applicationinsights` | Spine Logger to Application Insights                  | published   |
| `@pegma/logger-cloudflare`          | Spine Logger to Cloudflare Workers Logs               | published   |
| `@pegma/logger-datadog`             | Spine Logger to Datadog logs                          | published   |
| `@pegma/health`                     | Composable health probes and public liveness responses | published   |
| `@pegma/sessions`                   | Server-side session records: hashed ids, dual expiry  | published   |
| `@pegma/authorization-core`         | Permission and entitlement resolution                 | published   |
| `@pegma/authorization-identity`     | Verified Identity claims adapter                      | published   |
| `@pegma/support-desk-*`             | Ticket, application, mail, and template source        | unpublished |
| `@pegma/webhooks`                   | Inbound webhook receipts: dedup, quarantine, retention | unpublished |
| `@pegma/rate-limit`                 | Honest two-tier request limiting                      | published   |
| `@pegma/identity`                   | First-party identity: passkeys-first, no passwords    | published   |
| `@pegma/mail`                       | Transactional mail: an outbox that owns no store      | published   |

Each component's `docs/PROJECT_PLAN.md` is the source of truth, and the
[pegma.dev roadmap](https://pegma.dev/roadmap) compiles those plans at build
time.

The 2026-07-28 Identity batch published `@pegma/rate-limit@0.1.0`,
`@pegma/mail@0.1.0`, `@pegma/identity@0.1.0`, and the synchronized
Authorization Core `0.1.2` package set containing
`@pegma/authorization-identity`. `@pegma/sessions@0.1.0` and the Storage Core
`0.4.0` D1 adapter complete the composition now running on pegma.dev.

The 2026-07-29 Storage Blobs first release published
`@pegma/storage-blobs@0.1.0` with Azure Blob, Cloudflare R2, and S3 adapters
at the same version (signed `v0.1.0`, trusted-publisher provenance).

Support Desk now implements its customer application slice and
provider-neutral outbound-mail integration against exact `@pegma/mail@0.1.0`.
Its four packages remain unpublished until the deployment and hardening phases.

Webhooks Phase 2 is implemented and merged into RetireGolden. Its operational
exit still awaits observed production Stripe traffic, and Phase 3 is gated on
a second real non-Stripe provider. `@pegma/webhooks` remains unpublished.

Normal releases use repository workflows with short-lived OIDC authority and
provenance attestations; no long-lived publish tokens exist. Sessions `0.1.0`
is the documented legacy exception: its initial workflow failed before the npm
name existed, so the exact artifact was published manually without provenance.
Sessions releases from `0.1.1` onward use the hardened OIDC path.

Components share contracts through `@pegma/spine` and, where they persist
anything, use `@pegma/storage-core`. Narrow sibling dependencies are added only
when real consumers justify them—for example Identity composes Mail and Rate
Limit—then pinned exactly and wired explicitly at the host boundary.

## Design principles

- **Assembled by agents.** Every decision optimizes for one question: how much
  context must a fresh agent read to make a correct change, and how does it
  know the change is correct? Minimize the first, mechanize the second.
- **Boring on purpose.** Ordinary, idiomatic TypeScript. Novel structures make
  both humans and models worse at reading code.
- **Contracts are the joints.** Components meet at typed interfaces, never at
  each other's internals. Swapping an implementation should not ripple.
- **Conformance suites are the specification.** If a rule matters, it is a
  type or a test — not a paragraph someone has to remember.
- **Explicit wiring.** No autodiscovery, no convention-based magic. The
  composition root is the map of the system.
- **Uniform by repetition.** Every repository uses the same layout, scripts,
  and conventions, so that one worked example teaches all of them.

## Provenance

The name is Latin, borrowed from Greek πῆγμα (from πήγνυμι, “to fasten
together”): a framework of joined parts. In Roman amphitheatres the same word
named a machine-operated scaffold — multi-stage wooden machinery raised and
lowered by ropes and counterweights — that brought scenery and performers into
view. Pegma is that kind of thing: independent pieces fastened together, raised
into place by the agent that assembles them.

Pegma is developed by [RetireGolden, LLC](https://retiregolden.org), which
uses these components in production. The projects are deliberately not
retirement-specific.
