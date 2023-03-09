# Wellenplan GitHub Actions

These are the [reusable workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows)
that Wellenplan uses for CI/CD.

## Usage

See below for copy-pasteable examples of the provided actions.

If you need multiple actions to happen then it's up to you to combine them as needed. Please add an example if you use the same combo more than once.

Please remember to replace `@main` with the current version of this repo when you use these actions. You should also add the following `.github/debendabot.yaml` file.

```yaml
version: 2
updates:
  - package-ecosystem: "github-actions"
    directory: "/"
    schedule:
      interval: "daily"
    commit-message:
      prefix: "chore(ci): "
```

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
    uses: wellenplan/actions/.github/workflows/directus-extension.yaml@main
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
    uses: wellenplan/actions/.github/workflows/semantic-release.yaml@main
    secrets:
      ORGA_USER_TOKEN: ${{ secrets.ORGA_USER_TOKEN }}
```
