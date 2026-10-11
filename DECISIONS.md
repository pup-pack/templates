# Decisions

> Record repository decisions.

## Baseline Model

Repository baselines are additive:

```text
ALL -> ALL-PY -> ALL-PY-SRC -> optional specializations
```

Each layer may add files, checks, workflows, or documentation. Later layers may
also override earlier files when the same filename has a different contract.

| Tier              | Applies to                                    | Adds                                                             |
| ----------------- | --------------------------------------------- | ---------------------------------------------------------------- |
| `ALL`             | Every repository, any language                | Basic validation, Markdown/YAML/link checks, common config files |
| `ALL-PY`          | Any repository with Python tooling or scripts | Ruff and Python checks and configuration                         |
| `ALL-PY-SRC`      | Python repositories with a `src/` package     | `ty`, tests, Zensical docs                                       |
| `ALL-PY-SRC-PYPI` | Publishable Python packages                   | PyPI release workflows                                           |

## Versioning Policy

These repositories are not production deployment targets.
We avoid pinning versions in `pyproject.toml` where possible
and try to keep our tools and `uv.lock` updated for
security, compatibility, and maintenance.

## Override Policy

Later layers may override earlier files when the same filename has a
different contract.
