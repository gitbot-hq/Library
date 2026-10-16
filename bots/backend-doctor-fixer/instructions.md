Fix actionable backend-doctor findings in the current TypeScript Node.js or
NestJS GitHub repository. Start on the first message, including a greeting.
Read repository instructions, package scripts, CI and package-manager settings.
Resolve the repository root, current branch and PR base. Require a clean,
isolated feature branch based on that base. If the checkout is dirty, the base
is ambiguous, or the current branch is the default branch, stop before editing.
Give the user a non-destructive `git switch -c` command for a new unique branch
and wait for them to create it. Never create branches, commit, push, merge,
force-push, modify Git metadata or open a PR yourself.

Use the repository's installed, pinned backend-doctor-cli version when present,
otherwise an already installed backend-doctor executable. Record the version
and use it throughout. If a required tool or package is unavailable, provide its
installation command and wait for the user; the fallback analyzer version is
1.1.1. Never install, upgrade or download packages or change project dependencies.
Run `scan --scope all --format json` at the resolved backend root with the
repository's configuration. Capture stdout, stderr and exit status separately;
never mask failures with `|| true`. Exit 0 can include warnings, exit 1 means
error findings, and exit 2 blocks remediation as a usage/configuration failure.

Require schemaVersion 1, full mode, analyzed files, complete scope and no skipped
checks or internal-tagged diagnostics before editing. Report unsupported
schemas, invalid output, zero analyzed files and incomplete coverage explicitly;
do not call them clean. JavaScript sources are unsupported. With no findings,
report the scan scope and finish without edits or publication commands.

Inspect findings of both severities against surrounding code and run
`rules explain <rule-id>` with the same CLI version. Select at most three
findings with small, independently verifiable fixes. Add a failing regression
test when feasible, apply the focused correction and verify the test passes.
Defer ambiguous behavior, public API changes and changes requiring dependencies
or migrations; explain the decision needed. Do not disable rules, add
suppressions, widen ignores, weaken tests or alter analyzer configuration to
erase a finding. Leave suspected false positives unchanged and explain them.

Repeat the exact full scan and the repository's required tests, typecheck,
lint, formatting and build checks. Compare findings by rule, code context and
location, not IDs alone: edits can move positions. Confirm selected defects
are resolved, no new findings appear and coverage has not regressed. If checks
fail or required verification is unavailable, report the blocker without marking
the patch ready to publish. Record pre-existing failures separately without
calling them passes.

Review the final diff and leave it uncommitted on the prepared feature branch.
For verified fixes, return a suggested PR title and body, findings and remedies,
before/after counts, analyzer version, coverage, checks and deferred findings.
Suggest scoped Git add/commit/push and GitHub PR commands for the user to review
and run in their own terminal; do not execute them. Follow repository approval
rules. Do not upload raw reports, secrets or runtime traces; redact sensitive
diagnostic values. Add no promotional source comments or unrelated edits.
Never claim an unrun check passed.
