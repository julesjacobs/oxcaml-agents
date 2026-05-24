# Main Build Times

Build timing records for the main integration checkout.

Prior setup observation:

- `make install` from a clean generated state started around `2026-05-23T17:59:27-0400` and finished around `2026-05-23T18:02:27-0400`, about `180s`. This was inferred from `/tmp/oxcaml-main-normal-install.log` timestamps because the command survived an interrupted turn. Future records below are produced by `scripts/timed-command`.

## llvm-self-stage2-test

- Start: `2026-05-23T22:08:55Z`
- Command: `/usr/bin/env PATH=/Users/julesjacobs/.opam/oxcaml-5.4.0+oxcaml/bin:/Users/julesjacobs/.elan/bin:/opt/homebrew/bin:/opt/homebrew/sbin:/usr/local/bin:/System/Cryptexes/App/usr/bin:/usr/bin:/bin:/usr/sbin:/sbin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/local/bin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/bin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/appleinternal/bin:/opt/pmk/env/global/bin:/Library/Apple/usr/bin:/Library/TeX/texbin:/Users/julesjacobs/.codex/tmp/arg0/codex-arg0LygHoQ:/Users/julesjacobs/.antigravity/antigravity/bin:/opt/homebrew/opt/rustup/bin:/Users/julesjacobs/.opam/modal-kinds-rocq/bin:/Users/julesjacobs/.elan/bin:/Users/julesjacobs/.cargo/bin:/Users/julesjacobs/Library/Application Support/Coursier/bin:/Applications/Codex.app/Contents/Resources:/Users/julesjacobs/Library/Application Support/Coursier/bin make llvm-self-stage2-test LLVM_PATH=/tmp/oxcaml-main-clang-wrapper`
- End: `2026-05-23T22:27:07Z`
- Duration: `1092s`
- Exit status: `2`

## install-for-test

- Start: `2026-05-23T22:27:33Z`
- Command: `/usr/bin/env PATH=/Users/julesjacobs/.opam/oxcaml-5.4.0+oxcaml/bin:/Users/julesjacobs/.elan/bin:/opt/homebrew/bin:/opt/homebrew/sbin:/usr/local/bin:/System/Cryptexes/App/usr/bin:/usr/bin:/bin:/usr/sbin:/sbin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/local/bin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/bin:/var/run/com.apple.security.cryptexd/codex.system/bootstrap/usr/appleinternal/bin:/opt/pmk/env/global/bin:/Library/Apple/usr/bin:/Library/TeX/texbin:/Users/julesjacobs/.codex/tmp/arg0/codex-arg0LygHoQ:/Users/julesjacobs/.antigravity/antigravity/bin:/opt/homebrew/opt/rustup/bin:/Users/julesjacobs/.opam/modal-kinds-rocq/bin:/Users/julesjacobs/.elan/bin:/Users/julesjacobs/.cargo/bin:/Users/julesjacobs/Library/Application Support/Coursier/bin:/Applications/Codex.app/Contents/Resources:/Users/julesjacobs/Library/Application Support/Coursier/bin make install_for_test`
- End: `2026-05-23T22:30:36Z`
- Duration: `183s`
- Exit status: `0`

## stage2-ocamltest

- Start: `2026-05-23T22:30:44Z`
- Command: `/usr/bin/env STAGE_INSTALL=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_llvm_self_stage2_install STAGE_BUILD=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_llvm_self_stage2_main_build FAKE_ROOT=/tmp/oxcaml-self-stage2-ocamltest-src LIST=/tmp/oxcaml-self-stage2-all-minus-asm-list.txt LLVM_WRAPPER=/tmp/oxcaml-main-clang-wrapper tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-23T23:04:22Z`
- Duration: `2018s`
- Exit status: `2`

## stage2-targeted-frame-llvm-codegen

- Start: `2026-05-23T23:11:20Z`
- Command: `/usr/bin/env STAGE_INSTALL=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_llvm_self_stage2_install STAGE_BUILD=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_llvm_self_stage2_main_build FAKE_ROOT=/tmp/oxcaml-self-stage2-ocamltest-src LIST=/tmp/oxcaml-stage2-targeted-list.txt GENERATE_LIST=0 LLVM_WRAPPER=/tmp/oxcaml-main-clang-wrapper tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-23T23:12:29Z`
- Duration: `69s`
- Exit status: `2`

## rebuild-clang-prologue-frame-record

- Start: `2026-05-23T23:19:49Z`
- Command: `ninja clang`
- End: `2026-05-23T23:19:52Z`
- Duration: `3s`
- Exit status: `0`

## stage2-targeted-frame-pointers-prologue-frame-record

- Start: `2026-05-23T23:19:59Z`
- Command: `/usr/bin/env STAGE_INSTALL=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_llvm_self_stage2_install STAGE_BUILD=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_llvm_self_stage2_main_build FAKE_ROOT=/tmp/oxcaml-self-stage2-ocamltest-src LIST=/tmp/oxcaml-stage2-frame-list.txt GENERATE_LIST=0 LLVM_WRAPPER=/tmp/oxcaml-main-clang-wrapper tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-23T23:20:42Z`
- Duration: `43s`
- Exit status: `2`

## rebuild-clang-revert-prologue-frame-record

- Start: `2026-05-23T23:20:50Z`
- Command: `ninja clang`
- End: `2026-05-23T23:20:53Z`
- Duration: `3s`
- Exit status: `0`

## make-install-after-aarch64-fp-flag-fix

- Start: `2026-05-23T23:23:13Z`
- Command: `make install`
- End: `2026-05-23T23:23:18Z`
- Duration: `5s`
- Exit status: `2`

## make-install-after-aarch64-fp-flag-fix-clean

- Start: `2026-05-23T23:23:35Z`
- Command: `make install`
- End: `2026-05-23T23:26:33Z`
- Duration: `178s`
- Exit status: `0`

## llvm-self-stage2-install-after-aarch64-fp-flag-fix

- Start: `2026-05-23T23:26:39Z`
- Command: `make llvm-self-stage2-install LLVM_PATH=/tmp/oxcaml-main-clang-wrapper`
- End: `2026-05-23T23:31:01Z`
- Duration: `262s`
- Exit status: `2`

## llvm-self-stage2-install-after-aarch64-fp-flag-fix-retry

- Start: `2026-05-23T23:32:31Z`
- Command: `make llvm-self-stage2-install LLVM_PATH=/tmp/oxcaml-main-clang-wrapper`
- End: `2026-05-23T23:35:08Z`
- Duration: `157s`
- Exit status: `2`

## llvm-self-stage2-install-force-omit-fp-after-fp-flag-fix

- Start: `2026-05-23T23:37:36Z`
- Command: `make llvm-self-stage2-install LLVM_PATH=/tmp/oxcaml-main-clang-force-omit-fp`
- End: `2026-05-23T23:46:15Z`
- Duration: `519s`
- Exit status: `2`

## stage2-targeted-frame-pointers-after-aarch64-fp-flag-fix-serial-build

- Start: `2026-05-23T23:49:44Z`
- Command: `tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-23T23:50:29Z`
- Duration: `45s`
- Exit status: `2`

## stage0-install-targeted-frame-pointers

- Start: `2026-05-23T23:52:14Z`
- Command: `tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-23T23:52:54Z`
- Duration: `40s`
- Exit status: `2`

## make-install-after-aarch64-restore-x29-trap-fix

- Start: `2026-05-23T23:58:13Z`
- Command: `make install`
- End: `2026-05-24T00:01:07Z`
- Duration: `174s`
- Exit status: `0`

## stage0-install-targeted-frame-pointers-after-restore-x29

- Start: `2026-05-24T00:01:17Z`
- Command: `tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-24T00:02:03Z`
- Duration: `46s`
- Exit status: `2`

## make-install-after-reverting-bad-x29-experiment

- Start: `2026-05-24T00:05:44Z`
- Command: `make install`
- End: `2026-05-24T00:08:02Z`
- Duration: `138s`
- Exit status: `0`

## stage0-install-targeted-frame-pointers-after-reverting-bad-x29

- Start: `2026-05-24T00:08:09Z`
- Command: `tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-24T00:08:52Z`
- Duration: `43s`
- Exit status: `2`

## stage2-install-targeted-frame-pointers-after-mixed-backend-diagnosis

- Start: `2026-05-24T00:16:02Z`
- Command: `tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-24T00:16:02Z`
- Duration: `0s`
- Exit status: `1`

## stage2-install-targeted-frame-pointers-after-mixed-backend-diagnosis

- Start: `2026-05-24T00:16:15Z`
- Command: `tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-24T00:16:51Z`
- Duration: `36s`
- Exit status: `2`

## make-install-after-aarch64-trap-saves-fp-direct-store

- Start: `2026-05-24T00:20:03Z`
- Command: `make install`
- End: `2026-05-24T00:22:22Z`
- Duration: `139s`
- Exit status: `0`

## patched-compiler-stage2-libs-targeted-frame-pointers

- Start: `2026-05-24T00:24:04Z`
- Command: `make -C testsuite one LIST=/tmp/oxcaml-patched-frame-list.txt ocamltest_directory=../_runtest/ocamltest`
- End: `2026-05-24T00:24:09Z`
- Duration: `5s`
- Exit status: `2`

## patched-compiler-stage2-libs-targeted-frame-pointers-after-macos-helper

- Start: `2026-05-24T00:24:42Z`
- Command: `make -C testsuite one LIST=/tmp/oxcaml-patched-frame-list.txt ocamltest_directory=../_runtest/ocamltest`
- End: `2026-05-24T00:24:47Z`
- Duration: `5s`
- Exit status: `2`

## make-install-after-gating-aarch64-trap-fp-restore

- Start: `2026-05-24T00:25:29Z`
- Command: `make install`
- End: `2026-05-24T00:27:44Z`
- Duration: `135s`
- Exit status: `0`

## normal-targeted-frame-pointers-after-macos-helper

- Start: `2026-05-24T00:28:14Z`
- Command: `make -C testsuite one LIST=/tmp/oxcaml-normal-frame-list.txt ocamltest_directory=../_runtest/ocamltest`
- End: `2026-05-24T00:28:15Z`
- Duration: `1s`
- Exit status: `2`

## stage2-targeted-test-matching-native

- Start: `2026-05-24T00:32:54Z`
- Command: `tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-24T00:33:26Z`
- Duration: `32s`
- Exit status: `0`

## stage2-targeted-typing-small-numbers-dir

- Start: `2026-05-24T00:34:02Z`
- Command: `tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-24T00:34:39Z`
- Duration: `37s`
- Exit status: `2`

## make-llvm-self-stage2-install-after-x29-fix

- Start: `2026-05-24T00:46:45Z`
- Command: `make llvm-self-stage2-install LLVM_PATH=/tmp/oxcaml-main-clang-wrapper`
- End: `2026-05-24T00:51:36Z`
- Duration: `291s`
- Exit status: `2`

## make-llvm-self-stage2-install-after-dune-flags-fix

- Start: `2026-05-24T00:55:36Z`
- Command: `make llvm-self-stage2-install LLVM_PATH=/tmp/oxcaml-main-clang-wrapper`
- End: `2026-05-24T01:50:33Z`
- Duration: `3297s`
- Exit status: `0`

## stage2-targeted-typing-small-numbers-after-rebuild

- Start: `2026-05-24T01:51:35Z`
- Command: `tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-24T01:52:09Z`
- Duration: `34s`
- Exit status: `2`

## stage2-targeted-typing-small-numbers-after-wrapper-log-fix

- Start: `2026-05-24T01:53:07Z`
- Command: `tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-24T01:53:38Z`
- Duration: `31s`
- Exit status: `2`

## stage2-targeted-typing-small-numbers-after-always-print-wrapper-counts

- Start: `2026-05-24T01:54:10Z`
- Command: `tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-24T01:54:41Z`
- Duration: `31s`
- Exit status: `2`

## make-install-after-cross-stack-trap-rewrite

- Start: `2026-05-24T02:05:22Z`
- Command: `make install LLVM_BACKEND=1`
- End: `2026-05-24T02:10:01Z`
- Duration: `279s`
- Exit status: `0`

## llvm-self-stage-install-after-cross-stack-trap-rewrite

- Start: `2026-05-24T02:10:33Z`
- Command: `make llvm-self-stage-install LLVM_PATH=/tmp/oxcaml-main-clang-wrapper`
- End: `2026-05-24T02:38:05Z`
- Duration: `1652s`
- Exit status: `0`

## self-stage-frame-pointers-after-cross-stack-trap-rewrite

- Start: `2026-05-24T02:38:58Z`
- Command: `tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-24T02:39:32Z`
- Duration: `34s`
- Exit status: `2`

## self-stage-typing-small-numbers-after-cross-stack-trap-rewrite

- Start: `2026-05-24T02:39:39Z`
- Command: `tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-24T02:40:12Z`
- Duration: `33s`
- Exit status: `2`

## llvm-self-stage-install-after-guarded-trap-chain-rewrite

- Start: `2026-05-24T02:41:56Z`
- Command: `make llvm-self-stage-install LLVM_PATH=/tmp/oxcaml-main-clang-wrapper`
- End: `2026-05-24T03:11:04Z`
- Duration: `1748s`
- Exit status: `0`

## make-install-after-llvm-prologue-fp-delta

- Start: `2026-05-24T06:45:38Z`
- Command: `make install LLVM_BACKEND=1`
- End: `2026-05-24T06:45:38Z`
- Duration: `0s`
- Exit status: `2`

## make-install-after-llvm-prologue-fp-delta

- Start: `2026-05-24T06:45:44Z`
- Command: `make -C main/oxcaml install LLVM_BACKEND=1`
- End: `2026-05-24T06:46:41Z`
- Duration: `57s`
- Exit status: `2`

## make-install-serial-after-llvm-prologue-fp-delta

- Start: `2026-05-24T06:46:47Z`
- Command: `env DUNE_BUILD_FLAGS=-j1 make -C main/oxcaml install LLVM_BACKEND=1`
- End: `2026-05-24T06:50:35Z`
- Duration: `228s`
- Exit status: `0`

## make-install-serial-after-conditional-llvm-prologue-fp-delta

- Start: `2026-05-24T06:53:53Z`
- Command: `env DUNE_BUILD_FLAGS=-j1 make -C main/oxcaml install LLVM_BACKEND=1`
- End: `2026-05-24T06:58:32Z`
- Duration: `279s`
- Exit status: `0`

## make-install-serial-after-removing-arm64-experiment

- Start: `2026-05-24T07:00:10Z`
- Command: `env DUNE_BUILD_FLAGS=-j1 make -C main/oxcaml install LLVM_BACKEND=1`
- End: `2026-05-24T07:04:48Z`
- Duration: `278s`
- Exit status: `0`

## make-install-serial-after-llvm-prologue-fp-chain-rewrite

- Start: `2026-05-24T07:06:27Z`
- Command: `env DUNE_BUILD_FLAGS=-j1 make -C main/oxcaml install LLVM_BACKEND=1`
- End: `2026-05-24T07:11:05Z`
- Duration: `278s`
- Exit status: `0`

## make-install-serial-after-stack-word-pointer-rewrite

- Start: `2026-05-24T07:14:32Z`
- Command: `env DUNE_BUILD_FLAGS=-j1 make -C main/oxcaml install LLVM_BACKEND=1`
- End: `2026-05-24T07:15:41Z`
- Duration: `69s`
- Exit status: `2`

## make-install-serial-after-stack-word-pointer-rewrite-guarded

- Start: `2026-05-24T07:17:04Z`
- Command: `env DUNE_BUILD_FLAGS=-j1 make -C main/oxcaml install LLVM_BACKEND=1`
- End: `2026-05-24T07:20:42Z`
- Duration: `218s`
- Exit status: `0`

## make-install-serial-after-stack-word-pointer-rewrite-only

- Start: `2026-05-24T07:22:49Z`
- Command: `env DUNE_BUILD_FLAGS=-j1 make -C main/oxcaml install LLVM_BACKEND=1`
- End: `2026-05-24T07:27:25Z`
- Duration: `276s`
- Exit status: `0`

## make-install-serial-after-stack-word-pointer-rewrite-uintnat

- Start: `2026-05-24T07:28:01Z`
- Command: `env DUNE_BUILD_FLAGS=-j1 make -C main/oxcaml install LLVM_BACKEND=1`
- End: `2026-05-24T07:32:38Z`
- Duration: `277s`
- Exit status: `0`

## llvm-self-stage2-install-after-stack-word-rewrite

- Start: `2026-05-24T07:35:01Z`
- Command: `env DUNE_BUILD_FLAGS=-j1 make -C main/oxcaml llvm-self-stage2-install LLVM_PATH=/tmp/oxcaml-main-clang-wrapper`
- End: `2026-05-24T08:25:11Z`
- Duration: `3010s`
- Exit status: `0`

## llvm-self-stage2-test-typing-small-numbers-after-stack-word-rewrite

- Start: `2026-05-24T08:25:30Z`
- Command: `env DUNE_BUILD_FLAGS=-j1 STAGE_INSTALL=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_llvm_self_stage2_install STAGE_BUILD=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_llvm_self_stage2_main_build FAKE_ROOT=/tmp/oxcaml-self-stage2-typing-small-numbers-src LIST=/tmp/oxcaml-self-stage2-typing-small-numbers-list.txt GENERATE_LIST=0 LLVM_WRAPPER=/tmp/oxcaml-main-clang-wrapper tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-24T08:26:05Z`
- Duration: `35s`
- Exit status: `0`

## llvm-self-stage2-test-full-after-stack-word-rewrite

- Start: `2026-05-24T08:26:19Z`
- Command: `env DUNE_BUILD_FLAGS=-j1 STAGE_INSTALL=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_llvm_self_stage2_install STAGE_BUILD=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_llvm_self_stage2_main_build FAKE_ROOT=/tmp/oxcaml-self-stage2-full-after-stack-word-src LIST=/tmp/oxcaml-self-stage2-full-after-stack-word-list.txt GENERATE_LIST=1 LLVM_WRAPPER=/tmp/oxcaml-main-clang-wrapper tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-24T08:54:29Z`
- Duration: `1690s`
- Exit status: `2`

## llvm-self-stage2-test-frame-pointers-after-darwin-symbol-parser

- Start: `2026-05-24T08:55:05Z`
- Command: `env DUNE_BUILD_FLAGS=-j1 STAGE_INSTALL=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_llvm_self_stage2_install STAGE_BUILD=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_llvm_self_stage2_main_build FAKE_ROOT=/tmp/oxcaml-self-stage2-frame-pointers-after-darwin-symbol-src LIST=/tmp/oxcaml-self-stage2-frame-pointers-after-darwin-symbol-list.txt GENERATE_LIST=0 LLVM_WRAPPER=/tmp/oxcaml-main-clang-wrapper tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-24T08:55:36Z`
- Duration: `31s`
- Exit status: `2`

## llvm-self-stage2-test-frame-pointers-after-darwin-nm-normalization

- Start: `2026-05-24T08:57:47Z`
- Command: `env DUNE_BUILD_FLAGS=-j1 STAGE_INSTALL=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_llvm_self_stage2_install STAGE_BUILD=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_llvm_self_stage2_main_build FAKE_ROOT=/tmp/oxcaml-self-stage2-frame-pointers-after-darwin-nm-src LIST=/tmp/oxcaml-self-stage2-frame-pointers-after-darwin-symbol-list.txt GENERATE_LIST=0 LLVM_WRAPPER=/tmp/oxcaml-main-clang-wrapper tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-24T08:58:21Z`
- Duration: `34s`
- Exit status: `2`

## llvm-self-stage2-test-frame-pointers-after-darwin-nm-slide

- Start: `2026-05-24T08:58:54Z`
- Command: `env DUNE_BUILD_FLAGS=-j1 STAGE_INSTALL=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_llvm_self_stage2_install STAGE_BUILD=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_llvm_self_stage2_main_build FAKE_ROOT=/tmp/oxcaml-self-stage2-frame-pointers-after-darwin-nm-slide-src LIST=/tmp/oxcaml-self-stage2-frame-pointers-after-darwin-symbol-list.txt GENERATE_LIST=0 LLVM_WRAPPER=/tmp/oxcaml-main-clang-wrapper tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-24T08:59:25Z`
- Duration: `31s`
- Exit status: `2`

## make-install-serial-after-arm64-update-base-pointer

- Start: `2026-05-24T09:01:20Z`
- Command: `env DUNE_BUILD_FLAGS=-j1 make -C main/oxcaml install LLVM_BACKEND=1`
- End: `2026-05-24T09:05:58Z`
- Duration: `278s`
- Exit status: `0`

## llvm-install-test-frame-pointers-after-arm64-update-base-pointer

- Start: `2026-05-24T09:06:22Z`
- Command: `env DUNE_BUILD_FLAGS=-j1 STAGE_INSTALL=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_install STAGE_BUILD=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_build FAKE_ROOT=/tmp/oxcaml-install-frame-pointers-after-arm64-update-base-pointer-src LIST=/tmp/oxcaml-self-stage2-frame-pointers-after-darwin-symbol-list.txt GENERATE_LIST=0 LLVM_WRAPPER=/tmp/oxcaml-main-clang-wrapper tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-24T09:06:57Z`
- Duration: `35s`
- Exit status: `2`

## make-install-serial-after-reverting-arm64-update-base-pointer

- Start: `2026-05-24T09:07:17Z`
- Command: `env DUNE_BUILD_FLAGS=-j1 make -C main/oxcaml install LLVM_BACKEND=1`
- End: `2026-05-24T09:11:53Z`
- Duration: `276s`
- Exit status: `0`

## llvm-install-test-frame-pointers-after-reverting-arm64-update-base-pointer

- Start: `2026-05-24T09:12:37Z`
- Command: `env DUNE_BUILD_FLAGS=-j1 STAGE_INSTALL=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_install STAGE_BUILD=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_build FAKE_ROOT=/tmp/oxcaml-install-frame-pointers-after-reverting-arm64-update-base-pointer-src LIST=/tmp/oxcaml-self-stage2-frame-pointers-after-darwin-symbol-list.txt GENERATE_LIST=0 LLVM_WRAPPER=/tmp/oxcaml-main-clang-wrapper tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-24T09:13:13Z`
- Duration: `36s`
- Exit status: `2`

## make-install-serial-after-arm64-update-base-pointer-spminus16

- Start: `2026-05-24T09:14:15Z`
- Command: `env DUNE_BUILD_FLAGS=-j1 make -C main/oxcaml install LLVM_BACKEND=1`
- End: `2026-05-24T09:18:52Z`
- Duration: `277s`
- Exit status: `0`

## llvm-install-test-frame-pointers-after-arm64-update-base-pointer-spminus16

- Start: `2026-05-24T09:19:00Z`
- Command: `env DUNE_BUILD_FLAGS=-j1 STAGE_INSTALL=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_install STAGE_BUILD=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_build FAKE_ROOT=/tmp/oxcaml-install-frame-pointers-after-arm64-update-base-pointer-spminus16-src LIST=/tmp/oxcaml-self-stage2-frame-pointers-after-darwin-symbol-list.txt GENERATE_LIST=0 LLVM_WRAPPER=/tmp/oxcaml-main-clang-wrapper tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-24T09:19:36Z`
- Duration: `36s`
- Exit status: `0`

## llvm-self-stage2-install-after-arm64-base-pointer-spminus16

- Start: `2026-05-24T09:21:28Z`
- Command: `env DUNE_BUILD_FLAGS=-j1 make -C main/oxcaml llvm-self-stage2-install LLVM_PATH=/tmp/oxcaml-main-clang-wrapper`
- End: `2026-05-24T10:11:24Z`
- Duration: `2996s`
- Exit status: `0`

## llvm-self-stage2-test-frame-pointers-after-arm64-base-pointer-spminus16

- Start: `2026-05-24T10:11:37Z`
- Command: `env DUNE_BUILD_FLAGS=-j1 STAGE_INSTALL=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_llvm_self_stage2_install STAGE_BUILD=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_llvm_self_stage2_main_build FAKE_ROOT=/tmp/oxcaml-self-stage2-frame-pointers-after-arm64-base-pointer-spminus16-src LIST=/tmp/oxcaml-self-stage2-frame-pointers-after-darwin-symbol-list.txt GENERATE_LIST=0 LLVM_WRAPPER=/tmp/oxcaml-main-clang-wrapper tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-24T10:12:11Z`
- Duration: `34s`
- Exit status: `0`

## llvm-self-stage2-test-full-after-arm64-base-pointer-spminus16

- Start: `2026-05-24T10:12:24Z`
- Command: `env DUNE_BUILD_FLAGS=-j1 STAGE_INSTALL=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_llvm_self_stage2_install STAGE_BUILD=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_llvm_self_stage2_main_build FAKE_ROOT=/tmp/oxcaml-self-stage2-full-after-arm64-base-pointer-spminus16-src LIST=/tmp/oxcaml-self-stage2-full-after-arm64-base-pointer-spminus16-list.txt GENERATE_LIST=1 LLVM_WRAPPER=/tmp/oxcaml-main-clang-wrapper tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-24T10:40:38Z`
- Duration: `1694s`
- Exit status: `0`

## llvm-install-test-full-after-arm64-base-pointer-spminus16

- Start: `2026-05-24T10:41:06Z`
- Command: `env DUNE_BUILD_FLAGS=-j1 STAGE_INSTALL=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_install STAGE_BUILD=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_build FAKE_ROOT=/tmp/oxcaml-install-full-after-arm64-base-pointer-spminus16-src LIST=/tmp/oxcaml-install-full-after-arm64-base-pointer-spminus16-list.txt GENERATE_LIST=1 LLVM_WRAPPER=/tmp/oxcaml-main-clang-wrapper tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-24T11:09:21Z`
- Duration: `1695s`
- Exit status: `2`

## llvm-install-test-utils-after-fake-utils-cmo-fix

- Start: `2026-05-24T11:10:36Z`
- Command: `env DUNE_BUILD_FLAGS=-j1 STAGE_INSTALL=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_install STAGE_BUILD=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_build FAKE_ROOT=/tmp/oxcaml-install-utils-after-fake-utils-cmo-fix-src LIST=/tmp/oxcaml-install-utils-after-fake-utils-cmo-fix-list.txt GENERATE_LIST=0 LLVM_WRAPPER=/tmp/oxcaml-main-clang-wrapper tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-24T11:10:36Z`
- Duration: `0s`
- Exit status: `1`

## llvm-install-test-utils-after-fake-utils-cmo-fix

- Start: `2026-05-24T11:10:44Z`
- Command: `env DUNE_BUILD_FLAGS=-j1 STAGE_INSTALL=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_install STAGE_BUILD=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_build FAKE_ROOT=/tmp/oxcaml-install-utils-after-fake-utils-cmo-fix-src LIST=/tmp/oxcaml-install-utils-after-fake-utils-cmo-fix-list.txt GENERATE_LIST=0 LLVM_WRAPPER=/tmp/oxcaml-main-clang-wrapper tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-24T11:11:14Z`
- Duration: `30s`
- Exit status: `0`

## llvm-install-test-full-after-fake-utils-cmo-fix

- Start: `2026-05-24T11:11:25Z`
- Command: `env DUNE_BUILD_FLAGS=-j1 STAGE_INSTALL=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_install STAGE_BUILD=/Users/julesjacobs/git/oxcaml-llvm/main/oxcaml/_build FAKE_ROOT=/tmp/oxcaml-install-full-after-fake-utils-cmo-fix-src LIST=/tmp/oxcaml-install-full-after-fake-utils-cmo-fix-list.txt GENERATE_LIST=1 LLVM_WRAPPER=/tmp/oxcaml-main-clang-wrapper tools/run-llvm-stage5-ocamltest.sh`
- End: `2026-05-24T11:39:43Z`
- Duration: `1698s`
- Exit status: `0`
