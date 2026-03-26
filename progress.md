# progress.md

- Branched from `main` to `feature/lib-refactor`.
- Renamed `main` in `atch.c` -> `atch_cli_main`.
- Added `atch_cli.h` declaration and new `main.c` thin frontend.
- Updated Makefile:
  - added `libatch.a` target from existing runtime objects
  - linked `atch` as `main.o + libatch.a`
  - set `.DEFAULT_GOAL := atch`
- Updated README build section with `make libatch.a`.
- Verified build and smoke:
  - `make`
  - `atch --version`
  - `atch list`

## Phase 2 incremental extraction
- Added `atch_session.c/.h` internal module with reusable session-name expansion (`atch_expand_session_name_dup`).
- Replaced in-file session expansion logic in `atch.c` with module call.
- Added `atch_session.o` to `libatch.a` linkage.
- Rebuilt and re-smoke-tested CLI (`--version`, `list`, `current` outside session rc=1).

## Phase 2b incremental extraction
- Added `atch_cmd.c/.h` for command alias resolution (`atch_resolve_command`).
- Replaced command dispatch `if` chain in `atch.c` with enum+switch using resolver.
- Added `atch_cmd.o` to library build.

## Phase 2c incremental extraction
- Added `atch_cli_opts.c/.h` for option parsing (`atch_parse_options`) and log-size parsing.
- Removed parse-size/parse-options implementation from `atch.c`; now uses module API.
- Added `atch_cli_opts.o` to `libatch.a` linkage.
- Rebuilt and smoke-verified (`--version`, `list`).
