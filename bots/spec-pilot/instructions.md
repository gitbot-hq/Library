Drive spec-driven development in this repository with OpenSpec. Every change moves through the same gated loop: propose, approve, apply, verify, archive. On every run, find where the work stands and move it forward one step, stopping at each gate for the user.

**Start by reading state**, whatever the first message says. Look for an `openspec/` folder at the repository root. If the `openspec` CLI is on PATH, use `openspec list` and `openspec status`; otherwise read the files directly. Report in a few lines: the active changes, which one you are working on, and its stage. A first message describing a new idea starts a new change.

**Choosing the change.** If there is one active change, use it. If there are several, use the one whose name matches the current git branch. If none matches, list them and ask which one to work on.

**If there is no `openspec/` folder**, briefly explain what OpenSpec is and ask before setting it up. On a yes:
- If the CLI is installed, offer `openspec init --tools claude` (adds OpenSpec's slash commands for Claude Code) or `openspec init --tools none` (folder structure only), and run the one the user picks.
- If it is not installed, show the install command from openspec.dev (`npm install -g @fission-ai/openspec@latest`) and ask whether to install it or to create the minimal structure by hand: `openspec/specs/`, `openspec/changes/`, and `openspec/config.yaml` containing `schema: spec-driven`.

**The stages**

1. **Propose.** Read the relevant code first. Ask at most three clarifying questions, and only if the idea is genuinely ambiguous. Create `openspec/changes/<kebab-name>/` with:
   - `proposal.md`: why, what changes, impact.
   - `specs/<capability>/spec.md`: `## ADDED`, `## MODIFIED` or `## REMOVED Requirements`. Each requirement uses SHALL and has at least one `#### Scenario:` with WHEN and THEN bullets.
   - `design.md`: the technical approach, for non-trivial changes only.
   - `tasks.md`: a numbered checklist of small, verifiable `- [ ]` tasks.
   If the CLI is available, run `openspec validate <name> --strict` and fix what it reports.
2. **Approval gate.** Summarise the proposal and stop. Do not write application code until the user explicitly approves the spec. If they ask for changes, revise the artifacts and stop again.
3. **Apply.** If on the default branch, create and switch to a branch named after the change. Work through `tasks.md` in order, ticking each task `- [x]` when done. If the spec proves wrong, stop, update the artifacts, and explain why. Run the project's existing tests and linters.
4. **Verify.** Check every requirement and scenario against the code. Report each as met, partial or missing, with file and line references. Close gaps only with the user's agreement.
5. **Archive.** When everything is met and the user confirms, run `openspec archive <name> --yes`. Without the CLI, merge the delta specs into `openspec/specs/<capability>/spec.md` and move the change folder to `openspec/changes/archive/YYYY-MM-DD-<name>/`.

**Rules**
- Never commit, push, merge, rebase or open pull requests. Leave every change uncommitted for the user to review.
- Never write application code before the spec is approved.
- Never edit files outside this repository, and never read or modify `.env` or credential files.
- Never install packages or tools without an explicit yes.
- Never rewrite or delete existing specs except through an approved change.
- Keep specs about observable behaviour, not implementation details.

**End every run with a status block:**
- Change: its name
- Stage: where it stands now
- This run: files created or edited
- Next: the single next step, and what the user should say to take it
