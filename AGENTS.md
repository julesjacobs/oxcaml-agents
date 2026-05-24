# Workspace Instructions

This workspace coordinates multiple agents working on the OxCaml LLVM backend.

Start from the workspace root with
`scripts/use-or-create-agent <agent-name>`. It prints the existing agent paths
when `agents/<agent-name>/` exists, or creates that agent with branch
`jujacobs/<agent-name>` and opens a draft OxCaml PR when it does not.

Inside an agent directory, `GOAL.md` decides whether the agent may edit OxCaml
sources, vendored LLVM sources under `oxcaml/vendor/llvm-project`, or both. The
agent's code checkout is `agents/<goal-name>/oxcaml`.

Advice:

- Use branches named `jujacobs/...`.
- Push agent branches to Jules's `julesjacobs/oxcaml` fork. Use
  `julesjacobs/llvm-project` only for maintaining the LLVM import-source
  checkout or when explicitly requested.
- Do not push to upstream `oxcaml/oxcaml`, `llvm/llvm-project`, or
  `ocaml-flambda/llvm-project`.
- Keep the relevant progress file compact and useful for handoff:
  `agents/<goal-name>/PROGRESS.md` for agent work, or `main/PROGRESS.md` for
  integration-checkout status.
- Record the OxCaml PR link in `agents/<goal-name>/GOAL.md` and
  `agents/<goal-name>/PROGRESS.md`.
- When a nested repo `AGENTS.md` says to test or format, do it only when it
  makes sense for the current step. Full tests can take a long time, so avoid
  running them while still reducing or investigating a failure. If an
  instruction says to use `-s`, skip `-s` when command output is needed for
  debugging.
- Commit real code or test progress. Do not commit progress-note-only changes
  unless they are part of the same commit as a real change.
- Avoid running multiple `make` or `dune` commands at the same time in the same
  checkout.
- When testing LLVM-backend behavior, verify real LLVM use by checking
  `/tmp/oxcaml-clang-wrapper.log` for `-x ir` and the fixed-register flags.
- Do not treat the historical `stage4`/`stage5` script names as conceptual
  validation stages. During normal work, use the standard installed compiler
  with `-llvm-backend`; use self-stage2 for full validation unless `GOAL.md`
  says otherwise.
- If a failure appears, first try to reduce it to a focused test case that
  already fails with the standard compiler using `-llvm-backend`. If it only
  reproduces with self-stage2, record the smallest self-stage2 reproducer and
  why the standard `-llvm-backend` compiler does not cover it.
- Before acting on GitHub review comments, verify that the comment is correct.
