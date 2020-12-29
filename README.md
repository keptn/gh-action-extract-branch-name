# GH Action to Extract Branch Name for commits and PRs
![GitHub release (latest by date)](https://img.shields.io/github/v/release/keptn/gh-action-extract-branch-name)

This repo provides a utility GitHub action for the [CI Workflow](https://github.com/keptn/keptn/tree/master/.github/workflows) in the [Keptn Project](https://github.com/keptn). Nevertheless, this action provides a very basic functionality, as in "Extract the current branch name or Pull Request ID", which is useful for creating artifacts based on the branch name (e.g., `docker build . -t my-image:$BRANCH_NAME`).
In addition, as a convenience, it provides the `GIT_SHA` of the commit (if executed on a local branch) or the merge commit (if executed on aPull Request).

*Note*: This requires the full git repo to be cloned, so use `fetch-depth: 0`
```
      - name: Check out code
        uses: actions/checkout@v2
        with:
          fetch-depth: 0 # need to checkout "all commits" for certain features to work (e.g., get all changed files)
```

## Inputs

* GITHUB_REF: Use ${{ github.ref }}
## Outputs

* BRANCH
* BRANCH_SLUG
* GIT_SHA

## Example usage

```
      - name: Check out code
        uses: actions/checkout@v2
        with:
          fetch-depth: 0 # need to checkout "all commits" for certain features to work (e.g., get all changed files)
      - name: Extract branch name
        id: extract_branch
        uses: keptn/gh-action-extract-branch-name@main
        with:
          GITHUB_REF: ${{ github.ref }}
      - name: Print outputs
        run: |
          echo "GIT_SHA=${{ steps.extract_branch.outputs.GIT_SHA }}"
          echo "BRANCH_SLUG=${{ steps.extract_branch.outputs.BRANCH_SLUG }}"
          echo "BRANCH=${{ steps.extract_branch.outputs.BRANCH }}"
```

For a full example, please refer to [.github/workflows/main.yml](.github/workflows/main.yml).
