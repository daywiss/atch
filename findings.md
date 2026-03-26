# findings.md

## Findings
- Lowest-risk path to "library" was to separate entrypoint from runtime/CLI logic without changing behavior.
- Renaming `main` in `atch.c` to `atch_cli_main` and adding a tiny `main.c` wrapper enables reusable linkage.
- Adding `libatch.a` as an explicit build artifact works with existing object layout.
- Introducing `libatch.a` before `atch` in Make changed default target implicitly; fixed via `.DEFAULT_GOAL := atch`.
- Session name/path expansion was a good first reusable extraction target because it had clear boundaries and minimal side effects.

## Decisions
- Keep core behavior unchanged; avoid moving large code blocks in first refactor.
- Preserve current CLI parser/dispatcher in `atch.c` for now.
- Treat this as phase 1+2 internal modularization toward future library split.

## Notes
- `atch_expand_session_name_dup` now centralizes bare-name expansion and cache-dir creation behavior for future frontends.
