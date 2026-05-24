# Main Integration Checkout

This directory is the known-good integration checkout.

Do not do exploratory work here. Start agent work from the workspace root with
`scripts/use-or-create-agent <agent-name> [branch-suffix]`, then work in the
agent directory it prints.

The expected branches are:

- `oxcaml`: `jujacobs/llvm-backend-integration`

Vendored LLVM lives at `oxcaml/vendor/llvm-project`. A sibling
`main/llvm-project` checkout may exist as an import source, but it is not an
agent target.

Use this checkout to verify the integration state and to create new OxCaml
branches for agent work.

The normal iteration path is the standard installed compiler with
`-llvm-backend`. Self-stage2 is for full validation or for failures that
genuinely only reproduce there. The historical `stage4`/`stage5` script names
are implementation details, not a requirement for four conceptual stages.

When a nested repo `AGENTS.md` says to test or format, do it only when it makes
sense for the current step. Full tests can take a long time, so avoid running
them while still reducing or investigating a failure. If an instruction says to
use `-s`, skip `-s` when command output is needed for debugging.
