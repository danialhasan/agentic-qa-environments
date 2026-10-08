---
name: agentic-qa-environments
description: Prepare, recover, and verify isolated local or cloud environments for agent-driven development and full-stack browser QA. Use when a task needs reproducible services, seeded state, browser access, or evidence across UI, API, and database boundaries.
---

# Agentic QA environments

Produce a usable environment and an acceptance receipt that says which requested behaviors were observed. A successful install is a prerequisite; it does not establish that an agent can edit, test, use the browser, or preserve application data.

## Establish the execution contract

Read the selected repository's setup instructions and pinned dependencies. Identify the requested user journey and whether the agent must also edit code, run tests, recover services, or record the interaction. Keep the environment local or cloud as requested. A local browser controlling a remote service is a distinct topology; record where each component runs.

Before starting services, record the checkout and revision, relevant uncommitted changes, dependency and migration identities, runtime versions, available resources, current listeners, and ownership of existing services. Check effective configuration, including inherited environment variables, without printing secret values. A loopback app URL does not establish that its database or provider destination is isolated.

Define the smallest useful acceptance slice and its observable result. For example, a synthetic user creates a note, reloads, reopens it, and sees the exact saved content while an independent database read confirms persistence. Decide which failure, recovery, concurrency, and recording checks matter for this task. Use [the example environment contract](assets/environment.example.json) as a shape, not as executable configuration.

## Build and identify the environment

Use an owned runtime directory separate from source and shared services. Keep tools, state, private configuration, logs, and evidence identifiable. Pin dependencies with the repository lockfile and record image digests when containers are used. Check disk, memory, architecture, browser dependencies, and allowed downloads before expensive setup. Cache immutable dependencies where supported; never bake active credentials or mutable customer data into an image.

Separate dependency installation, service startup, migrations, and synthetic seeding. Make repeat startup preserve state. Reset only a disposable resource whose ownership is established. Record whether each dependency is owned or borrowed, and give concurrent runs separate ports, namespaces, profiles, and fixture identifiers. Inspect unexpected listeners instead of killing whatever holds a port.

Use explicit development destinations and fail on missing configuration. Do not silently substitute production, another account, a remote paid provider, or a mocked service. Provider access, application login, browser sign-in, and connector authorization are separate capabilities. Setup does not grant any of them. Use existing authorized access; request only the specific missing authority or information after checking available evidence.

For implementation and recovery details, read [bootstrap and lifecycle](references/bootstrap-and-lifecycle.md).

## Exercise the requested behavior

Confirm fresh readiness from the intended runtime, not just an open port. Record a process start identity or runtime nonce and bind subsequent evidence to it. An expected error response may prove routing; it cannot prove the successful business operation behind that route.

Use the available supported browser surface and its normal sandbox. Verify actual browser launch behavior; wrappers and inherited variables can change launch flags. Do not resolve a failed launch by disabling sandboxing or broadening host permissions. A virtual display enables rendering, but does not itself provide browser control, extension access, authentication, or platform permission.

Seed minimal synthetic records through the supported setup path, then use the normal application journey for acceptance. Bind visible state to a fresh API response for the current document and exact fixture. Independently read the database for persisted values and relationships; a toast or HTTP success alone is insufficient. Keep inspection from performing the write under test.

When development is requested, make a bounded edit in the intended checkout, run the affected check, and demonstrate that the running application serves that edit. Keep a meaningful failing control where it helps prove the verifier detects the target defect, then restore the intended behavior and recheck.

Choose relevant negatives such as unauthorized access, stale writes, rejected input, or a controlled dropped write. Isolate deliberate faults from normal operation and label their receipts. Repeat with the same fixture identity when claiming recovery or idempotency. After an interruption, verify fresh runtime identity and unchanged expected data. If services are shared, confirm a healthy peer remained usable. A restart does not by itself test credential expiry or renewal.

## Retain evidence and state the limits

Use one receipt per run with environment identity, checks, actual outcomes, artifact locations and hashes, cleanup results, and unresolved requirements. Keep failed attempts intact and link later corrective runs. Mark checks as passed, failed, blocked, or not tested; do not convert an unfinished requirement into success.

Inspect screenshots and recordings for the actual requested states. Keep machine evidence and readable visual evidence together, with enough timing and identity to connect them. Read [evidence and measurement](references/evidence-and-measurement.md) when recording, comparing local and cloud execution, or auditing an acceptance claim. Encoded frame rate, renderer callbacks, captured frames, and application changes measure different things.

Treat traces, browser profiles, auth responses, cookies, URLs, storage dumps, and logs as private until reviewed. Retain restricted originals and make separately hashed sanitized copies when sharing is needed. Sanitization must not silently remove evidence required for acceptance; record the resulting limitation. Verify artifacts after transfer by hash and inspect their readable contents.

Stop and clean only owned processes, fixtures, and temporary resources. Include child processes and cancellation paths; verify shared identities remain intact. Preserve data and logs required for diagnosis. Report remaining cleanup failures explicitly.

Finish with what the environment can demonstrably do, what remains untested or blocked, and the next concrete action. Use [the synthetic acceptance receipt](assets/acceptance.example.json) for partial results. Keep implementation, local proof, cloud proof, CI, provider execution, deployment, and human acceptance separate.
