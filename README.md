# Agentic QA environments

A reusable agent skill for preparing and verifying isolated development environments with real application services, synthetic test data, browser interaction, and evidence across the UI, API, and database.

Use it to make a local or cloud workspace ready for an agent to develop and test an application, recover interrupted services, or produce an acceptance receipt with clear limits. It includes guidance and synthetic examples. It does not include an application-specific installer, cloud provisioning service, credentials, or provider adapters.

## Install

Clone this repository and inspect the skill before installing it:

```sh
git clone https://github.com/danialhasan/agentic-qa-environments.git
cd agentic-qa-environments
```

For Codex, ask its skill installer to install `skills/agentic-qa-environments` from this repository. You can also copy that folder into your existing Codex skills directory. Preserve the `references`, `assets`, and `agents` subdirectories, and do not overwrite an existing skill without reviewing its changes. Restart the client if required for discovery.

Other agents that support `SKILL.md` can load [the entrypoint](skills/agentic-qa-environments/SKILL.md) directly. Tool availability and filesystem permissions still come from the agent's host.

## Use

> Use $agentic-qa-environments to prepare this repository's cloud workspace for a synthetic user's save, reload, and reopen journey. Use isolated dependencies, verify persistence independently, and report which acceptance layers pass.

> Use $agentic-qa-environments to diagnose this environment after an interrupted run, preserve its seeded data, and verify that shared services remain usable.

> Use $agentic-qa-environments to audit this local/cloud comparison and recording. Separate application correctness, capture cadence, resource measurements, and untested provider behavior.

The agent needs access to the selected application's setup instructions, pinned dependencies, an authorized workspace, and tools for the requested observations. Browser QA needs a supported browser and control surface. Database verification needs access to isolated test state. Headed capture may need a display and recording tools. The skill does not grant connector authorization, browser privileges, credentials, extra network access, or spending authority.

## Package

- [SKILL.md](skills/agentic-qa-environments/SKILL.md) defines the workflow and when to use it.
- [Bootstrap and lifecycle](skills/agentic-qa-environments/references/bootstrap-and-lifecycle.md) covers setup, seeding, ownership, recovery, and optional remote providers.
- [Evidence and measurement](skills/agentic-qa-environments/references/evidence-and-measurement.md) covers acceptance, recording, reproducibility, and sharing.
- [Example environment](skills/agentic-qa-environments/assets/environment.example.json) and [example receipt](skills/agentic-qa-environments/assets/acceptance.example.json) show a fictional notes application. Their data is synthetic, their artifact paths are illustrative, and they are not executable configuration or measured results.

## Verification limits

This package provides a method to apply and verify in your own repository. It does not certify any cloud provider, guarantee that a full application will run in an arbitrary sandbox, or claim a recording frame rate. Local execution, cloud execution, provider calls, CI, deployment, and human acceptance require their own evidence.

Structural validation and isolated agent scenario evaluations check the package's usability. They do not establish a live cloud deployment or real provider performance. No application code, private traces, customer data, or third-party adapters are distributed here.

## License

The newly authored package is available under the [MIT License](LICENSE). External documentation is linked for reference and remains under its owners' terms.
