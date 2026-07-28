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
> Pegma is in early development. The first `0.x` packages are on npm, but no
> public API is stable and none of it is ready for production use.

## The idea

Most of what a site needs has been built ten thousand times: accounts,
authorization, a support queue, a blog, billing. Rebuilding them per project
is expensive, and having an agent generate them from scratch each time is
worse — thousands of lines of novel, unverified logic, different every run.

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
| `@pegma/audit`                      | Append-only audit records                             | published   |
| `@pegma/logger-tee`                 | Fan-out Spine Logger to multiple sinks                | published   |
| `@pegma/logger-applicationinsights` | Spine Logger to Application Insights                  | published   |
| `@pegma/logger-cloudflare`          | Spine Logger to Cloudflare Workers Logs               | published   |
| `@pegma/logger-datadog`             | Spine Logger to Datadog logs                          | published   |
| `@pegma/authorization-core`         | Permission and entitlement resolution                 | in progress |
| `@pegma/support-desk-core`          | Ticket and message workflow                           | in progress |
| `@pegma/webhooks`                   | Inbound webhook receipts: dedup, quarantine, retention | in progress |
| `@pegma/sessions`                   | Server-side session records: hashed ids, dual expiry  | published   |
| `@pegma/rate-limit`                 | Honest two-tier request limiting                      | planned     |
| `@pegma/identity`                   | First-party identity: passkeys-first, no passwords    | planned     |
| `@pegma/mail`                       | Transactional mail: an outbox that owns no store      | planned     |

Planned components carry a published plan and a deliberate gate; each
repository's `docs/PROJECT_PLAN.md` is the source of truth, and the
[pegma.dev roadmap](https://pegma.dev/roadmap) compiles those plans at build
time.

Webhooks Phase 2 is implemented and merged into RetireGolden. Its operational
exit still awaits observed production Stripe traffic, and Phase 3 is gated on
a second real non-Stripe provider. `@pegma/webhooks` remains unpublished.

Sessions Phase 1 is merged, Phase 2 is merged as the first RetireGolden
consumer migration, and `@pegma/sessions` is published as `0.1.0`. Its early
`0.x` API remains unstable.

Every published package is released only from its repository's workflow on a
short-lived OIDC credential, with a provenance attestation linking the tarball
to the commit that built it. No long-lived publish tokens exist.

Components depend on `@pegma/spine` and, where they persist anything, on
`@pegma/storage-core`. They do not depend on each other.

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

The name is Latin, borrowed from Greek πῆγμα: a framework fastened together,
and in Roman amphitheatres a machine-operated scaffold that raised the scenery
into place.

Pegma is developed by [RetireGolden, LLC](https://retiregolden.org), which
uses these components in production. The projects are deliberately not
retirement-specific.
