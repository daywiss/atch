# findings.md

## Findings
- Lowest-risk path to "library" was to separate entrypoint from runtime/CLI logic without changing behavior.
- Renaming `main` in `atch.c` to `atch_cli_main` and adding a tiny `main.c` wrapper enables reusable linkage.
- Adding `libatch.a` as an explicit build artifact works with existing object layout.
- Introducing `libatch.a` before `atch` in Make changed default target implicitly; fixed via `.DEFAULT_GOAL := atch`.
- Session name/path expansion was a good first reusable extraction target because it had clear boundaries and minimal side effects.
- Command alias matching/dispatch is another clean extraction point that reduces CLI frontend coupling.
- Option parsing is a third good extraction target because it is self-contained and shared by multiple command paths.
- Moving command handlers into a runtime module gives clearer separation between CLI orchestration (`atch.c`) and command behavior implementation.

## Decisions
- Keep core behavior unchanged; avoid moving large code blocks in first refactor.
- Preserve legacy CLI semantics while progressively extracting reusable modules.
- Treat this as phase 1+2 internal modularization toward future library split and richer frontends.

## Notes
- `atch_expand_session_name_dup` centralizes bare-name expansion and cache-dir creation behavior for future frontends.
- `atch_resolve_command` centralizes alias policy (`list/l/ls`, `attach/a`, etc.) for reuse outside the CLI binary.
- `atch_parse_options` centralizes option semantics and validation, reducing direct coupling in `atch.c`.
- `atch_cli_runtime` now encapsulates command handlers and shared runtime helpers for potential alternate CLIs/managers.
