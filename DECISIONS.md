# Decisions

This file records repository baseline choices.

## Baseline Model

Repository baselines are additive:

```text
ALL -> ALL-PY -> ALL-PY-SRC -> optional specializations
```

Each layer may add files, checks, workflows, or documentation. Later layers may
also override earlier files when the same filename has a different contract.

| Tier                | Applies to                                      | Adds                                                             |
| ------------------- | ----------------------------------------------- | ---------------------------------------------------------------- |
| `ALL`               | Every repository, any language                  | Basic validation, Markdown/YAML/link checks, common config files |
| `ALL-PY`            | Any repository with Python tooling or scripts   | Ruff and Python checks and configuration                         |
| `ALL-PY-SRC`        | Python repositories with a `src/` package       | `ty`, tests, Zensical docs                                       |
| `ALL-PY-SRC-PYPI`   | Publishable Python packages                     | PyPI release workflows                                           |
| `ALL-COURSE`        | Course repositories                             | Course-specific ignores and safe defaults                        |
| `ALL-COURSE-PY-SRC` | Course repositories with Python source packages | Standard course docs, API docs, and course docs config           |

## Ruff Policy

Use Ruff as the safe Python floor.

## Versioning Policy

These repositories are not production deployment targets.
We avoid pinning versions where possible
and try to keep our tools and `uv.lock` updated.

## Override Policy

Later layers may override earlier files only when the same filename has a
different contract.
WHY: course repositories and package repositories have different generated
files, docs navigation, and student-facing surfaces.

Do not duplicate files downstream when the shared `ALL` version is correct.

Valid examples:

```text
ALL/.gitignore -> ALL-COURSE/.gitignore
ALL-PY-SRC/zensical.toml.template -> ALL-COURSE-PY-SRC/zensical.toml.template
```

## Course Repository Policy

Course repositories should stay safe.
They may use the same shared config files as research and package repositories,
but should avoid unnecessary commit-time friction.
In course repositories:

- avoid making Markdown line wrapping too severe;
- keep Ruff as a safe floor;
- avoid strict optional rule families unless the course teaches them;
- keep generated outputs and personalized student files ignored.
