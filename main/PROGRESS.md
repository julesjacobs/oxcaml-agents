# Main Progress

Last updated: 2026-05-24.

## Current State

The shared workspace is under `/Users/julesjacobs/git/oxcaml-llvm`.

- OxCaml: `main/oxcaml`, branch `jujacobs/llvm-backend-integration`,
  fork `https://github.com/julesjacobs/oxcaml`
- LLVM: `main/llvm-project`, branch `jujacobs/oxcaml-llvm-integration`,
- Vendored LLVM: `main/oxcaml/vendor/llvm-project`, imported from
  `main/llvm-project` commit `1fc49b70ffad57d8706036336ca0d6d94ac2353e`
- Build timings: `main/BUILD_TIMES.md`
- Patched clang wrapper used for tests: `/tmp/oxcaml-main-clang-wrapper`

The main checkout now has evidence that both the direct `_install` compiler and
the self-stage2 compiler pass the full LLVM-backend testsuite on this machine.

Current commits:

- OxCaml: `eab5b5f7ca` (`Fix LLVM stage script flag and log handling`)
- LLVM: `1fc49b70f` (`Record LLVM integration fixes used by current build`)
- Vendored LLVM baseline: uncommitted import under
  `main/oxcaml/vendor/llvm-project`

## Verified Evidence

- Current source has four uncommitted fixes:
  - `runtime/fiber.c` rewrites copied native stack words that look like
    pointers into the old stack after stack reallocation, and follows
    exception-handler links across parent stacks.
  - `testsuite/tests/frame-pointers/fp_backtrace.c` parses Darwin
    `backtrace_symbols` output and uses `nm` fallback resolution for
    `__code_begin` aliases.
  - `runtime/arm64.S` now updates the oldest saved frame pointer in the target
    fiber by storing the frame record address that `SWITCH_OCAML_STACKS` is
    about to create. The earlier experiment that stored live `x29` was wrong
    and was reverted before this fix.
  - `tools/setup-llvm-stage4-ocamltest.sh` supplements missing bytecode
    `compiler-libs/*.cmo` files from `_build/install/main` when the tested
    install tree does not provide them. This fixes direct `_install`
    `tests/utils` runs without overriding stage installs that already include
    those files.
- `make-install-serial-after-stack-word-pointer-rewrite-uintnat` succeeded:
  `DUNE_BUILD_FLAGS=-j1 make -C main/oxcaml install LLVM_BACKEND=1`, duration
  277s.
- `make-install-serial-after-arm64-update-base-pointer-spminus16` succeeded:
  `DUNE_BUILD_FLAGS=-j1 make -C main/oxcaml install LLVM_BACKEND=1`, duration
  277s.
- The native-toplevel stack-reallocation repro now exits 0 with `_install`:
  `let a = match #'m' with | #'a'..#'z' -> 1;;` followed by
  `let b = match #'m' with | #'\x00'..#'\x80' -> 0 | #'\x81'..#'\xff' -> 1;;`.
  It used to exit 133 (`SIGTRAP`).
- Directly feeding `testsuite/tests/typing-small-numbers/test_matching_native.ml`
  to the rebuilt `_install/bin/ocamlnat` exits 0.
- `llvm-self-stage2-install-after-stack-word-rewrite` succeeded:
  `DUNE_BUILD_FLAGS=-j1 make -C main/oxcaml llvm-self-stage2-install
  LLVM_PATH=/tmp/oxcaml-main-clang-wrapper`, duration 3010s. This built
  `_llvm_self_stage_install` and `_llvm_self_stage2_install`; wrapper evidence
  showed fresh `-x ir` clang invocations and fixed-register flags.
- `llvm-self-stage2-test-typing-small-numbers-after-stack-word-rewrite`
  succeeded in the staged setup, duration 35s.
- Full stage2 testsuite after the stack-word rewrite, before the latest
  `runtime/arm64.S` base-pointer fix: 6634 passed, 267 skipped, 6 failed,
  0 unexpected errors, duration 1690s. The only failures were the six native
  `tests/frame-pointers` tests.
- After the Darwin `fp_backtrace.c` parser and `nm` normalization, the focused
  stage2 `tests/frame-pointers` run improved from 6 failures to 1 failure:
  `tests/frame-pointers/effects.ml` missed
  `camlEffects__h_effect_e_2_8_code` after `perform` returned.
- The bad `runtime/arm64.S` experiment that stored `x29` at the target base
  pointer slot made focused `_install` frame-pointer output worse: 17 passed,
  4 failed. It was rebuilt out with
  `make-install-serial-after-reverting-arm64-update-base-pointer`, duration
  276s.
- The corrected `runtime/arm64.S` base-pointer update fixed the focused
  `_install` frame-pointer directory:
  `llvm-install-test-frame-pointers-after-arm64-update-base-pointer-spminus16`
  reported 21 passed, 0 failed, 0 unexpected errors, with 28 wrapper calls and
  14 fresh `-x ir` invocations.
- `llvm-self-stage2-install-after-arm64-base-pointer-spminus16` succeeded:
  `DUNE_BUILD_FLAGS=-j1 make -C main/oxcaml llvm-self-stage2-install
  LLVM_PATH=/tmp/oxcaml-main-clang-wrapper`, duration 2996s. Wrapper evidence
  showed fresh `-x ir` clang invocations in both self stages.
- `llvm-self-stage2-test-frame-pointers-after-arm64-base-pointer-spminus16`
  succeeded: 21 passed, 0 failed, 0 unexpected errors, with 28 wrapper calls
  and 14 fresh `-x ir` invocations.
- `llvm-self-stage2-test-full-after-arm64-base-pointer-spminus16` succeeded:
  6640 passed, 267 skipped, 0 failed, 0 unexpected errors, duration 1694s,
  with 6472 wrapper calls and 3236 fresh `-x ir` invocations.
- The first direct `_install` full run after the base-pointer fix failed only
  because `tests/utils` could not find bytecode `compiler-libs/*.cmo` files in
  the fake source tree. After the fake-source setup fix,
  `llvm-install-test-utils-after-fake-utils-cmo-fix` succeeded: 6 passed,
  0 failed.
- `llvm-install-test-full-after-fake-utils-cmo-fix` succeeded: 6640 passed,
  267 skipped, 0 failed, 0 unexpected errors, duration 1698s, with 6472 wrapper
  calls and 3236 fresh `-x ir` invocations.

## Current Blockers

No blocker remains for the active goal. The self-stage build has shown
parallel-only segfaults in earlier attempts, so keep using
`DUNE_BUILD_FLAGS="-j1"` for baseline setup until that separate issue is
understood.

## Next Step

Commit the four OxCaml changes if this is ready to publish. Commit the initial
`vendor/llvm-project` import as a separate mechanical baseline when ready.
