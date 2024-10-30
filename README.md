# parse-semver-ref-action

This action parses a GitHub ref (e.g. `refs/tags/v1.2.3`) and outputs it's components.

## Usage

```yaml
on:
  release:
    types: [published]

jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Parse ref
        uses: ryangoree/parse-semver-ref-action@v1
        id: parse
        with:
          ref: ${{ github.ref }}

      - name: Do something with the parsed ref
        run: |
          echo "Major: ${{ steps.parse.outputs.major }}"
          echo "Minor: ${{ steps.parse.outputs.minor }}"
          echo "Patch: ${{ steps.parse.outputs.patch }}"
          echo "Prerelease: ${{ steps.parse.outputs.prerelease }}"
          echo "Build: ${{ steps.parse.outputs.build }}"
          echo "Name: ${{ steps.parse.outputs.name }}"
          echo "Scope: ${{ steps.parse.outputs.scope }}"
```

## Inputs

### `ref` _(Required)_

The github ref to parse (e.g. refs/tags/v1.0.0, refs/tags/pkg@v1.2.3).

## Outputs

### `ref`

The ref that was parsed.

### `matched`

`"true"` if the ref matched the semver pattern, `"false"` otherwise.

### `major`

The major version number from the tag (e.g. `1` from `refs/tags/v1.2.3`).

### `minor`

The minor version number from the tag (e.g. `2` from `refs/tags/v1.2.3`).

### `patch`

The patch version number from the tag (e.g. `3` from `refs/tags/v1.2.3`).

### `prerelease`

The prerelease version from the tag (e.g. `alpha` from `refs/tags/v1.2.3-alpha`).

### `build`

The build version from the tag (e.g. `build` from `refs/tags/v1.2.3+build`).

### `name`

The package name from the tag (e.g. `pkg` from `refs/tags/pkg@v1.2.3`).

### `scope`

The package scope (if any) from the tag (e.g. `org` from `refs/tags/@org/pkg@v1.2.3`).
