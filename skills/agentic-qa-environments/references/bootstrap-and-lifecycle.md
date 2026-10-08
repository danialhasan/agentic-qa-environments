# Bootstrap and lifecycle

Read this when writing an environment recipe or repairing startup and recovery. Adapt commands to the selected repository; this package does not provide an application adapter.

## Installation and startup

Use three independently inspectable stages:

1. **Prepare dependencies.** Verify the checkout, lockfile, migration set, architecture, tool versions, image identities, free disk and expected downloads. Install into the permitted workspace or image. Preserve the install log and distinguish an image-cold run from a cached run.
2. **Start services.** Load private configuration, reserve owned ports, start dependencies, apply the intended schema, and launch the selected applications. Record effective destinations without credentials. Fail readiness if the runtime serves stale source or points at an unexpected dependency.
3. **Create test state.** Generate a unique fixture namespace and the minimum users, roles, and records for the requested journey. Record the seed version and baseline counts. Keep this stage explicit so restarting an environment cannot repeatedly create records or dispatch work.

A seed snapshot must match the schema and application revision. Prefer synthetic data generated from a deterministic recipe. Restore a snapshot only into an owned disposable destination, and verify the target before reset. A cache is an optimization; document what gets reconstructed when it is absent.

Record source changes during setup and rebuild affected outputs before making claims. For a benchmark or reproducible acceptance run, freeze the relevant source and tool identities at execution time. A source archive collected afterward cannot establish exactly which helper ran.

## Browser and display

Select a supported browser build and automation version for the runtime. Confirm dependencies, user identity, sandbox configuration, and viewport before the product flow. The [Playwright Docker documentation](https://playwright.dev/docs/docker) distinguishes root and non-root sandbox behavior, browser dependencies, and matching client/server versions. Verify the pinned implementation rather than assuming its newest documented behavior applies.

If headed capture needs a virtual display, allocate an owned display and browser profile. Verify the app's actual viewport as well as the captured pixel dimensions. Capture a known page and inspect the result before a long recording. Headless mode, a virtual display, and a desktop browser can have different rendering and interaction behavior; label which was exercised.

A missing sandbox capability is an environment limitation. Continue independent setup or diagnostics, and identify the supported runtime requirement. Do not add elevated capabilities, change network policy, disable security controls, or install global tools solely to make a check pass.

## Ownership and recovery

Maintain a small ownership manifest: run ID, runtime directory, process IDs with start identities, process groups or supervisor handles, container IDs, volumes, ports, display, browser profile, and fixture namespace. Distinguish borrowed dependencies from owned ones before launch. A PID by itself is insufficient because operating systems reuse it.

Use a supervisor or cleanup mechanism that handles ordinary exit, failure, timeout, and interruption. Cancel the owned child process tree, then wait for it to stop before removing state. Recheck ownership before any stop or deletion. Report live orphan processes separately from exited processes awaiting reaping. Do not remove a directory while an owned child can still write into it.

Recovery should preserve expected records, issue a fresh application identity, and re-establish authenticated access where relevant. For borrowed services, restart only the borrower and verify owner services remain usable. A shared database requires separate namespaces and narrowly targeted cleanup; a shared schema reset is not an isolated action.

Test credential expiry only when it is part of the acceptance scope. Use disposable local identities and short-lived test credentials with their own storage. Observe actual rejection after expiry, renewal through the supported path, and resumed access. Exercise interruption during multi-file credential replacement if that mechanism is under test, without exposing values. Do not infer renewal from a successful restart using a still-valid token.

## Optional remote providers

Local databases, authentication services, provider emulators, and real remote APIs are separate execution modes. Record the exact method required by the application and verify that the pinned local implementation supports it. Installing a browser or adding model credentials cannot supply a missing provider method.

When repeated failures suggest a contract mismatch, inspect the pinned platform source and a mature primary-source implementation before declaring a platform restriction or rewriting the architecture. Keep the decision specific to the method and version that were checked.

Prepare a bounded real-provider check only when needed: selected account, endpoint, input, maximum attempts, deadline, output evidence, cleanup, and spend scope. Confirm existing authorization for those actions. A request timeout or stated budget does not enforce an account billing ceiling. On failure, retain the receipt and honor the agreed retry scope; do not silently switch accounts, plans, credentials, or providers.

Neither a successful emulator check nor a successful single remote call proves the whole production workflow. State exactly which path was exercised.
