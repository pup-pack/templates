# Templates

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/license/MIT)
[![Check Links](https://github.com/pup-pack/templates/actions/workflows/links.yml/badge.svg?branch=main)](https://github.com/pup-pack/templates/actions/workflows/links.yml)
[![Dependabot](https://img.shields.io/badge/Dependabot-enabled-brightgreen.svg)](https://github.com/pup-pack/templates/security)

<img src="docs/images/pup.png" alt="pup logo" width="110">

> Canonical baseline files for professional Python repositories.

This repository stores reusable project files, configuration files, workflow files,
and documentation scaffolding for professional course, tooling, and software
engineering repositories.

The template layers are additive.
Later layers override earlier layers when a repository profile
needs a more specific version of the same file.

## Layers

Common additive layers include:

```text
ALL
ALL-PY
ALL-PY-SRC
ALL-PY-SRC-PYPI
```

## Requirements

Nothing is required to use the template files manually.
Copy and adapt files as needed.

For managed updates, the `pup-up` command can fetch files from this repository
and apply the appropriate layered baseline to a target repository.

```shell
# dry run: show what would change
uvx pup-up

# same, but force the latest pup-up version
uvx pup-up@latest

# see the differences
uvx pup-up --diff

# actually add and overwrite the files listed (CAUTION: DESTRUCTIVE)
uvx pup-up --write
```

## Developer Command Reference

Open a machine terminal where you want the project:

```shell
git clone https://github.com/pup-pack/templates

cd templates
code .
```

### Add SHAs to Actions and Check

```shell
# Update GitHub Actions and pin all action references to immutable SHAs
uvx gha-tools autoupdate --pin=all --write .github/workflows
uvx gha-tools autoupdate --pin=all --write ALL/.github/workflows
uvx gha-tools autoupdate --pin=all --write ALL-PY/.github/workflows
uvx gha-tools autoupdate --pin=all --write ALL-PY-SRC/.github/workflows
uvx gha-tools autoupdate --pin=all --write ALL-PY-SRC-PYPI/.github/workflows

# Then audit the resulting GitHub configuration for security findings
uvx zizmor@latest .github/
uvx zizmor@latest ALL/.github/
uvx zizmor@latest ALL-PY/.github/
uvx zizmor@latest ALL-PY-SRC/.github/
uvx zizmor@latest ALL-PY-SRC-PYPI/.github/

uvx zizmor@latest --fix=all .github/
uvx zizmor@latest --fix=all ALL/.github/
uvx zizmor@latest --fix=all ALL-PY/.github/
uvx zizmor@latest --fix=all ALL-PY-SRC/.github/
uvx zizmor@latest --fix=all ALL-PY-SRC-PYPI/.github/
```

### Git add-commit-push to GitHub

```shell
# save progress
git add -A
git commit -m "update"
git push -u origin main
```

## Annotations

[.annotations/annotations.md](./.annotations/annotations.md)

## Citation

[CITATION.cff](./CITATION.cff)

## License

[MIT](./LICENSE)
