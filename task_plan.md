# task_plan.md

## Goal
Refactor `atch` into an internal library-oriented layout while maintaining existing behavior.

## Phases
| Phase | Description | Status | Success Criteria |
|---|---|---|---|
| 1 | Entrypoint separation + library artifact | complete | `main.c` thin CLI wrapper, `libatch.a` builds, `atch` behavior unchanged in smoke checks |
| 2 | Extract internal modules (path/session/control parsing helpers) | todo | Reduced coupling in `atch.c`; same CLI behavior |
| 3 | Public/internal API shaping | todo | Stable internal headers for reuse by future frontends |
| 4 | Validation/docs | in_progress | README and make usage updated; additional tests pending |
