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
