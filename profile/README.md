# Pegma

Composable, MIT-licensed components for building web applications — designed
to be assembled and maintained by AI coding agents.

> [!IMPORTANT]
> Pegma is in early development. Nothing is published to npm yet, no public
> API is stable, and none of it is ready for production use.

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

| Package                       | Purpose                                             | Status      |
| ----------------------------- | --------------------------------------------------- | ----------- |
| `@pegma/spine`                | Shared identity, time, logging, and event contracts | in progress |
| `@pegma/storage-core`         | Schema-agnostic persistence with declared collections | planned   |
| `@pegma/authorization-core`   | Permission and entitlement resolution                | planned     |
| `@pegma/support-desk-core`    | Ticket and message workflow                          | planned     |

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
