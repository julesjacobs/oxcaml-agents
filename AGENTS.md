# Workspace Instructions

This workspace coordinates multiple agents working on the OxCaml LLVM backend.

Start from the workspace root with
`scripts/use-or-create-agent <agent-name>`. It prints the existing agent paths
when `agents/<agent-name>/` exists, or creates that agent with branch
`jujacobs/<agent-name>` and opens a draft OxCaml PR when it does not.
Use `scripts/agent-doctor [agent-name]` to check current agent state.

Inside an agent directory, the canonical goal file is
`agents/<goal-name>/oxcaml/agent-state/<goal-name>/GOAL.md`. It decides
whether the agent may edit OxCaml sources, vendored LLVM sources under
`oxcaml/vendor/llvm-project`, or both. The agent's code checkout is
`agents/<goal-name>/oxcaml`.

Advice:

- Use branches named `jujacobs/...`.
- Push agent branches to Jules's `julesjacobs/oxcaml` fork. Use
  `julesjacobs/llvm-project` only for maintaining the LLVM import-source
  checkout or when explicitly requested.
- Do not push to upstream `oxcaml/oxcaml`, `llvm/llvm-project`, or
  `ocaml-flambda/llvm-project`.
- Keep the relevant progress file compact and useful for handoff:
  `agents/<goal-name>/oxcaml/agent-state/<goal-name>/PROGRESS.md` for agent
  work, or `main/PROGRESS.md` for integration-checkout status.
- Record the OxCaml PR link in
  `agents/<goal-name>/oxcaml/agent-state/<goal-name>/GOAL.md` and
  `agents/<goal-name>/oxcaml/agent-state/<goal-name>/PROGRESS.md`.
- The nested `oxcaml/AGENTS.md` is generic OxCaml guidance. Use it for codebase
  context and command names. For this workspace, this file overrides it on
  commits, pushes, progress files, test scope, and whether command output should
  be silent.
- Commit real code or test progress. Progress-only commits are allowed only
  when they update `agent-state/<goal-name>/PROGRESS.md`.
- Push committed progress updates so the current handoff state is visible on
  the agent's GitHub PR.
- Avoid starting multiple independent `make` or `dune` commands at the same
  time in the same checkout, because they may contend on dune's lockfile and
  deadlock. This does not mean single builds should be serialized: let one
  build/test command use its normal internal parallelism.
- Use `scripts/agent-doctor [agent-name]` when an agent path, branch, state
  file, or LLVM helper path looks suspicious. Fix the reported mismatch before
  starting long builds or tests.
- An agent should be able to work from its private checkout without knowing the
  surrounding workspace. Keep that agent's custom LLVM build beside the checkout
  at `../llvm-build`, with clang at `../llvm-build/bin/clang`. Pass
  `LLVM_PATH=$PWD/../llvm-build/bin/clang` to commands that need the custom
  clang. If a command needs wrapper logs, run
  `../../../scripts/write-agent-clang-wrapper ../llvm-build/bin/clang` from the
  checkout, then pass `LLVM_PATH=$PWD/../clang-wrapper`. Check
  `../clang-wrapper.target` for the wrapped clang and `../clang-wrapper.log` for
  fresh `-x ir` invocations. Do not point LLVM commands at `/usr/bin/clang`, a
  shared wrapper, or another agent's LLVM build.
- Keep native and LLVM-backend builds explicitly separated. LLVM self-stage
  scripts write `duneconf/*.ws` files that inject
  `OCAMLPARAM=_,llvm-backend=1,llvm-path=...`; a later plain `make install`
  can accidentally reuse those workspaces and produce an LLVM-built `_install`.
  Before building the native comparison compiler, use
  `tools/build-clean-native-install.sh` when it exists. It saves the clean
  compiler under `_native_install` and its build tree under `_native_build`, so
  later LLVM work can overwrite `_build`/`_install` without losing the native
  comparison compiler. Otherwise remove `_build`, `_install`, and
  `duneconf/{boot,runtime_stdlib,main}.ws`, then run
  `make install LLVM_BOOT_BACKEND=0 LLVM_BACKEND=0 OCAMLPARAM= BUILD_OCAMLPARAM=`.
  Before trusting a native-vs-LLVM benchmark, check `_build/log` says
  `OCAMLPARAM: ""` or `OCAMLPARAM: unset`, check the LLVM self-stage log has
  fresh IR/wrapper activity, and record `shasum`/sizes for both timed compiler
  executables. Benchmark harnesses should fail fast if the native build log
  contains `llvm-backend=1` or if both timed compiler paths resolve to the same
  file.
- Do not treat the historical `stage4`/`stage5` script names as conceptual
  validation stages. During normal work, use the standard installed compiler
  with `-llvm-backend`; use self-stage2 for full validation unless the
  canonical goal file says otherwise.
- If a failure appears, first try to reduce it to a focused test case that
  already fails with the standard compiler using `-llvm-backend`. If it only
  reproduces with self-stage2, record the smallest self-stage2 reproducer and
  why the standard `-llvm-backend` compiler does not cover it.
- Before acting on GitHub review comments, verify that the comment is correct.
