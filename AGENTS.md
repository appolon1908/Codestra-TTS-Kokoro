<!-- CODESTRA-GOVERNANCE-V3:BEGIN -->
# Codestra Governed Development Contract v3

Standalone family: Voice Agent
Component: Codestra-TTS-Kokoro

Mandatory hierarchy:
Product -> Section -> Subsection -> Atomic Task

Only authorized promotion:
subsection -> section -> development -> testing -> staging -> production

Agent rules:
- one active lease per subsection;
- work only in the assigned subsection branch/worktree;
- implementation + tests + evidence + commit + push are required;
- review-only output is not completion;
- no force push and no direct protected-environment writes;
- every promotion requires codestra-control-plane plus repository CI;
- dirty, stale, divergent, dependency-incomplete, or uncertified work fails closed.

Production safety:
- PRODUCTION_GO=NO
- LIVE_CAPABILITIES_ENABLED=NO
- EXTERNAL_EFFECTS=false

Live calls, SMS, email, WhatsApp, payments, publishing, credential issuance,
production database writes, and production infrastructure mutation remain disabled
until separately certified and explicitly approved.
<!-- CODESTRA-GOVERNANCE-V3:END -->


# Existing repository-specific instructions

# Repository Agent Instructions

This `AGENTS.md` applies to the entire repository unless a deeper `AGENTS.md` provides more specific instructions for a subdirectory.

## Ownership and repository identity
- The canonical GitHub namespace for this repository is `appolon1908`.
- Treat this repository and its current default branch as the authoritative remote state. Do not assume an older owner or transferred repository path is still canonical.
- When touching cross-repository references, verify the dependency exists under `appolon1908/<repo>` before changing URLs, package sources, submodules, CI references, or documentation.

## Working rules
- Preserve repository history, current architecture, public APIs, and compatibility unless the assigned task explicitly requires a change.
- Use one active task branch/worktree per implementation lane.
- Do not perform feature development directly on a protected default branch unless the repository workflow explicitly requires it.
- Never force-push, rewrite shared history, or discard another contributor's uncommitted work.
- Before publishing changes, verify the exact repository, branch, upstream, remote HEAD, and working-tree state; fetch the target branch first.
- Do not create duplicate engines, services, adapters, schemas, or sources of truth when a canonical implementation already exists.

## Implementation and verification
- Implement requested behavior completely and add or update tests for changed behavior.
- Run the relevant unit, integration, lint, type-check, build, API/OpenAPI, Postman, or end-to-end checks that exist in this repository.
- Do not disable, delete, bypass, or weaken CI/security checks merely to make a pipeline green; fix the underlying issue.
- Keep code, schemas, generated contracts, OpenAPI definitions, migrations, and tests synchronized when a change affects them.
- Preserve backward compatibility unless a breaking change is explicitly approved and documented.

## Security and production effects
- Never commit passwords, tokens, API keys, private keys, certificates, production credentials, or other secrets.
- Default-deny live external side effects such as payments, payouts, phone calls, SMS, email, WhatsApp, social publishing, or provider mutations unless the task explicitly authorizes production effects.
- Do not bypass authentication, authorization, tenant isolation, policy, idempotency, audit, reconciliation, or safety gates.
- Keep production and staging credentials outside source code and test fixtures.

## Handoff requirements
- Report the branch, exact HEAD SHA, files changed, tests/checks run, results, and remaining blockers.
- Distinguish clearly between code-ready, merge-ready, staging-ready, and production-ready states.
- Do not claim completion, certification, deployment, or production readiness without evidence.
