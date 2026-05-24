# Workspace Instructions

This workspace coordinates multiple agents working on the OxCaml LLVM backend.

Follow the local `GOAL.md` in an agent directory. That file decides whether the
agent may edit OxCaml sources, vendored LLVM sources under
`oxcaml/vendor/llvm-project`, or both.

Rules:

- Use branches named `jujacobs/...`.
- Push agent branches to Jules's `julesjacobs/oxcaml` fork. Use
  `julesjacobs/llvm-project` only for maintaining the LLVM import-source
  checkout or when explicitly requested.
- Do not push to upstream `oxcaml/oxcaml`, `llvm/llvm-project`, or
  `ocaml-flambda/llvm-project`.
- Keep `PROGRESS.md` compact and useful for handoff.
- Record long-running build and test commands in `main/BUILD_TIMES.md` or the
  agent's `BUILD_TIMES.md` with `scripts/timed-command`.
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
  validation stages. Debug with the direct `_install` compiler first; use
  self-stage2 as the final self-hosting proof unless `GOAL.md` says otherwise.
- If a self-stage or stage2 failure appears, first try to reduce it to a
  focused test case that already fails with the direct `_install` compiler. If
  it only reproduces with self-stage2, record the smallest self-stage2
  reproducer and why direct `_install` does not cover it.
- Before acting on GitHub review comments, verify that the comment is correct.
