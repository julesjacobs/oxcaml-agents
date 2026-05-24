# OxCaml LLVM Multi-Agent Workspace

This workspace is for coordinated work on making the OxCaml LLVM backend good
enough to replace the native backend when explicitly enabled.

The workspace is intentionally split into independent OxCaml worktrees so
several agents can build and test at the same time without fighting over Dune
locks, generated files, or local branches. LLVM lives inside each OxCaml
worktree at `vendor/llvm-project`, so an agent can make OxCaml and LLVM changes
on one branch and one PR.

## Layout

```text
~/git/oxcaml-llvm/
  main/
    oxcaml/
      vendor/
        llvm-project/
    llvm-project/  # import-source checkout, not an agent target
    AGENTS.md
    PROGRESS.md
  agents/
    <goal-name>/
      oxcaml/
        agent-state/
          <goal-name>/
            GOAL.md
            PROGRESS.md
        vendor/
          llvm-project/
      AGENTS.md
```

`main/` is the known-good integration checkout. It should stay clean and track
the current personal integration branch.

`agents/<goal-name>/` is where one agent works on one concrete goal. The
canonical goal file is
`agents/<goal-name>/oxcaml/agent-state/<goal-name>/GOAL.md`. It decides whether
that agent may edit OxCaml sources, vendored LLVM sources under
`oxcaml/vendor/llvm-project`, or both.

`main/llvm-project` may exist as an import source for future vendored LLVM
baseline updates. Do not create new agent worktrees from it. The OxCaml
monorepo is the review and PR unit.

## Starting Agent Work

Use this command from the workspace root:

```sh
./scripts/use-or-create-agent <agent-name>
```

If `agents/<agent-name>/` already exists, the command prints its paths. If it
does not exist, the command creates it with branch `jujacobs/<agent-name>`,
pushes that branch to `julesjacobs/oxcaml`, opens a draft OxCaml PR, and records
the PR link in the agent state files.

Work in:

```text
agents/<agent-name>/oxcaml/
```

The task definition is
`agents/<agent-name>/oxcaml/agent-state/<agent-name>/GOAL.md`. Handoff notes
for that agent go in
`agents/<agent-name>/oxcaml/agent-state/<agent-name>/PROGRESS.md`.

Before LLVM-backend work in an agent checkout, initialize per-agent temporary
paths:

```sh
eval "$(../../../scripts/agent-tmp-env)"
```

If you need a clang wrapper:

```sh
eval "$(../../../scripts/write-agent-clang-wrapper /path/to/clang)"
```

Use `$LLVM_PATH` and check `$LLVM_WRAPPER_LOG`. Do not use a shared wrapper or
log.

## Branches

Use branches in Jules's personal fork, not upstream repositories.

Branch names should describe the goal:

```text
jujacobs/llvm-tail-call-domainstate-results
jujacobs/llvm-stack-check-audit
jujacobs/llvm-statepoint-frame-table-contract
```

Do not use branches named `codex/...`.

Agents should branch from the personal integration branch unless their
canonical goal file says otherwise. A typical flow is:

```text
jujacobs/llvm-tail-call-domainstate-results
  -> jujacobs/llvm-backend-integration
```

The integration branch is updated deliberately. Agents should not merge their
own work into it unless their canonical goal file explicitly says to do so.

## Pull Requests

`scripts/use-or-create-agent` opens a draft OxCaml PR against the personal
integration branch when it creates a new agent. These PRs are for tracking,
browsing diffs, review comments, and agent review. They do not mean the work is
ready for upstream.

Vendored LLVM changes should live in the same OxCaml branch and PR as the
OxCaml changes that require them. Use `julesjacobs/llvm-project` only when
maintaining the LLVM import-source checkout or when explicitly asked to publish
a standalone LLVM branch.

Each draft PR should make the current state clear:

```md
Goal:
...

Current state:
- Works: ...
- Fails: ...
- Unknown: ...

Vendored LLVM changes:
- ...

Evidence:
- Command: ...
- Result: ...

Notes:
...
```

GitHub is useful for review and coordination, but custom LLVM-backend validation
is usually local. Do not treat a green GitHub status as proof unless the relevant
LLVM backend path and toolchain were actually exercised.

## Agent Files

Each agent directory has:

- `agents/<goal-name>/oxcaml/agent-state/<goal-name>/GOAL.md`: the current
  task, scope, editable paths, and expected output, plus the OxCaml PR link.
- `agents/<goal-name>/oxcaml/agent-state/<goal-name>/PROGRESS.md`: compact
  handoff notes for that agent.
- `agents/<goal-name>/AGENTS.md`: local instructions for that agent.
- `agents/<goal-name>/oxcaml/`: the agent's OxCaml checkout and code working
  directory.

Keep `agents/<goal-name>/oxcaml/agent-state/<goal-name>/PROGRESS.md` short,
usually one or two pages. It should contain:

- Current claim.
- Evidence: commands, exact results, and important log paths.
- Current blocker.
- Next step.
- Active branches, commits, and PR links.

Delete stale history from
`agents/<goal-name>/oxcaml/agent-state/<goal-name>/PROGRESS.md`. It is a
handoff file, not a diary.

## Agent Directory Creation

Use the helper script from the workspace root:

```sh
./scripts/use-or-create-agent <agent-name>
```

Example:

```sh
./scripts/use-or-create-agent llvm-stack-checks
```

This creates:

```text
agents/llvm-stack-checks/
  oxcaml/        # branch jujacobs/llvm-stack-checks
    agent-state/
      llvm-stack-checks/
        GOAL.md
        PROGRESS.md
  AGENTS.md
```

It also pushes `jujacobs/llvm-stack-checks`, opens a draft PR in
`julesjacobs/oxcaml`, and records the PR link in
`oxcaml/agent-state/llvm-stack-checks/GOAL.md` and
`oxcaml/agent-state/llvm-stack-checks/PROGRESS.md`.

The agent's LLVM edit location is
`agents/llvm-stack-checks/oxcaml/vendor/llvm-project`.

The helper was smoke-tested by creating two agent worktrees from `main/`; those
smoke worktrees have been removed.

## Vendoring LLVM

Use the helper script from the workspace root:

```sh
./scripts/import-vendored-llvm [llvm-source] [oxcaml-checkout]
```

The current vendored baseline was imported from `main/llvm-project` into
`main/oxcaml/vendor/llvm-project`. The source branch and commit are recorded in
`main/oxcaml/vendor/LLVM_BASE.md`. Re-run the helper only for deliberate
baseline updates.

Make the initial vendoring import a mechanical baseline commit or PR. After
that baseline exists, agent branches can change both OxCaml files and files
under `vendor/llvm-project` in the same OxCaml PR. Keep baseline updates
separate from semantic changes when possible.

## Validation Levels

Do not treat the LLVM workflow as requiring four conceptual stages. The
important validation levels are:

1. Normal iteration: the standard installed compiler produced by
   `make install`, with `-llvm-backend`.
2. Full validation: self-stage2, a compiler rebuilt using the LLVM backend.

The scripts have historical names such as `stage4` and `stage5`, and the
self-stage builder has internal boot/runtime/main build directories. Those are
implementation details. Agent work should normally debug with the standard
installed compiler and `-llvm-backend`. Use self-stage2 for full validation or
when the agent goal is explicitly about self-hosting.

## Build Times

Record long-running build and test commands in `main/BUILD_TIMES.md` with:

```sh
./scripts/timed-command main/BUILD_TIMES.md <step-name> <command> ...
```

Agents can check that file to estimate cost before broad validation. Treat the
commands there as historical records, not recipes to copy.

Current rough timings on this machine:

- `make install`: about 180s.
- `make install_for_test`: 183s.
- Self-stage2 install: about 3000-3300s, succeeds.
- Direct `_install` full LLVM-backend testsuite through
  `tools/run-llvm-stage5-ocamltest.sh`: about 1700s, succeeds.
- Self-stage2 full LLVM-backend testsuite through
  `tools/run-llvm-stage5-ocamltest.sh`: about 1700s after the stage2 install,
  succeeds.
- Focused `tests/frame-pointers`: about 35-45s in the LLVM harness.

## Commit Policy

Commit real code or test progress. Progress-only commits are allowed only for
`agent-state/<goal-name>/PROGRESS.md`.

Push committed progress updates to the agent branch so the current handoff
state is visible on the GitHub PR.

Experiments may live on experiment branches, for example:

```text
jujacobs/exp-llvm-stack-check-measurement
```

Candidate fixes should be cleaned up before review, for example:

```text
jujacobs/llvm-stack-check-prologue-fix
```

## Review Policy

Before continuing after a push or review request, agents should check unresolved
GitHub review comments on their active PR.

Agents must verify review comments locally before changing code. Do not blindly
accept comments from review agents. If a comment is rejected, record the reason
briefly in the agent's canonical progress file.

## Testing Rules

Avoid starting multiple independent `make` or `dune` commands at the same time
in the same checkout, because they may contend on dune's lockfile and deadlock.
This does not mean single builds should be serialized: let one build/test
command use its normal internal parallelism.

The custom `tools/run-llvm-stage5-ocamltest.sh` harness is designed for
stage-style validation and is slower than the regular testsuite targets. Use it
when the stage-style environment is needed. For normal installed-compiler work,
prefer the regular testsuite targets, which can use GNU parallel.

When testing LLVM-backend behavior, prove real LLVM use. The usual check is that
`$LLVM_WRAPPER_LOG` contains `-x ir` and the fixed-register flags.

```text
-ffixed-x15 -ffixed-x26 -ffixed-x27 -ffixed-x28
```

Use focused reproducers and tests before broad self-hosting runs. Broad tests
are valuable, but they are expensive and harder to debug when they fail.

If a self-stage or stage2 test fails, first try to reduce it to a focused test
case that already fails with the standard compiler using `-llvm-backend`. That
is the normal debugging target. If the failure only reproduces with
self-stage2, record that fact in the agent's canonical progress file, keep the
smallest self-stage2 reproducer you found, and explain why the standard
`-llvm-backend` compiler does not cover it.

For backend-generated executable failures, try `_install` first:

```sh
STAGE_INSTALL=$PWD/_install \
STAGE_BUILD=$PWD/_build \
NORMAL_BUILD=$PWD/_build \
FAKE_ROOT=$FAKE_ROOT \
LIST=$LIST \
GENERATE_LIST=0 \
LLVM_WRAPPER=$LLVM_WRAPPER \
LLVM_WRAPPER_LOG=$LLVM_WRAPPER_LOG \
  tools/run-llvm-stage5-ocamltest.sh
```

For frame-pointer correctness on ARM64, `_install` is only a quick smoke check:
it links against a normally built stdlib, so it is a mixed-backend run. Prefer
`_llvm_self_stage_install` for cheap frame-pointer iteration and
`_llvm_self_stage2_install` when validating self-hosted behavior.

For benchmarks, use the compiler produced by `make install`, not the boot
compiler.

## Current Main Status

As of 2026-05-24, the main checkout has evidence that both the standard
installed compiler with `-llvm-backend` and a self-stage2 compiler pass the
full LLVM-backend testsuite. See `main/PROGRESS.md` for exact commands, counts,
and wrapper evidence.

Do not claim broader replacement readiness from this alone. New work should
still prove the relevant path with focused standard `-llvm-backend` tests first,
then use self-stage2 as the final integration gate when needed.
