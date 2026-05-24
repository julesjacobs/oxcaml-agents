# Main Integration Checkout

This directory is the known-good integration checkout.

Do not do exploratory work here. Use `../scripts/create-agent` to create a
per-goal agent directory and work there. Before creating one, check whether an
existing `../agents/<goal-name>/` already matches the task; if it does, use
that directory instead.

The expected branches are:

- `oxcaml`: `jujacobs/llvm-backend-integration`

Vendored LLVM lives at `oxcaml/vendor/llvm-project`. A sibling
`main/llvm-project` checkout may exist as an import source, but it is not an
agent target.

Use this checkout to verify the integration state and to create new OxCaml
branches for agent work.

The validation levels are direct `_install` and self-stage2. The historical
`stage4`/`stage5` script names are implementation details, not a requirement
for four conceptual stages. When investigating a failure, reduce it to a
focused direct `_install` test whenever possible; use self-stage2 as the final
self-hosting proof or when the failure genuinely only reproduces there.

When a nested repo `AGENTS.md` says to test or format, do it only when it makes
sense for the current step. Full tests can take a long time, so avoid running
them while still reducing or investigating a failure. If an instruction says to
use `-s`, skip `-s` when command output is needed for debugging.
