# Wellenplan GitHub Actions

These are the [reusable workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows)
that Wellenplan uses for CI/CD.

## Usage

### Directus Extension

Create the main `.github/workflows/ci.yaml` file for a Directus extension:

```yaml
# .github/workflows/ci.yaml
name: Directus Extension

on:
  push:
    branches:
      - main
  pull_request:
    types: [opened, reopened, synchronize, ready_for_review]

jobs:
  call-workflow:
    uses: wellenplan/actions/.github/workflows/directus-extension.yaml@v0.2.0
    secrets:
      ORGA_USER_TOKEN: ${{ secrets.ORGA_USER_TOKEN }}
      NPM_TOKEN: ${{ secrets.NPM_TOKEN }}
```

### Semantic Release

For repos that have a seperate release process:


```yaml
# .github/workflows/semantic-release.yaml
name: Semantic Release

on:
  push:
    branches:
      - main

jobs:
  call-workflow:
    uses: wellenplan/actions/.github/workflows/semantic-release.yaml@v0.2.0
    secrets:
      ORGA_USER_TOKEN: ${{ secrets.ORGA_USER_TOKEN }}
```
